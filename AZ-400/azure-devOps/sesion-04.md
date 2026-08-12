# Azure DevOps - Sesión 04

---

## 1. Repaso: Agent Pools y agente personalizado

Se retomaron dudas de la sesión anterior sobre los tipos de grupos de agentes disponibles al crear un pipeline:

- **Azure Pipelines (pool por defecto de Microsoft):** agente gratuito compartido.
    - La primera vez que se usa, requiere completar un formulario de activación de la capa gratuita (demora aproximada de 2 a 3 días en ser aprobado).
    - Ventaja: no requiere infraestructura propia.
    - Desventaja: se compite por una **cola regional compartida**, por lo que solo se ejecuta un job a la vez y los tiempos de espera pueden variar (5, 10 minutos o más).
- **GitHub-hosted:** alternativa que Microsoft habilitó tras adquirir GitHub.
- **Agente propio (self-hosted):** el que se configuró en la sesión anterior. No tiene límite de ejecuciones concurrentes más allá de la cantidad de agentes que se registren.

### Dimensionamiento de recursos del agente

Se mostró como ejemplo una máquina con **4 CPU y 16 GB de RAM**, catalogada como más que suficiente para un agente individual. Se explicó que, en un escenario real:

- Los commits de Integración Continua (CI) no ocurren constantemente; normalmente se concentran a mediodía o al final del día.
- Los despliegues (deploys) suelen programarse en horarios de baja concurrencia (de noche), donde alcanza con 1-2 agentes activos.
- Con hardware modesto es posible simular varios agentes en paralelo usando **contenedores Docker** (se mencionó un rango de 5 a 10 contenedores como agentes para un proyecto real, siendo suficiente incluso con 5).

---

## 2. Tareas (Tasks) en modo interactivo

Se continuó explorando el catálogo de tareas del **modo interactivo** (Assistant) del editor de pipelines, usando como ejemplo un pipeline "vacío" para practicar libremente.

### 2.1 Command Line — herramienta de depuración

Se destacó como una de las tareas más útiles para depurar, ya que Azure Pipelines no ofrece un modo "debug" interactivo tradicional. Se recomienda usar comandos simples (`ls`, `pwd`, etc.) para:

- Confirmar la ruta de trabajo actual del agente.
- Verificar que un archivo o carpeta se generó correctamente.

### 2.2 Variables predefinidas del sistema

Cada ejecución de un pipeline expone variables predefinidas (ej. identificador de build, directorio binario, directorio de trabajo). Puntos clave:

- Las variables de sistema (o "de pipeline") siguen un formato reconocible por defecto y cambian en cada ejecución (ej. un número de build incremental).
- Es posible consultar el listado completo de variables predefinidas de Azure DevOps buscando en la documentación oficial.
- También se pueden **crear variables propias**, tanto a nivel de pipeline como a nivel de grupo de variables, y marcarlas como "secretas" (ocultas) si se requiere.
- **Recomendación:** trabajar directamente con los valores que ofrecen las variables predefinidas (ej. "directorio de salida", "directorio actual") en lugar de intentar interpretar o depender de identificadores internos (hashes) que la herramienta genera automáticamente para carpetas temporales, ya que no son estables ni predecibles.

### 2.3 Tarea Archive (compresión de archivos)

Se usó como ejemplo para explicar el patrón general de configuración de cualquier tarea:

- Se puede definir la ruta a comprimir, el formato de compresión (Zip, 7-Zip, etc.) y el nombre del archivo de salida.
- Cada tarea tiene un botón de **ayuda contextual** que muestra ejemplos y explica cada parámetro.
- Cada tarea puede tener **distintas versiones** (ej. versión 1 y versión 2), que a veces cambian la forma de invocar el programa o los parámetros disponibles; se recomienda revisar cuál versión conviene según el caso de uso.
- Cada tarea cuenta con un enlace **"About this task"** que lleva a la documentación oficial de Microsoft.

### 2.4 Carpetas de trabajo temporales del agente

Se explicó que cada ejecución de un pipeline genera una carpeta de trabajo identificada con un hash o número temporal (no es un snapshot ni un tag). Estas carpetas:

- Se acumulan por defecto tras cada ejecución, a menos que se configure explícitamente la limpieza automática (opción de tipo "clean").
- Al activar dicha opción, el agente elimina el contenido previo antes de cada nueva ejecución, en lugar de solo hacer un checkout sobre lo existente.

---

## 3. Triggers (Disparadores de ejecución)

### 3.1 Habilitar Integración Continua

Para que un pipeline se ejecute automáticamente ante cambios en el repositorio, debe activarse la opción **"Enable continuous integration"**.

### 3.2 Branch filters (patrones de rama)

- Se debe definir un patrón de nombre de rama que disparará el pipeline (ej. `feature*` para todas las ramas que comiencen con "feature").
- El símbolo `*` funciona como comodín.
- Es una práctica común asociar el CI a ramas de feature (y opcionalmente también a `main`), según la política de cada equipo/empresa.
- También es posible **excluir** ramas específicas dentro de la configuración de triggers.

### 3.3 Tipos de disparadores

Existen dos formas principales de disparar un pipeline:

1. **Por commit (Continuous Integration):** el pipeline se ejecuta automáticamente cada vez que se sube un cambio a una rama que cumple el patrón definido.
2. **Programado (Scheduled):** el pipeline se ejecuta en un horario definido (ej. de lunes a viernes a las 7:00 a.m.), útil para equipos que prefieren no ejecutar el pipeline en cada commit sino de forma periódica (por ejemplo, antes del inicio de la jornada laboral).

> Ambas configuraciones no son excluyentes; la elección depende de la política de cada equipo o cliente.

---

## 4. Opciones adicionales del pipeline

### 4.1 Formato del número de Build

En la sección **Options** es posible personalizar el formato con el que se identifica cada ejecución (build), por ejemplo usando variables predefinidas para mostrar fecha, hora, u otro identificador en lugar del número de build por defecto. Esto solo cambia la presentación/etiqueta del build, no su ID interno.

### 4.2 Política de cola y tiempo de vida útil

- Se puede configurar si el pipeline debe esperar en cola cuando no hay agentes disponibles, o pausarse/deshabilitarse.
- Se puede definir un **tiempo máximo de ejecución** (timeout), ya que cada ejecución de pipeline tiene un tiempo de vida útil configurable.

### 4.3 Historial de cambios

La sección de historial permite comparar configuraciones entre versiones del pipeline (auditoría de qué cambió y cuándo).

---

## 5. Modo YAML (no interactivo)

Tras dominar el modo interactivo, se introdujo la edición directa del archivo YAML como el método de trabajo real y recomendado.

### 5.1 Sintaxis básica

- La estructura fundamental es `steps` y dentro de cada step, un `script` (o una `task` con sus parámetros).
- El formato YAML es de tipo **clave-valor**, y es sensible a la indentación (espacios); cada nivel de jerarquía debe respetarse cuidadosamente.
- El editor cuenta con ayuda contextual: al escribir `task:` y un espacio, se despliegan sugerencias de tareas disponibles.
- Existe un botón de **validación** que detecta errores de sintaxis, aunque no siempre señala la línea exacta del error (se mencionó un caso donde el error reportado en una línea correspondía en realidad a otra).

### 5.2 Recomendación para principiantes

Practicar con cambios pequeños e ir validando progresivamente, documentando qué se modificó, para poder identificar la causa si el pipeline falla en tiempo de ejecución (aunque sea sintácticamente válido).

### 5.3 Vinculación de un YAML ya existente en el repositorio

Cuando un repositorio ya cuenta con un archivo `azure-pipelines.yml` (u otro nombre) versionado, al crear un nuevo pipeline se debe seleccionar la opción de **"Azure Pipelines YAML file"** (no la opción de plantilla/asistente), elegir la rama y el archivo YAML correspondiente, y el pipeline queda enlazado a ese archivo.

---

## 6. Organización de pipelines en proyectos reales

### 6.1 Carpeta `devops` en el código fuente

Se explicó el estándar habitual en proyectos reales: crear una carpeta (comúnmente nombrada como el repositorio) que contiene los distintos archivos YAML según el ambiente, por ejemplo:

```text
devops/
 ├── ci.yml
 ├── cd-uat.yml
 ├── cd-produccion.yml
 └── rollback.yml
```

Este patrón reemplaza la necesidad de mantener toda la configuración en un único archivo, permitiendo separar los pipelines por ambiente o propósito (CI, CD a UAT, CD a Producción, Rollback).

### 6.2 Organización de pipelines dentro de Azure DevOps (carpetas lógicas)

Además de la organización a nivel de código fuente, los pipelines creados en Azure DevOps también pueden agruparse en **carpetas lógicas** dentro del portal (ej. una carpeta "Desarrollo"), usando la opción **"Move"**. Esto es independiente de la ubicación del archivo YAML en el repositorio.

> Se aclaró la diferencia: una cosa es dónde vive el archivo YAML dentro del código fuente, y otra distinta es cómo se organiza/visualiza el pipeline dentro del portal de Azure DevOps.

### 6.3 Edición y trazabilidad

Desde el pipeline en el portal, la opción **"Edit"** lleva directamente al código fuente del YAML, incluyendo la rama donde reside.

---

## 7. Caso práctico: primer pipeline real para un proyecto Java/Spring Boot

Se inició la construcción de un pipeline real partiendo de un proyecto Spring Boot (Java 21) generado desde Spring Initializr, como preparación para las siguientes sesiones donde se abordará: compilar, generar Dockerfile, subir la imagen a un Azure Container Registry (ACR) y desplegar en Kubernetes usando Helm.

### 7.1 Pasos realizados

1. Se creó el proyecto Java/Spring Boot y se subió al repositorio con los comandos estándar de Git (`init`, `add`, `commit`, `push origin main`).
2. Se creó un nuevo pipeline desde cero, primero explorando la plantilla sugerida automáticamente por Azure DevOps (Maven).
3. Se identificó dónde se configura la **versión de Java** del build (parámetro dentro de la tarea de Maven), ajustándola a la versión usada por el proyecto (Java 21).
4. Se movió el pipeline a la carpeta lógica "Desarrollo" dentro del portal.

### 7.2 Problema real encontrado: configuración de JAVA_HOME en el agente

Al ejecutar el pipeline en el agente self-hosted, la tarea de Maven falló indicando que no se había especificado la versión de Java instalada en el entorno (variable `JAVA_HOME` no configurada correctamente para el proceso).

**Resolución aplicada:**
- Se verificó la versión de Java instalada en el agente con `java -version`.
- Se editó el archivo de perfil del sistema (`/etc/profile`) para exportar correctamente la variable de entorno, por ejemplo:
  ```bash
  export JAVA_HOME=/ruta/a/java21
  ```
- Se identificó que el error hacía referencia a una variable específica distinta a la que inicialmente se había configurado, por lo que fue necesario ajustar el nombre exacto de la variable esperada por el proceso.
- Tras corregir la variable de entorno, el pipeline reconoció Java correctamente y completó la compilación con éxito.

**Lección clave:** no basta con tener el software instalado en la máquina del agente — debe estar correctamente configurado a nivel de variables de entorno del sistema, y a veces requiere reiniciar el shell/sesión (o releer el perfil, ej. `source /etc/profile`) para que los cambios tomen efecto sin reiniciar toda la máquina.

---

## 8. Cierre y próximos pasos del curso

- Próxima etapa: generar el **Dockerfile**, subir la imagen a un **Azure Container Registry (ACR)** y desplegar en **Kubernetes** usando **Helm**.
- Se aclaró la diferencia entre ACR (Azure) y otros registries como el de Amazon (ECR) — cada nube tiene su propio servicio de registro de contenedores.
- Se confirmó el cronograma del curso: quedan pocas clases antes del **examen teórico** y el **trabajo práctico entregable**.
    - El entregable consistirá en un repositorio con su respectivo archivo YAML de pipeline, el cual será ejecutado por el profesor para su evaluación.

---

## Ideas Clave de la Sesión

- Se profundizó en el uso de **Agent Pools**: pool por defecto (compartido, con cola), GitHub-hosted, y agente propio (sin límite de concurrencia según cantidad de agentes registrados).
- Se exploró el catálogo de tareas en modo interactivo, con énfasis en **Command Line** (para depuración) y **Archive** (compresión), destacando el uso de variables predefinidas del sistema.
- Se explicaron los **triggers**: por commit (CI) y programados (scheduled), junto con el uso de patrones de rama (`feature*`).
- Se introdujo el trabajo directo en **YAML**, remarcando la importancia de la indentación y el uso de la ayuda contextual del editor.
- Se explicó el estándar de organización de pipelines en proyectos reales: carpeta `devops` con archivos YAML separados por ambiente (CI, CD UAT, CD Producción), y organización adicional en carpetas lógicas dentro del portal de Azure DevOps.
- Se construyó el primer pipeline real sobre un proyecto Java/Spring Boot, incluyendo la resolución de un problema práctico de configuración de `JAVA_HOME` en el agente self-hosted.
- El curso avanza hacia Docker, Azure Container Registry, Kubernetes y Helm en las próximas sesiones, previo al examen y trabajo final.