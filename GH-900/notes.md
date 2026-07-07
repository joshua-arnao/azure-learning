| ÁREA DE DOMINIO GH-900                                                     | PESO |
|:---------------------------------------------------------------------------|:-----|
| Introducción a Git y GitHub                                                | 22%  |
| Trabajo con repositorios de GitHub                                         | 8%   |
| Características de colaboración (Issues, Pull Requests, Discussions, etc.) | 30%  |
| Desarrollo moderno (GitHub Actions, Codespaces, Copilot, DevOps concepts)  | 13%  |
| Gestión de proyectos                                                       | 7%   |
| Privacidad, seguridad y administración                                     | 10%  |
| Beneficios de la comunidad GitHub                                          | 10%  |

---

## PROBLEMÁTICA
Antes de 1986, los programadores trabajaban de forma aislada y si uno editaba un archivo lo 'bloqueaba' para que nadie más lo pueda modificar, lo que hacía imposible el trabajo colaborativo. Para solucionar esto, se creó  **CVS(Concurrente versions systems)**, que introdujo un servidor centralizado para que todos aplicaran cambios a la vez sin tenet que bloquear los archivos. Como CVS generaba errores al subir archivos y rompia el código, se creó **SVN(Subversion)** para solucionarlo. Sin embargo, este modelo seguía siendo muy lento y dependiente de internet, por lo que finalmente se creó Git (un tipo de **VCS(Version Control System)** distribuido) para poder trabajar de forma rápida y sin depender de un servidor central.

### LA EVOLUCIÓN DEL TRABAJO COLABORATIVO

1. CVS (Concurrent Versions System / Sistema de Versiones Concurrentes): 
   - Fue el pionero en crear un servidor **centralizado** donde todos los programadores enviaban sus cambios
   - Acabó con el problema de "bloquear archivos". Antes de CVS, si tú editabas un archivo, nadie más podía tocarlo. CVS permitió que varios programadores modificaran el mismo archivo a la vez y el sistema juntaba los cambios automáticamente.

2. SVN (Subversion):
   - CVS tenía fallos graves. Si subías cambios en 10 archivos y el internet fallaba en el archivo número 5, el servidor guardaba la mitad del código roto (no tenía **"cambios atómicos"**). Tampoco permitía cambiar el nombre de las carpetas sin romper el historial.
   -  SVN mantuvo la idea del servidor centralizado pero corrigió todos los errores de CVS, permitiendo cambiar nombres de carpetas y asegurando que los cambios se subieran completos o no se subieran nada.

3. VCS (VERSION CONTROL SYSTEM)
   - El modelo de servidor central (de CVS y SVN) se volvió muy lento a medida que los proyectos crecían. Además, si el servidor central se caía o no tenías internet, los programadores no podían trabajar ni ver el historial del proyecto.
   -  Eliminó la dependencia de un servidor central. Con Git, cada programador tiene una copia exacta y completa de todo el proyecto y su historial en su propia computadora.

Para el trabajo colaborativo en desarrollo de software, es necesario combinar un proceso **centralizado** y **distribuido** para garantizar la autonomía individual sin perder la coordinación del equipo.

#### CENTRALIZADO (CENTRALIZED VCS — CVCS):
- Solo el servidor tiene el historial completo.
- Tu computadora solo tiene la "foto actual" de los archivos, no el historial.
- Consecuencia: si el servidor se cae, no puedes ver versiones anteriores, no puedes comparar cambios, no puedes hacer commit — estás completamente bloqueado.

#### DISTRIBUIDO (DISTRIBUTED VCS — DVCS), COMO GIT:
- Cuando se hace `git clone`, no copias solo los archivos actuales, copias todo el repositorio `.git`, con todo su historial completo, todas las ramas, todos los commits.
- Consecuencia práctica: cada copia es, en sí misma, un backup completo del proyecto. Puedes seguir trabajando, hacer commits, crear ramas, revisar historial, todo sin internet, porque no dependes del servidor para nada de eso.
- Solo necesitas conexión para sincronizar con otros (git push / git pull), no para trabajar.

> "Distribuido" no significa que no exista un servidor remoto (GitHub sigue funcionando como punto **central** de sincronización), significa que el **historial no depende de él**. El servidor remoto es una copia más entre iguales (peers), no la única fuente de verdad.


## ¿QUÉ ES EL CONTROL DE VERSIONES?

Un sistema de control de versiones (VCS) es un programa o un conjunto de programas que realiza el seguimiento de los cambios de una colección de archivos.

El control de versión se describe a menudo como parte de la adminsitración de configuración de Software (SCM).

Con un VCS, puede:

- Ver todos los cambios realizados en un proyecto, **cuando** se hicieron los cambios y **quién** los efectuó.
- Incluir un mensaje con cada cambio para explicar los motivos.
- Recuperar versiones anteriores del proyecto completo o archivos individuales.
- Crear *ramas*, donde los cambios se pueden hacer experimentalmente. Esta característica permite que se trabaje en
  varios conjuntos de cambios diferentes al mismo tiempo, posiblemente por difernetes personas , sin que ello afecte a
  la rama principal. Y más adelante se pueden fusionar los cambios que deses conservar en la rama princiapal.
- Adjuntar una etiqueta de versión, por ejemplo, para marcar una nueva versión.

> Git es un VSC de código abierto

## CONTROL DE VERSIONES DISTRIBUIDO
Git se almacena el historial completo en tu ordenador local, y también en un servidor. Se pueden editar archivos sin conexión de red, confirmalos localmente y sincronizarlos con el servidor cuando una conexión este disponible

## TERMINILOGÍA DE GIT

- **Árbol de trabajo**: Conjunto de directorios y archivos anidados.
- **Repositorio**: Almacén de datos, contenido en un directorio oculto `.git` aquí se almacena el historial y los metadatos de un proyecto.
- **Hash**: Número generado por una función hash que representa el contenido de un archivo u **objeto**. UNa ventaja de usar códigos hash es que Git puede indicar si un archivo a cambiado aplicado un algoritmo al contenido y comparando el resultado.
- **Objeto**: Un repositorio de Git puede contener 4 tipos de objetos, cada uno identificado de forma única por un hash:
  - Blob - contiene un archivo normal
  - Árbol / Tree - representa un directorio contiene
    - nombres
    - valores
    - hash
    - permisos
  - Confirmación / Commit - versión especifica del árbol
  - Etiqueta / Tag - almacena metadatos como:
    - nombre
    - mensaje
    - firma (opcional)
- **Confirmación**: Cuando se usa como verbo *confirma* significa crear un **objeto de confirmación**. Confirma los cambios realizados para que otros usuarios puedan verlos
- **Rama / Branch**: Una rama es una serie nombrada de commits enlazados. El nivel superior de una rama se denomina `HEAD`.
- **Remote**: Es una referencia a otro repositorio Git. Al clonar crea un remoto denominado `origin` que apunta al repositorio clonado
- **Comandos, subcomandos y opciones**: las operaciones de Git se realizan mediante comandos como git push y git pull. git es el comando, mientras que push o pull es el subcomando.

## FUNCIONAMIENTO DE GIT

### LOS 3 ESTADOS DE UN ARCHIVO GIT
Git necesita saber, en todo momento, en que "fase" de confirmación esta cada archivo, para no confirmar(commit) cosas que no quería y para permitirte revisar los cambios antes de guardarlos permanentemente.

| Estado                 | Significado                                                                                                    |
|:-----------------------|:---------------------------------------------------------------------------------------------------------------|
| Modificado / Modified  | Cambiar el archivo en el árbol de trabajo(working tree), pero Git todavia no lo vigila para el próximo commit. |
| Preparado / Staged     | Marcaste el cambio con `git add`para el siguiente commit.                                                      |
| Confirmado / Committed | El cambio ya queda guardado en el repositorio local `.git`.                                                    |



### LAS 3 ÁREAS DE GIT
Estas 3 zonas son literalmente los "lugares físicos" donde viven los archivos según su estado:

| Zona                               | Qué contiene                                                                          |
|:-----------------------------------|:--------------------------------------------------------------------------------------|
| Área de trabajo / Working Area     | Los archivos tal cual los ves y editas en tu carpeta del proyecto.                    |
| Área de preparación / Staging Area | Una "sala de espera" antes del commit. Aquí llegan los archivos cuando haces `git add` |
| Repositorio / Repository           |  El historial permanente. Aquí llegan los archivos cuando haces `git commit` |

#### FLUJO COMPLETO:

```markdown
------------------                  ----------------                   -------------
|Working Directory|  --(git add)--> | Staging Area | --(git commit)--> | Repository |
|   (Modified)    |                 |   (Staged)   |                   | (Committed)|
-------------------                 ----------------                   --------------
```

U: Untracked - Sin seguimiento
A: Stage Area

