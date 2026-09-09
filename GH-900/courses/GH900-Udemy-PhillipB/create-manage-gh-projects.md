# Create and Manage GitHub Projects, and add Issues and PRs

## ¿Qué es un GitHub Project?
Una herramienta para planificar y hacer seguimiento de Issues, Pull
Requests y otros elementos de trabajo, dentro del propio GitHub (sin
depender de un Jira/Trello externo).

> Si no ves la pestaña "Projects" en tu repo: Settings del repositorio
> → scroll abajo → activar "Projects".

## Tipos de vista al crear un proyecto
| Vista| Qué es |
|:------|:-------------|
| **Table**| Como una hoja de cálculo — filas y columnas |
| **Board** | Kanban — columnas por estado, tarjetas movibles |
| **Roadmap** | Elementos con fecha de inicio y fecha objetivo (timeline) |

## Plantillas disponibles al crear
- Team planning
- Feature release (lanzamiento futuro)
- Kanban
- Bug tracker (seguimiento de errores)
- Iterative development (desarrollo iterativo)
- Product launch roadmap
- Team retrospective

## Crear un proyecto — pasos
1. Pestaña **Projects** → **New Project**
2. Elegir vista/plantilla (ej. Table)
3. Click **Create project**
4. Renombrar: click en el ícono de lápiz junto al título

## Gestión de vistas
- Un proyecto puede tener MÚLTIPLES vistas (botón "New view")
- Se puede duplicar una vista existente como base para otra

## Dónde encontrar tus proyectos
- Ícono de hamburguesa → "Projects" → lista de TODOS los proyectos
  (de todos los repos), filtrable por "vistos recientemente" o"creados por mí"
- Click en el `...`  junto a un proyecto:
    - Desde "vistos recientemente" → quitar de la lista
    - Desde la pestaña Projects de un repo → eliminar el proyecto
    - También permite **duplicar** el proyecto

## Agregar elementos a un proyecto
**Opción A — Crear un issue nuevo directo desde el proyecto:**
- Click en el signo `+` → título + descripción
- Se crea en el repo asociado al proyecto por defecto, pero se puede elegir otro repo, plantilla/formulario, asignado, milestone

**Opción B — Agregar issues/PRs ya existentes:**
- Click en `+` → "Add items from repository"
- Selección múltiple, con buscador (funciona entre varios repos)
- Solo muestra por defecto los más recientes que NO están ya en el
  proyecto — hay que buscar para ver más

## Organizar elementos dentro del proyecto
- **Reordenar**: arrastrar filas arriba/abajo, o usar la flecha al
  pasar el mouse por el margen izquierdo → mover antes/después de un
  elemento específico, o a una posición exacta
- **Filtrar por palabra clave**: busca coincidencias en título/descripción
- **Archivar**: saca el elemento de la lista activa (no lo borra)
- Ver archivados: `...` → "Archived items" → opción de restaurar o eliminar
- **Eliminar**: borra el elemento del proyecto directamente

## Campos editables por elemento
- **Assignees** (asignados)
- **Status** (por defecto 3 estados):

  | Estado | Significado |
  |:---|:---|
  | Todo | No iniciado |
  | In Progress | Trabajándose activamente |
  | Done | Terminado |

- Campos adicionales que se pueden agregar (botón `+`):
    - Labels visibles
    - Links a Pull Requests
    - Milestones
    - Repository
    - Si es un sub-issue: issue padre y progreso de sub-issues

## Resumen
GitHub Projects = tablero de seguimiento nativo de GitHub (Table/Board/
Roadmap) donde se agrupan Issues y PRs de uno o varios repos, con
estados, asignados y vistas personalizables, sin salir de la plataforma.
