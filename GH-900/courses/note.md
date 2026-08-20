# GH-900 - GITHUB FOUNDATIONS
## UNDERSTAND THE BASICS OF GIT

---

### 1. ¿QUÉ ES GIT?

Git es un **Sistema de Control de Versiones Distribuido (DVCS — Distributed Version Control System)**.

**La idea central:** en un sistema distribuido, los usuarios **no necesitan estar conectados a una versión centralizada** para trabajar. Puedes tener una versión centralizada (como GitHub.com), pero **Git en sí mismo no lo requiere** — podrías usar Git únicamente en tu computadora, sin ningún servidor remoto de por medio.

| Escenario | ¿Dónde vive la copia? |
|---|---|
| Solo en tu computadora | Local, únicamente en tu disco |
| Usando GitHub | En la nube (remoto) **y** en tu computadora (local) |

En ambos casos, **cada persona tiene su propia copia completa** — esa es la esencia de "distribuido".

---

### 2. ¿QUÉ HACE GIT? (FUNCIONES CLAVES)

| Función | Detalle |
|---|---|
| **Rastrea el historial de archivos** | Registra **quién** hizo cada cambio y **por qué** (a través de mensajes de commit) y **cuándo** se hicieron. |
| **Permite comentarios en cambios e issues** | Puedes documentar el motivo de cada modificación. |
| **Soporta múltiples interfaces** | Se puede usar por línea de comandos (CLI) o mediante una interfaz gráfica (GUI), como una app o el navegador. |
| **Habilita colaboración a gran escala** | Permite que varias personas trabajen en el mismo proyecto — no solo en un mismo edificio o ciudad, sino a **escala internacional**. |
| **Restaura versiones anteriores** | Puedes volver a cualquier versión pasada de un archivo o del proyecto completo cuando lo necesites. |
| **Flexibilidad centralizada/local** | Los usuarios pueden elegir trabajar desde una versión centralizada (remota) o desde su propia copia local, y luego extraer o fusionar cambios entre ambas. |

---

### 3. ¿QUÉ ES UN REPOSITORIO?

Un repositorio contiene:
- **Todos los archivos y carpetas** del proyecto (similar a lo que verías en el Explorador de Windows o el Finder de Mac).
- **El historial de revisiones completo** de cada archivo — no solo el estado actual, sino todas las versiones anteriores.



> **Punto clave: los archivos NO se guardan automáticamente** 
> "No es el caso que empiezo a escribir y cada vez que escribo se guarda automáticamente. No, tengo que guardarlo o comprometerlo (commit)."

Un **commit** representa una instantánea (*snapshot*) de cómo estaba el contenido de un archivo **en un momento determinado** — es una acción explícita, no automática.

#### QUÉ PUEDES HACER CON EL HISTORIAL DE UN REPOSITORIO

- Ver la versión **actual** de un archivo.
- Ver **todas las versiones anteriores** (el ejemplo del video: un archivo con 4 versiones distintas, cada una ligada a un commit).
- Comparar cómo era el repositorio completo **en un punto específico del tiempo** (ej. al final del primer commit había 2 archivos; en el último commit, 3 archivos + 1 carpeta; en la versión actual, 4 archivos).
- Revisar código — tanto tú como otras personas pueden dejar comentarios sobre los cambios.

---

## 4. Repositorios Locales vs Remotos

| Tipo | Dónde vive | Requiere internet | Quién accede |
|---|---|---|---|
| **Remoto** | Almacenado de forma centralizada (ej. GitHub o servidores similares) | ✅ Sí — necesitas conexión para acceder | Varias personas, según los permisos que tengan |
| **Local** | En tu propia computadora | ❌ No — puedes trabajar sin red | Generalmente solo tú (a menos que alguien más tenga acceso a tu equipo) |

### Cómo se relacionan ambos

- Puedes crear un repositorio **local** clonando uno **remoto** (`git clone`).
- Puedes enviar (*push*) los cambios de tu repositorio local hacia el remoto.
- Tu repositorio local incluye **tus propios commits y tu historial local** — es una copia funcional completa, no un simple acceso al remoto.

---

## 5. Ramas (Branches)

- Git y GitHub organizan el contenido usando **ramas**, que contienen carpetas y subcarpetas — es decir, cada rama puede tener su propia versión completa del proyecto.
- La rama original/por defecto se llama:
    - **`main`** en GitHub
    - **`master`** en Git (el nombre técnico original)
    - Ambos plataformas usaban "master" anteriormente, pero **GitHub cambió el nombre por defecto a `main` en 2020**.

**Dato importante:** cuando navegas a una versión anterior del historial, técnicamente estás viendo una **rama generada automáticamente** por el sistema para representar ese punto en el tiempo — y tú también puedes crear tus propias ramas manualmente.

---

## 6. Repositorios: Públicos vs Privados

Los repositorios pueden ser:
- **Públicos** — visibles para cualquiera.
- **Privados** — con acceso restringido.

---

## 7. Operaciones Clave sobre Repositorios

| Operación | Qué hace |
|---|---|
| **Clonar (Clone)** | Duplica un repositorio completo para desarrollo independiente, **sin afectar** la rama principal/master. |
| **Confirmar (Commit)** | Guarda archivos dentro de un repositorio como una instantánea con mensaje. |
| **Fusionar (Merge)** | Incorpora cambios de una rama hacia otra rama del mismo repositorio. |
| **Comparar (Compare)** | Permite comparar diferentes versiones de código entre archivos. |

---

## 8. Flujo de Trabajo Básico de Git (Basic Git Workflow)

### Paso 1 — Trabajar en la rama principal (poco recomendado directamente)

En la rama principal/master, puedes añadir archivos y confirmarlos (*commit*). Al confirmar, los cambios se añaden a un **índice (index)** que contiene una instantánea del **árbol de trabajo (working tree)** — estos dos términos (*índice* / *árbol de trabajo*) describen el directorio de contenido en el momento de un commit específico.

> **Por qué normalmente NO se trabaja directo en la rama principal:** si esa rama representa el entorno de **producción** (el código que usa todo el mundo en vivo) y haces un cambio que rompe algo, **todo el sistema deja de funcionar** para los usuarios reales.

### Paso 2 — Crear una rama de trabajo

La solución es crear una **rama separada** donde puedas hacer cambios **sin afectar** la rama principal. Idealmente:

> "Lo ideal sería tener una rama separada para cada problema que vas a resolver."

Dentro de tu propia rama puedes:
- Crear archivos nuevos
- Editar archivos existentes
- Renombrar archivos
- Mover archivos a otra ubicación/carpeta
- Borrar archivos

Todo esto **solo afecta a la nueva rama** — la rama principal permanece intacta mientras trabajas.

### Paso 3 — Fusionar los cambios de vuelta (Merge)

Una vez satisfecho con los cambios, se **fusionan (merge)** de vuelta a la rama principal, usualmente acompañados de un mensaje describiendo qué problema se resolvió (ej. "Fix: solución para X problema").

**Punto importante sobre merge:**
> "Ahora sólo fusionará los cambios que haya realizado. No se fusionan otros archivos, por ejemplo, ya que otros pueden haberlos modificado."

Esto significa que el merge es **selectivo y seguro** — Git mantiene un registro de todos los cambios para que la rama principal siempre tenga la última versión correcta, sin sobreescribir trabajo de otros colaboradores.

### Paso 4 — Eliminar la rama (opcional)

Una vez que los cambios ya están fusionados en la rama principal y ya no necesitas la rama de trabajo, **puedes eliminarla** — cumplió su propósito.

---

## 9. Trabajando con un Repositorio Remoto/Centralizado

Cuando el repositorio centralizado vive en GitHub (o en otro servidor), el flujo se amplía:

```
1. Crear una rama (local o en GitHub)
2. Hacer los cambios necesarios
3. Enviar (push) los cambios al repositorio remoto
```

### El caso especial: Pull Request

> "Este tipo de empuje (push) podría implicar la aprobación en lugar de ser un empujón directo. Esto se denomina Pull Request."

**Cuándo aplica:** cuando el repositorio **no es tuyo** (no tienes permisos de escritura directa), en lugar de hacer push directo, propones tus cambios y pides que sean **revisados y aprobados** antes de integrarse — eso es exactamente un **Pull Request (PR)**.

### Manteniendo tu rama actualizada (Pull)

**El problema:** editaste tu rama localmente, pero mientras tanto, alguien más ya subió un archivo nuevo al repositorio remoto — tu rama **quedó desactualizada**.

**La solución:** puedes **traer (pull)** los últimos cambios de la versión centralizada hacia tu propia rama, actualizándola. Después de eso puedes:
- Seguir haciendo cambios adicionales y hacer push nuevamente, o
- Si se requiere revisión, hacer un Pull Request.

---

## 10. Resumen Visual del Flujo Completo

```
Repositorio Remoto (GitHub)
        │
        │ (clone)
        ▼
Repositorio Local ── rama main/master (producción — no editar directo)
        │
        │ (crear rama nueva)
        ▼
   Rama de trabajo ── crear/editar/renombrar/mover/borrar archivos
        │
        │ (commit — guarda snapshot con mensaje)
        ▼
   Cambios confirmados en la rama de trabajo
        │
        │ (merge de vuelta a main, o push + Pull Request si es remoto/compartido)
        ▼
Rama principal actualizada ── rama de trabajo eliminada (opcional)
```

**Si el remoto avanzó mientras trabajabas:**
```
git pull → trae los cambios del remoto a tu rama local → sigues trabajando → push / Pull Request
```

---

## Glosario rápido de esta sección

| Término | Significado |
|---|---|
| **DVCS** | Distributed Version Control System — sistema de control de versiones distribuido, como Git. |
| **Commit** | Acción explícita de guardar una instantánea (snapshot) del contenido en un momento dado, con un mensaje. |
| **Index / Working Tree** | El directorio de contenido tal como existía en el momento de un commit específico. |
| **Branch (rama)** | Línea de desarrollo independiente que permite trabajar sin afectar la rama principal. |
| **Main / Master** | Nombre de la rama por defecto/original (main en GitHub desde 2020, master en Git tradicionalmente). |
| **Merge** | Incorporar cambios de una rama a otra. |
| **Clone** | Crear una copia local completa de un repositorio remoto. |
| **Push** | Enviar tus commits locales al repositorio remoto. |
| **Pull** | Traer los últimos cambios del repositorio remoto hacia tu copia local. |
| **Pull Request (PR)** | Solicitud formal de fusionar cambios, sujeta a revisión y aprobación — usada cuando no tienes permisos de escritura directa. |


### Use Repository Templates

---

#### 1. ¿Qué es un Repository Template?

**El problema que resuelve:** normalmente, al crear un repositorio se empieza desde cero. Pero si quieres que **todos tus proyectos nuevos** partan con una estructura de archivos determinada, por ejemplo, un `CODE_OF_CONDUCT.md`, guías de contribución, una estructura de carpetas específica, repetir eso manualmente cada vez es ineficiente y propenso a inconsistencias.

**La solución:** convertir un repositorio existente en una **plantilla (template)**. Cualquier repositorio nuevo creado "a partir de" esa plantilla **hereda automáticamente** su estructura de archivos y carpetas — sin tener que copiar y pegar nada manualmente.

#### 2. Cómo habilitar un repositorio como plantilla

| Paso | Acción                                                                  |
|:-----|:------------------------------------------------------------------------|
| 1    | Se requieren **permisos de administrador** sobre el repositorio.        |
| 2    | Ir a **Settings** del repositorio.                                      |
| 3    | En la pestaña **General**, marcar la casilla **"Template repository"**. |

**Dato clave:** esta opción **no está activada por defecto**, sin haberla marcado antes, el botón "Use this template" simplemente no existe/no aparece en el repositorio.

#### 3. Cómo crear un nuevo repositorio a partir de una plantilla

Una vez habilitada la opción de plantilla:

1. En el repositorio (ya convertido en plantilla), aparece el botón **"Use this template"**.
2. Clic en **"Create a new repository"**.
3. Configurar el nuevo repositorio:

| Opción                   | Detalle                                                                                         |
|:-------------------------|:------------------------------------------------------------------------------------------------|
| **Nombre**               | Nombre del nuevo repositorio.                                                                   |
| **Include all branches** | Puedes elegir traer **todas las ramas** de la plantilla, no solo la rama principal por defecto. |
| **Descripción**          | Opcional.                                                                                       |
| **Visibilidad**          | Público o Privado.                                                                              |

4. Clic en **"Create repository"** — GitHub genera el nuevo repo con la estructura heredada (ej. el mismo `README.md` y contenido inicial de la plantilla).

##### 4. Qué SÍ y qué NO se copia desde la plantilla

| Se copia                                 | No se copia                                              |
|:-----------------------------------------|:---------------------------------------------------------|
| Archivos y carpetas del repositorio      | **Archivos almacenados en Git LFS** (Large File Storage) |
| Estructura general del proyecto          | —                                                        |
| Todas las ramas (si se marca esa opción) | —                                                        |

**Sobre Git LFS (Large File Storage):** es un almacén especial para archivos pesados, típicamente **muestras de audio, video, datasets y gráficos**. Al crear un repositorio desde una plantilla, **estos archivos NO se incluyen**, es una excepción importante a tener en cuenta si tu plantilla dependía de recursos grandes almacenados ahí.

#### 5. Diferencia clave: Template vs Clone vs Fork

Usar una plantilla **NO es lo mismo** que clonar o hacer fork:

| Acción                | ¿Qué genera?                                                                                                | ¿Mantiene conexión/historial con el original?                                        |
|:----------------------|:------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------|
| **Use this template** | Un repositorio **completamente nuevo e independiente**, con la estructura de archivos como punto de partida | ❌ No, empieza con un historial de commits limpio, sin relación con el repo original |
| **Fork**              | Una copia vinculada al repositorio original                                                                 | ✅ Sí, mantiene relación con el "upstream", pensado para contribuir de vuelta        |
| **Clone**             | Una copia local de un repositorio existente                                                                 | ✅ Sí — mismo historial completo, mismo remoto                                       |

**Por qué esto importa:** una plantilla es para **empezar proyectos nuevos con una base estandarizada**, no para colaborar en un proyecto compartido ni para mantener sincronización con el original.

## NAVIGATE GITHUB AND MANAGE REPOSITORY SETTINGS

## WORK WITH FILES IN A REPOSITORY

## COLLABORATE USING GITHUB

## IMPLEMENT DEVOPS PRACTICES

## USE GITHUB FOR CODE REVIEW

## MANAGE PROJECTS WITH GITHUB

## ENSURE REPOSITORY SECURITY

## ADMINISTRE GITHUB ORGANIZATIONS

## ENGAGE WITH THE GITHUB COMMUNITY

## WORK WITH GIT COMMANDS



