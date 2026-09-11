# Privacy, Security, and Administration — Manage Teams

## 1. ¿Qué es un Team?

Un **Team** es una forma de **organizar miembros** dentro de una organización, usada para:
- **Gestionar acceso** a repositorios de forma agrupada (en vez de persona por persona)
- **Enviar notificaciones** a un grupo completo

## 2. Crear un Team — opciones al configurarlo

**Ruta:** Organización → pestaña "Teams" → "New team"

| Campo | Detalle |
|---|---|
| **Team name** | Nombre del equipo |
| **Description** | Descripción |
| **Parent team (equipo padre)** | Opcional — permite anidar el equipo dentro de otro (**nested team**) |
| **Visibility** | Ver sección siguiente |
| **Notificaciones de mención** | Si se activa/desactiva el aviso cuando se menciona `@org/equipo` |

### Equipos anidados (Nested teams)

- Un equipo hijo **puede tener miembros distintos** a los del equipo padre, no hereda automáticamente la membresía.
- **Restricción importante:** un equipo con visibilidad **Secret NO puede ser anidado** dentro de un equipo padre.

---

## 3. Visibilidad de un Team — 2 opciones

| Visibilidad | ¿Quién lo ve? | ¿Recomendada? |
|---|---|---|
| **Visible** | Todos los miembros de la organización pueden verlo y **mencionarlo con `@`** — pero no es visible fuera de la organización | ✅ **Sí, es la recomendada por GitHub** |
| **Secret** | Solo los miembros del propio equipo y los **owners** de la organización pueden verlo | ❌ No recomendada por defecto; además **no puede anidarse** dentro de otro equipo |

## 4. Notificaciones al mencionar al equipo (`@org/equipo`)

Al crear el equipo, puedes definir si se notifica a **todos los miembros** cuando alguien menciona al equipo completo.

> **Detalle importante:** aunque desactives esa notificación grupal general, **los miembros individuales seguirán recibiendo notificaciones si son solicitados específicamente como reviewers**, desactivar la mención grupal no bloquea las notificaciones de revisión personal.

## 5. Gestión desde la página del Team

| Pestaña/Sección | Qué permite |
|---|---|
| **Teams (sub-pestaña)** | Añadir un equipo existente como **equipo hijo** |
| **Repositories** | Añadir o quitar el acceso del equipo a repositorios |
| **Settings** | Cambiar nombre, descripción, equipo padre (mover el equipo), visibilidad, notificaciones, foto de perfil |
| **Danger zone** | Eliminar el equipo |
| **Code review (sección lateral)** | Ver más abajo |
| **Members** | Ver, agregar, quitar miembros; cambiar su rol dentro del equipo |

## 6. Configuración de Code Review a nivel de Team

Una función especialmente útil: **evitar notificar a todo el equipo cuando se solicita revisión tanto al equipo como a miembros individuales**.

**Cómo funciona:**
- Si se activa esta opción, y se solicita revisión al equipo **y también** a miembros individuales del mismo equipo simultáneamente, GitHub **no notifica al equipo completo**, en su lugar, **enruta (routea) automáticamente** la solicitud de revisión hacia miembros específicos del equipo.
- Al activar esta opción, se pueden configurar ajustes adicionales de cómo se distribuye esa asignación.

### Recordatorios programados (Scheduled reminders)

Se pueden configurar **recordatorios automáticos** para pull requests pendientes, enviados a través de un **canal de Slack**.

## 7. Roles DENTRO de un Team (distinto al rol de organización)

Dentro del panel de **Members** de un equipo, cada miembro tiene uno de **2 roles internos del equipo**:

| Rol interno del equipo | Qué puede hacer |
|---|---|
| **Member (afiliado)** | **No puede hacer ninguna de las acciones de gestión listadas abajo** |
| **Maintainer** | Tiene permisos de gestión sobre el equipo (ver lista completa abajo) |

> **Importante:** este rol (Member/Maintainer) es **interno al equipo**, es **distinto** del rol organizacional (Read/Triage/Write/Maintain/Admin).

### Qué puede hacer un Maintainer de equipo

- Cambiar **nombre, descripción y visibilidad** del equipo
- Solicitar agregar un **equipo hijo**, o agregar/quitar un **equipo padre** (mover el equipo)
- Establecer la **foto de perfil** del equipo
- **Agregar o quitar miembros** de la organización al equipo
- **Quitar el acceso del equipo** a repositorios
- Gestionar las **asignaciones de code review** del equipo
- Gestionar los **recordatorios programados** de pull requests

## 8. Agregar miembros a un Team

Desde la pestaña **Members** del equipo → "Add a member" → buscar y seleccionar → "Invite".

Se puede filtrar la vista de miembros por su rol interno del equipo (Member / Maintainer).

## 9. Vista personal de "mis equipos"

Como usuario individual (no como vista de administración de la organización), puedes ver los equipos a los que perteneces desde tu **panel personal (dashboard)**, con acceso directo a la página de cada equipo.

## 10. Asignar un Team a un Repositorio

**Diferencia clave de interfaz — Colaboradores vs Equipos:**

| Si en Settings del repo ves... | Significa que... |
|---|---|
| **"Collaborators"** | Es un repositorio **personal** (no de organización) |
| **"Collaborators and teams"** | Es un repositorio **propiedad de una organización** |

### Pasos para asignar un equipo a un repositorio

```
Repositorio → Settings → Collaborators and teams → Add teams
```

Al agregar el equipo, se le asigna uno de los **5 roles de repositorio** ya vistos en la sección anterior:

```
Read | Triage | Write | Maintain | Admin
```

Esto define qué nivel de acceso **todos los miembros del equipo** tendrán sobre ese repositorio específico.

### Herencia de permisos en equipos anidados

**Si un equipo es un equipo hijo (nested team) de un equipo padre**, el equipo hijo **hereda automáticamente** los permisos relevantes que el equipo padre tenga asignados sobre los repositorios.