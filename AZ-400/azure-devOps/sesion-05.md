# Azure DevOps - Sesión 05

---

## 1. Objetivo de la sesión

Construir un flujo completo de **CI/CD** para un proyecto Java/Spring Boot, integrando análisis de calidad de código con **SonarCloud**, empaquetado en **Docker**, y publicación en un **registry** de imágenes, como paso previo al despliegue en Kubernetes (que se abordará en la siguiente sesión con Helm).

---

## 2. Integración con SonarCloud

### 2.1 Creación de cuenta y organización en SonarCloud

- Se recomienda crear la cuenta con **cualquier proveedor menos GitHub**, ya que iniciar sesión con GitHub prioriza el flujo de "GitHub Actions" en lugar del de Azure DevOps, complicando la integración.
- Al crear la organización en SonarCloud, se debe elegir la opción de **crear manualmente** (no importar), usando un nombre único (ej. nombre + apellido) para evitar colisiones con otros usuarios.
- Se debe usar el plan **Free**: es de uso académico, el código queda **público**, por lo que se recomienda **no subir código real de cliente**, solo proyectos propios o de práctica.

### 2.2 Creación del proyecto en SonarCloud

- Se crea manualmente un nuevo proyecto ("Analyze new Project" → "Create Project Manually").
- **Estándar recomendado:** usar como nombre del proyecto en SonarCloud el mismo nombre del repositorio de Azure DevOps, para mantener trazabilidad entre ambos sistemas.
- El proyecto debe configurarse como **público** (el plan gratuito no permite privados sin más requisitos).
- Importante: el **Project Key** no se puede modificar luego de creado, solo el nombre visible.

### 2.3 Personal Access Token de SonarCloud

- Se genera desde **My Account → Security → Generate Token**, asignándole un nombre descriptivo.
- Este token se usará para crear la conexión de servicio (Service Connection) desde Azure DevOps hacia SonarCloud.

---

## 3. Service Connections en Azure DevOps

### 3.1 Concepto

Una **Service Connection** es un punto de conexión/autenticación entre Azure DevOps y servicios o recursos externos (otro Azure DevOps, un Azure Service Bus, un registry Docker, SonarCloud/SonarQube, etc.). Se configuran desde **Project Settings → Service Connections → New Service Connection**.

### 3.2 Conexión a SonarCloud

Pasos para crear la conexión:

1. Buscar el conector **SonarCloud** dentro del catálogo de Service Connections.
2. Pegar el **token** generado previamente en SonarCloud y presionar **Verify** para validar la conexión.
3. Asignar un **nombre estándar y descriptivo** a la conexión (ej. identificando claramente que se trata del analizador de código, ya que a diferencia de otros conectores, este no suele diferenciarse por ambiente).
4. Marcar la opción **"Grant access permission to all pipelines"**, requisito indispensable para que los pipelines puedan usar la conexión.

---

## 4. Configuración del análisis SonarCloud dentro del pipeline (YAML)

### 4.1 Estructura estándar de 3 pasos

El análisis de SonarCloud en un pipeline sigue típicamente esta secuencia:

```text
Prepare (Preparar)
    ↓
Analyze (Analizar)
    ↓
Publish (Publicar)
```

- El paso de **Prepare** debe ejecutarse **antes** del paso de compilación (Build).
- El paso de **Publish** debe ejecutarse **después** del Build/Analyze.
- La cantidad exacta de pasos varía según el lenguaje: en proyectos Java (Maven/Gradle) el análisis suele quedar embebido dentro del propio paso de build, mientras que para otros lenguajes se requieren los 3 pasos explícitos.

### 4.2 Configuración del paso "Prepare"

En este paso se debe indicar:

- El **endpoint** (Service Connection) hacia SonarCloud creado previamente.
- La **organización** de SonarCloud a utilizar.
- El **tipo de análisis**, según el ecosistema del proyecto:
    - **Integrado/nativo**: para proyectos Maven o Gradle (Java), la integración viene prácticamente lista, solo requiere indicar los atributos del proyecto (Project Key y Project Name, provistos por SonarCloud).
    - **Genérico (Scanner CLI)**: para lenguajes sin integración nativa (ej. Angular, React, Node), se descarga y configura manualmente el **SonarScanner**, especificando parámetros como el directorio de origen del código, la versión del lenguaje, etc.
    - Casos particulares: **.NET** dispone de su propio *builder scan* (repositorio dedicado).

### 4.3 Ejecución del análisis (para Maven/Java)

- Para proyectos Maven, dentro de la sección **Settings** existe la opción de habilitar directamente el analizador (**"Run SonarQube or SonarCloud analysis"**), la cual agrega automáticamente las líneas necesarias al YAML sin necesidad de un paso separado.

### 4.4 Configuración del paso "Publish"

- Publica los resultados del análisis hacia el dashboard de SonarCloud.
- Incluye un parámetro de **timeout** (tiempo máximo de espera para la publicación, configurado en segundos; el valor por defecto ronda los 5 minutos). Se recomienda incrementarlo en proyectos grandes que tarden más en publicar resultados.

### 4.5 Quality Gate y cobertura de código

- Es posible configurar reglas de calidad (**Quality Gate Settings**) dentro de SonarCloud, como exigir un porcentaje mínimo de cobertura de código para que el análisis "pase".
- Estas reglas se configuran directamente en la plataforma de SonarCloud, no en el pipeline YAML.

---

## 5. Construcción del pipeline de CI/CD (YAML)

### 5.1 Organización del archivo

- Se creó un archivo YAML dedicado dentro de la carpeta `devops` del repositorio (ej. `backend-cicd.yml`), replicando la estructura vista en la sesión anterior.
- Aclaración importante: **YML** y **YAML** son equivalentes; ambas extensiones son interpretadas de la misma manera y pueden coexistir sin conflicto en un mismo proyecto.
- El pipeline se organizó dentro de la carpeta lógica correspondiente en el portal de Azure DevOps (ej. "CICD"), igual que se hizo en la sesión anterior.

### 5.2 Etapas del flujo completo

Se definió conceptualmente el flujo integral de CI/CD para el proyecto:

```text
1. Compilar el proyecto (Build)
2. Analizar calidad de código (SonarCloud: Prepare → Analyze → Publish)
3. Generar imagen Docker (empaquetar el binario)
4. Subir la imagen a un Registry (Docker Hub / ACR / etc.)
5. Desplegar en Kubernetes (próxima sesión, con Helm)
```

- Se aclaró conceptualmente la diferencia entre CI y CD: el **CI** normalmente se asocia a ramas de trabajo (feature, bugfix, hotfix) y se dispara en cada commit; el **CD** depende del modelo de gestión de ramas de la organización (Git Flow, Trunk-Based Development, GitHub Flow, etc.) y suele estar más orientado al despliegue hacia ambientes.

### 5.3 Generación del Dockerfile

- Se generó un Dockerfile para Java 21 + Maven, optimizado para tiempos de ejecución, usando una herramienta de IA como asistente (aclarando explícitamente el prompt usado: actuar como experto en Docker).
- El Dockerfile fue ajustado para copiar el artefacto (`.jar`) generado por Maven, sin necesidad de volver a compilar dentro del propio contenedor Docker (ya que el binario se genera previamente en el paso de Build del pipeline).

### 5.4 Tarea Docker en el pipeline

- Se agregó una tarea de tipo **Docker** al pipeline, configurada para realizar **Build and Push** (construir la imagen y subirla al registry) en un solo paso.
- Parámetros clave a configurar:
    - **Registry / Service Connection** hacia el destino de la imagen (Docker Hub, Azure Container Registry, u otro).
    - **Ruta del Dockerfile** dentro del repositorio.
    - **Nombre del repositorio de la imagen** (debe respetar mayúsculas/minúsculas y coincidir con la cuenta/organización de destino).
    - **Tag de la imagen**, comúnmente asociado al número de build.
- Advertencia práctica: algunos proveedores de nube/registries (se mencionó el caso de Huawei) no soportan cierta metadata adicional que Azure DevOps agrega por defecto; en esos casos debe desmarcarse esa opción para evitar errores.

### 5.5 Service Connection hacia el Registry Docker

- Se creó una nueva Service Connection de tipo **Docker Registry**, usando **Docker Hub** como destino (por ser gratuito).
- Requiere usuario y contraseña de la cuenta de Docker Hub.
- **Importante:** el nombre de usuario/organización configurado en el registry debe coincidir con la cuenta bajo la cual se va a publicar la imagen — no es posible subir imágenes a una cuenta/organización ajena sin permisos explícitos.
- Se aclaró que el flujo es agnóstico del proveedor: cambiar de Docker Hub a Azure Container Registry (u otro) solo implica reemplazar la URL del registry y las credenciales; el resto de la configuración del pipeline permanece igual. Esto se explicó como una decisión pedagógica deliberada: no atar el flujo a un proveedor específico de nube.

### 5.6 Nota sobre Azure Container Registry (ACR) y AKS

- Se explicó que, en el caso específico de **Azure Kubernetes Service (AKS)**, es recomendable **vincular el ACR directamente al clúster** desde su creación. Si el clúster y el ACR se crean por separado, el despliegue puede fallar con errores de autorización (401) al intentar descargar la imagen, ya que el clúster no tiene permisos automáticos hacia un registry externo no vinculado.

---

## 6. Depuración de errores comunes durante la construcción del pipeline

Durante la práctica en vivo surgieron varios problemas reales, útiles como referencia:

- **Ruta del Dockerfile fuera de contexto:** el Dockerfile hacía referencia al artefacto compilado (`target/*.jar`) asumiendo que este se encontraba dentro del mismo contexto de build; al no ser así, fue necesario ajustar la ruta (agregar el prefijo de carpeta correspondiente, ej. `devops/`) para que Docker pudiera localizar el archivo `.jar` generado por Maven.
- **Nombre de la imagen mal formado:** al configurar el destino de la imagen en la tarea Docker, se debe respetar el orden `usuario/nombre-imagen` cuando se trabaja con Docker Hub, ya que de lo contrario el registry rechaza la subida por no reconocer el contexto (organización/usuario) de destino.
- **Agentes “colgados” o procesos zombis:** se mostró cómo, en un agente self-hosted, un proceso anterior (por ejemplo relacionado con Docker) puede quedar bloqueado impidiendo nuevas ejecuciones; se recurrió a comandos como `ps aux | grep` y `kill -9` para identificar y terminar el proceso, o en última instancia reiniciar el agente.

---

## 7. Próximos pasos anunciados

- Para la siguiente sesión se trabajará el **despliegue en Kubernetes**, comparando dos enfoques:
    - **kubectl**: cliente binario para administrar el clúster de forma directa (más comandos, más manual).
    - **Helm**: gestor de paquetes/charts para Kubernetes, permite desplegar múltiples objetos con un solo comando y facilita el rollback, considerado el enfoque más profesional y mantenible.
- Se anunció que el profesor creará un repositorio propio con un **Helm Chart genérico** (ej. `devops-help`), que podría evolucionar hacia un framework reutilizable para desplegar distintos tipos de servicios (no solo backend).
- Se confirmó el cronograma: la siguiente sesión cerrará **CI/CD hasta el ambiente de UAT**, tras lo cual se tomará el **examen teórico** y se asignará el **trabajo práctico entregable** (un repositorio con su respectivo archivo YAML de pipeline).

---

## Ideas Clave de la Sesión

- Se integró **SonarCloud** al flujo de CI mediante una Service Connection y los pasos estándar **Prepare → Analyze → Publish**.
- El nivel de integración con SonarCloud depende del lenguaje: nativo en Maven/Gradle (Java), manual vía Scanner CLI en otros ecosistemas (Angular, Node, etc.).
- Se recomienda usar un **estándar de nombres consistente** para Service Connections y proyectos (ej. igualar el nombre del proyecto SonarCloud al del repositorio).
- Se construyó un pipeline de **CI/CD completo**: compilación → análisis de calidad → generación de imagen Docker → publicación en un Registry.
- El flujo se diseñó de forma **agnóstica al proveedor de nube**: el mismo patrón aplica para Docker Hub, Azure Container Registry, u otros registries, cambiando solo credenciales y URL.
- En AKS es recomendable vincular el ACR desde la creación del clúster para evitar errores de autorización al desplegar imágenes.
- Se practicó la **depuración de errores reales** de pipeline: rutas de contexto incorrectas en Docker, nombres de imagen mal formados, y procesos colgados en el agente self-hosted.
- La siguiente sesión abordará el **despliegue en Kubernetes con Helm**, cerrando el flujo de CI/CD hasta el ambiente de UAT, previo al examen y trabajo final del curso.