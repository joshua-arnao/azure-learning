# Azure DevOps - Sesión 03

---

## Resolución de Conflictos en Git (Repaso Práctico)

Se retomó el flujo de trabajo con ramas para explicar cómo se generan y resuelven conflictos al hacer Pull Requests.

### Flujo típico de trabajo con ramas

```text
Rama main (o base)
    ↓
Se crea una nueva rama (feature)
    ↓
Ambas ramas son modificadas por distintos integrantes
    ↓
Se genera un Pull Request
    ↓
Puede aparecer un conflicto
```

### ¿Por qué ocurre un conflicto?

Sucede cuando dos ramas modifican el mismo archivo (o las mismas líneas) de forma distinta y Azure DevOps no puede fusionar los cambios automáticamente. La interfaz gráfica detecta el conflicto pero no lo resuelve por sí sola.

### Pasos para resolver conflictos manualmente (por comandos)

1. **Sincronizar ambas ramas antes de resolver cualquier conflicto**
    - Ubicarse en cada rama (`git status`) y traer los cambios remotos con `git pull origin <rama>`.
    - Regla clave: siempre se estabiliza la rama *feature*, no la rama *main*.

2. **Ubicarse en la rama que se va a "estabilizar"** (la rama feature) y traer los cambios de la rama principal:
   ```text
   git merge main
   ```
    - Si no hay conflictos: aparece un mensaje de "auto merge".
    - Si hay conflictos: Git marca el archivo afectado.

3. **Abrir el archivo en conflicto** (se usó `nano` como editor, aunque puede usarse cualquiera) e interpretar las marcas de conflicto:
    - Lo que aparece bajo `<<<<<<< HEAD` son los cambios de **tu rama**.
    - Lo que aparece bajo `=======` hasta `>>>>>>>` son los cambios de la rama **main**.

4. **Decidir la resolución del conflicto** según:
    - Coordinación entre las personas que modificaron el código.
    - Juicio experto/técnico (por ejemplo, si ambas validaciones deben convivir en la lógica).
    - Consulta con el área funcional si aplica.
    - Eliminar las líneas de marcado (`<<<<<<<`, `=======`, `>>>>>>>`) y dejar el código final.

5. **Marcar el conflicto como resuelto:**
   ```text
   git add <archivo>
   ```

6. **Verificar** con `git status` que ya no aparezcan archivos pendientes de merge.

7. **Confirmar el merge:**
   ```text
   git commit -m "mensaje descriptivo (ej: merge from main to feature)"
   ```
    - Se recomienda usar un estándar propio y consistente para los mensajes de commit.

8. **Subir los cambios resueltos al repositorio remoto:**
   ```text
   git push origin <rama>
   ```

9. Con el conflicto resuelto en el remoto, el revisor puede aprobar y completar el Pull Request desde la interfaz de Azure DevOps.

### Ideas clave sobre conflictos

- Los conflictos se resuelven siempre primero en **local**, no directamente en el servidor remoto.
- Resolver por comandos (sin plugins) da mayor control y evita errores típicos de las herramientas gráficas.
- El flujo general es: **sincronizar → merge local → resolver conflicto → add → commit → push → completar PR**.
- Al completar un Pull Request, la rama feature puede eliminarse del remoto (no afecta la rama local).

---

## Introducción a Azure Pipelines

Configuración de **Azure Pipelines** para CI/CD.

### Pipeline components 
Sincronizar eventos de las siguientes manera:
- **Triggers**: Lanzan los pipelines.
- **Step**: Es un pequeño bloque de construcción del pipeline, puede ser task/script.
- **Task**: Actividad con un conjunto de entradas.
- **Job**: Conjunto de steps/tasks.
- **Stage**: Grupo que puede contener jobs.
- **Agente**: Maquina que ejecuta los jobs de los pipeline.

### Tipos de pipelines
- **Classic(Task group)**: Agrupa una secuencia de tareas que pueden ser reutilizados dentro de un build/release pipeline de un proyecto. Se trabaja dede una Interfas de usuario(UI).
  > El pipeline no esta en el código fuente.
- **Yaml(Templates)**: Editor de texto.
  > El pipeline si vive en el código fuente.

### Build Trigger
- **Continuos integration triggers**: Actualización de un repositorio branch/tag
- **Pull request triggers**: Abrir/Actualizar un pull request.
- **Pipeline/Build completion triggers**: Desencadenado por terminación de un pipeline.
- **Other triggers**: Programando, comentario, registros cerrados.

### Personal Access Token (PAT)

Antes de configurar un agente, se requiere generar un **Personal Access Token (PAT)**, necesario para autenticar el agente contra la organización.

Pasos:
1. Ir al ícono de usuario dentro de la organización → **Personal Access Tokens**.
2. Crear un **nuevo token**:
    - Nombre descriptivo (ej. referencia al proyecto/curso).
    - Organización a la que tendrá acceso (por seguridad, se recomienda limitarlo a una organización específica, no a todas).
    - Tiempo de expiración (ej. 30 días).
    - Scope: **Custom defined**, habilitando **"Show all scopes"** y seleccionando el scope necesario para agentes.
3. Guardar el token generado de forma segura ("guardarlo como oro"), ya que no se puede visualizar nuevamente.
4. Si se pierde, el token puede ser **editado, revocado o regenerado**, pero no hay límite en la cantidad de tokens que se pueden crear.

### Agent Pools (Grupos de Agentes)

Dentro de **Organization Settings → Agent Pools** se gestionan los agentes que ejecutarán los pipelines.

- Existe un **pool por defecto** ("Azure Pipelines") que usa infraestructura compartida de Microsoft:
    - Es de uso gratuito limitado (requiere activación mediante formulario si es la primera vez, con demora de aprobación de días).
    - Entra en una cola de atención compartida.
- También existe la opción de usar **agentes hosteados en GitHub**.
- Y la opción explicada en la sesión: **crear un Agent Pool propio (self-hosted)**, instalando el agente en una máquina propia.

### Instalación de un Agente Self-Hosted

Requisito principal: **una máquina con acceso a Internet** (puede ser una VM en la nube, una máquina personal, o un servicio gratuito de máquina virtual en la nube).

Pasos generales:
1. En **Agent Pools → Default → New Agent**, elegir el sistema operativo (Windows, macOS o Linux) y la **arquitectura** del procesador:
    - **x64**: arquitectura estándar (Intel, la mayoría de laptops personales/de trabajo).
    - **ARM64**: arquitectura de chips como Apple Silicon (M1, M2, etc.).
    - En Windows se identifica en "Mi PC → Propiedades"; en macOS/Linux se identifica con el comando `uname -a`.
2. Descargar el paquete del agente correspondiente y descomprimirlo en una carpeta dedicada (ej. `myagent`).
3. Ejecutar el script de configuración (`config.sh` / `config.cmd`):
    - Aceptar términos y condiciones.
    - Ingresar la **URL del servidor**, que corresponde al dominio de la **organización** (no del proyecto).
    - Ingresar el **tipo de autenticación** (PAT) y pegar el token generado previamente.
    - Seleccionar el **Agent Pool** (por defecto o personalizado).
    - Asignar un **nombre al agente**.
    - Definir la carpeta de trabajo (se recomienda dejar la ruta por defecto).
    - Opción de **ejecutar como servicio**: en ambientes productivos permite que el agente se reinicie automáticamente junto con la máquina; en entornos académicos/de aprendizaje se recomienda **no habilitarlo**, ya que puede generar conflictos al instalar múltiples agentes.
4. Ejecutar el agente (`run.sh` / `run.cmd`); el agente queda **escuchando tareas ("listening for jobs")**.
5. Verificar la conexión exitosa desde **Agent Pools → Agents** en Azure DevOps (debe figurar como "online").

## Consideraciones sobre software instalado en el agente

- Todo software o runtime que un pipeline necesite ejecutar (Java, Node, Maven, etc.) debe estar **instalado y correctamente configurado en la máquina donde corre el agente**.
- No basta con instalar el software: también debe estar correctamente configurado (ej. variables como `JAVA_HOME`) y, en algunos casos, requiere **reiniciar la máquina** para que se reconozca.
- Se recomienda **validar primero en local** que el comando/herramienta funciona correctamente antes de integrarlo al pipeline.
- Un agente puede tener múltiples versiones o servicios en conflicto (ej. distintas versiones de Node para distintos proyectos); este escenario se resuelve típicamente con **contenedores (Docker)**, donde cada agente corre dentro de una imagen con la configuración específica que necesita.
- Se puede tener más de un agente Docker corriendo en la misma máquina física.
- Elección del sistema operativo del agente: depende del tipo de proyecto a ejecutar.
    - Proyectos multiplataforma → se recomienda **Linux**.
    - Proyectos con dependencia de tecnologías Microsoft (ej. IIS, .NET tradicional) → puede requerir **Windows**.
    - Proyectos iOS → requieren **macOS**.

## Creación de un Pipeline (modo interactivo / Assistant)

Se mostró la forma **interactiva** (asistida) para crear un pipeline, recomendada como punto de partida para aprender el ecosistema YAML:

1. Al crear un pipeline nuevo, Azure DevOps ofrece un asistente visual tipo "drag and drop" donde se agregan **Jobs** y **Steps**.
2. Cada acción agregada en el asistente se traduce automáticamente a líneas de código **YAML** equivalentes (botón "View YML").
3. Dentro de un **Job** se pueden agregar múltiples **Tasks** desde un catálogo amplio: compilación, pruebas, empaquetado, despliegue, utilitarios, Terraform, y más — incluso se puede acceder a un **Marketplace** de tareas de la comunidad, o crear tareas propias y publicarlas ahí.
4. Se ejecutó un ejemplo simple ("Hola Mundo") usando una tarea de tipo **Command Line** con los comandos `ls -l` y `pwd`, para listar archivos y mostrar la ruta de trabajo del agente.
    - En Windows, la tarea equivalente es **PowerShell**.
    - Existen dos modalidades para el contenido del script: **inline** (el código se escribe directamente) o **file path** (se referencia un archivo dentro del repositorio).
5. Al guardar (**Save**), el pipeline se registra como un archivo `azure-pipelines.yml` en la raíz del repositorio (se puede personalizar el nombre y la ubicación).
6. Al ejecutar (**Run/Queue**), se genera un **Job** que corre en el agente seleccionado; el progreso y el log de ejecución pueden verse en tiempo real.

### Ventaja del modo interactivo

La configuración del Job se gestiona desde la interfaz sin necesidad de que el código YAML "viva" versionado inicialmente en el código fuente — útil para aprender y experimentar antes de trabajar directamente en YAML.

---

# Alternativas para levantar una máquina de pruebas (sin infraestructura propia)

Se mencionaron opciones gratuitas para practicar sin depender de una nube de pago:

- Servicios que otorgan una **máquina Linux temporal con IP pública**, accesible únicamente con una cuenta de correo (ej. Gmail), sin necesidad de registrar tarjeta ni crear cuenta en un proveedor cloud.
    - Uso gratuito limitado a algunas horas de sesión; al finalizar, la sesión y sus cambios se destruyen.
- Alternativas de proveedores cloud personales (ej. Digital Ocean) o cualquier VM propia, siempre que tenga acceso a Internet.
- Entornos tipo IDE en la nube que permiten interactuar directamente con el sistema de archivos de una máquina virtual Ubuntu (incluyendo conexión por SSH).

---

# Buenas prácticas y recomendaciones mencionadas

- Se recomienda **no usar código ni información real de clientes** en los laboratorios; usar proyectos propios o de práctica.
- Se recomienda entender y dominar los **comandos de Git** en lugar de depender de plugins gráficos, ya que estos últimos pueden generar errores o comportamientos inesperados al resolver merges.
- Un mismo proyecto (Azure DevOps Project) puede contener **múltiples repositorios** (uno por cada aplicación), sin necesidad de crear un proyecto distinto por cada una.
- El nombre con el que un pipeline clona el repositorio del agente puede personalizarse directamente desde el YAML.
- Se anticipó que más adelante se trabajará con **Helm** (administrador de dependencias/charts de Kubernetes) para el despliegue, momento en el que se necesitará descargar como mínimo dos repositorios: el del proyecto Helm (chart) y el del código fuente de la aplicación.

---

# Ideas Clave de la Sesión

- Se practicó la resolución manual de conflictos de Git en un flujo real de Pull Request, usando exclusivamente comandos.
- El flujo de resolución de conflictos es: sincronizar ramas → merge local → resolver conflicto en el archivo → `add` → `commit` → `push` → completar el PR.
- Se introdujo el ecosistema de **Azure Pipelines**: Personal Access Token, Agent Pools y agentes self-hosted.
- Un agente self-hosted requiere: una máquina con acceso a Internet, la arquitectura correcta del sistema operativo, un PAT válido y el software/runtime necesario correctamente instalado y configurado.
- Se mostró la creación de un pipeline en **modo interactivo (Assistant)**, que traduce automáticamente las acciones a código YAML, como puerta de entrada antes de escribir YAML directamente.
- Un pipeline se materializa como un archivo `azure-pipelines.yml` versionado en el repositorio.
- La siguiente etapa del curso continuará profundizando en el ecosistema de Pipelines (YAML), y más adelante se abordará Docker/Kubernetes/Helm para el despliegue.