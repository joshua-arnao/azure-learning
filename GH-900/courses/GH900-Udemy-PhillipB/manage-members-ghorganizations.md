# Privacy, Security, and Administration — Manage Members

## 1. Requisito previo: solo aplica a Organizaciones

La pestaña **"People"** (Personas), donde se gestionan los miembros, **solo existe en cuentas de Organización** si no la ves, probablemente estés en una **cuenta personal**, que no tiene este concepto de "miembros".


## 2. Filtros disponibles en la lista de miembros

| Filtro | Opciones |
|:---|:---|
| **Por nombre** | Búsqueda directa |
| **Por autenticación de 2 factores (2FA)** | Todos / Solo con 2FA deshabilitado |
| **Métodos de 2FA reconocidos** | Claves de seguridad, apps de autenticación, la app móvil de GitHub, o **SMS** (marcado explícitamente como método **"inseguro"** frente a los demás) |
| **Por afiliación (rol)** | Owners / Members (no-owners) / Todos |

### Exportar la lista

Se puede exportar en formato **JSON** o **CSV** (valores separados por comas).

## 3. Invitar nuevos miembros

Al invitar, se asigna uno de **2 roles** disponibles:

| Rol | Permisos |
|:---|:---|
| **Owner** | **Derechos administrativos completos** sobre la organización — acceso total a repositorios y equipos |
| **Member** | Puede ver a todos los demás miembros, se le puede dar acceso a repos específicos, y **puede crear nuevos equipos y repositorios** |

### ⏳ Dato clave de examen: expiración de la invitación

**La invitación expira en 7 días** si no se responde.


## 4. Gestionar un miembro existente

Al hacer clic en un miembro puedes ver/modificar:

- Su **afiliación** (Member ↔ Owner) — es cambiable después de agregarlo
- A qué **repositorios** tiene acceso
- Qué **roles** tiene
- A qué **equipos** pertenece
- Opción de convertirlo en **colaborador externo (outside collaborator)**
- Opción de **eliminarlo** de la organización

### Visibilidad de la afiliación

Puedes ver si la pertenencia del miembro a la organización es:
- **Pública** (visible en su perfil de GitHub para cualquiera), o
- **Privada** (solo visible para otros miembros de la organización)

### Vistas adicionales en el panel lateral (People)

- **Members** (miembros actuales)
- **Outside collaborators**
- **Pending invitations** (invitaciones pendientes)
- **Failed invitations** (invitaciones fallidas)
- **Security managers**


## 5. Roles predefinidos a nivel de Organización (Role Assignment)

Se accede vía: **Organization → Settings → Organization roles → Role assignments → New role assignment.**

Se pueden asignar a **usuarios individuales o equipos completos**. Existen **5 roles predefinidos**:

| Rol | Nivel de acceso | Para quién está pensado |
|:----|:---|:---|
| **All-repository read** | Solo lectura en todos los repos | Colaboradores **no técnicos** que necesitan ver y discutir el proyecto, sin tocar código |
| **All-repository triage** | Gestión de issues y PRs, **sin acceso de escritura** al código | Colaboradores que organizan/priorizan trabajo, pero no escriben código |
| **All-repository write** | Puede hacer push al proyecto | Gestores de proyecto que necesitan manejar el repo activamente |
| **All-repository maintain** | Gestión más amplia del repo, **sin permisos administrativos completos** (no puede hacer acciones sensibles/destructivas) | Mantenedores — nivel intermedio antes de admin |
| **(Admin — reservado para dueños/admins)** | Control total, incluye acciones destructivas (ej. eliminar un repositorio) y gestión de seguridad | Administradores plenos |


### Roles adicionales especializados

| Rol | Qué gestiona |
|:---|:---|
| **App manager** | Gestiona las **GitHub Apps** de la organización |
| **CI/CD admin** | Gestiona políticas de **Actions**: runners, runner groups, configuración de red, secrets, variables y métricas de uso |
| **Security manager** | Gestiona **políticas de seguridad, alertas y configuraciones** para la organización y todos sus repositorios |


## 6. Roles personalizados (Custom roles) — exclusivo de Enterprise

**Requiere GitHub Enterprise.** Permite crear **hasta 5 roles personalizados**, definiendo permisos específicos y granulares más allá de los roles predefinidos.

---

## Resumen visual — Jerarquía de roles de organización (de menor a mayor acceso)

```
Read  →  Triage  →  Write  →  Maintain  →  Admin/Owner
(solo    (gestiona    (push al   (gestión    (control total,
 ver)     issues/PR)   proyecto)  amplia,      incluye borrar
                                   sin admin)   repos, seguridad)

Roles especializados (paralelos, no jerárquicos):
  App manager · CI/CD admin · Security manager
```