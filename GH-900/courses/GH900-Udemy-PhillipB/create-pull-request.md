# Create Pull Requests

## 1. ¿Qué es un Pull Request (PR)?

Un **Pull Request** es una **solicitud formal** para fusionar cambios (que hiciste en un fork o en una rama) hacia el repositorio/rama original. Permite que otros colaboradores **revisen y discutan** los cambios antes de decidir si se confirman en el repositorio original.

## 2. Formas de crear un Pull Request

Hay varias entradas equivalentes en la interfaz de GitHub:

- Botón **"Contribute" → "Open pull request"**
- Botón **"Compare & pull request"** (aparece automáticamente tras un push reciente a una rama/fork)
- Pestaña **"Pull requests" → "New pull request"**

## 3. Terminología clave: Base vs Head

| Término                           | Significado                                                                |
|:----------------------------------|:---------------------------------------------------------------------------|
| **Head repository / head branch** | El repositorio/rama **de donde salen** los cambios (tu fork o tu rama)     |
| **Base repository / base branch** | El repositorio/rama **hacia donde van** los cambios (el original/upstream) |

> **Regla mental:** *"Head" es el origen, "Base" es el destino.*

## 4. Elementos adicionales al crear un PR

| Elemento                             | Qué hace                                                                               |
|:-------------------------------------|:---------------------------------------------------------------------------------------|
| **Adjuntar archivos**                | Vía ícono de clip, o arrastrar/soltar en la parte inferior del cuadro de texto         |
| **Mencionar a alguien (`@usuario`)** | Envía una notificación directa a esa persona                                           |
| **Labels (etiquetas)**               | Clasificar el PR (ej. bug, enhancement)                                                |
| **Assignees**                        | Asignar personas responsables del PR                                                   |
| **Projects**                         | Vincular el PR a un tablero de proyecto                                                |
| **Milestones**                       | Vincular el PR a un hito del proyecto                                                  |
| **Reviewers**                        | Solicitar revisores — **solo disponible si tienes acceso de escritura** al repositorio |

## 5. Estados de un Pull Request
Un PR, en cualquier momento de su vida, está en **uno de estos estados**:

| Estado                      | Ícono/Color típico | ¿Qué significa?                                               | ¿Se puede fusionar (merge)?                   |
|:----------------------------|:-------------------|:--------------------------------------------------------------|:----------------------------------------------|
| **Draft**                   | Gris (lápiz)       | El autor sigue trabajando; no está listo para revisión formal | ❌ No — el botón de merge está bloqueado      |
| **Open** (Ready for review) | Verde              | Listo, esperando revisión y/o aprobación                      | ✅ Sí (una vez aprobado, si el repo lo exige) |
| **Merged**                  | Morado             | Los cambios ya fueron fusionados a la rama base               | Ya se fusionó — estado final                  |
| **Closed** (sin fusionar)   | Rojo               | Se cerró el PR sin aceptar los cambios (se descartó)          | No — pero **puede reabrirse**                 |

## 6. Pull Request vs Draft Pull Request
Un **Draft Pull Request** es un Pull Request normal, con una sola diferencia: tiene una **etiqueta de estado especial** que le dice a GitHub *"todavía no está listo para ser fusionado ni revisado formalmente"*.

| Tipo                    | Comportamiento                                                                 |
|:------------------------|:-------------------------------------------------------------------------------|
| **Pull Request normal** | Puede fusionarse (merge) en cuanto esté aprobado                               |
| **Draft Pull Request**  | **No se puede fusionar** hasta marcarlo explícitamente como "Ready for review" |

**Por qué existe el Draft PR:** te permite abrir el PR y trabajar en él de forma visible (para llevar registro o pedir feedback temprano) sin activar aún el proceso formal de revisión.

> Los **Code Owners** (dueños de código, definidos para revisar ciertos archivos/carpetas obligatoriamente) **NO son notificados automáticamente** mientras el PR esté en estado Draft. Solo se activa esa notificación cuando el PR pasa a estado "Ready for review".

Un PR puede alternar libremente entre ambos estados: de normal a draft, y de draft a normal.

## 7. Qué se puede ver/hacer dentro de un Pull Request ya creado

| Pestaña/Sección   | Contenido                                                                                                                   |
|:------------------|:----------------------------------------------------------------------------------------------------------------------------|
| **Conversation**  | El PR inicial + todos los comentarios de la discusión                                                                       |
| **Commits**       | Los commits que forman parte del PR — **aún no confirmados** en la rama/repositorio upstream                                |
| **Checks**        | Resultados de comprobaciones automatizadas (ej. GitHub Actions)                                                             |
| **Files changed** | Los archivos modificados, con posibilidad de ver, editar o eliminar desde ahí, y de preguntarle a **Copilot** sobre el diff |

### Otras acciones disponibles

- **Subscribe / Unsubscribe:** activar o desactivar notificaciones sobre ese PR específico (mismo concepto de suscripción que vimos en Issues).
- **Abrir en GitHub Desktop.**
- **Close pull request:** cierra el PR sin fusionarlo — **puede reabrirse después** si es necesario (no es una acción destructiva/permanente).


## Resumen visual del flujo completo

```
Fork / Branch con cambios (HEAD)
            │
            │ Contribute → Open pull request
            ▼
   Formulario de PR: título + descripción (Markdown)
            │
            │ Elegir: PR normal  o  Draft PR
            ▼
      Create pull request
            │
            ▼
   Revisión / discusión / checks automatizados
            │
      ┌─────┴──────┐
      ▼             ▼
   Merge          Close
(se fusiona     (se cierra sin
 al repo BASE)   fusionar — reabrible)
```