# Azure DevOps - Sesión 02
## Resumen Teórico

---

# Gestión de Sprints

Se continuó trabajando sobre los conceptos de:

- Backlog
- Sprint Backlog
- Sprint Planning

Se explicó cómo crear nuevos Sprints dentro de Azure DevOps definiendo:

- Nombre del Sprint
- Fecha de inicio
- Fecha de fin

Los Sprints representan períodos de trabajo donde se agrupan las historias, tareas y actividades que serán desarrolladas por el equipo.

---

# Distribución del Trabajo

Los elementos de trabajo (Work Items) son planificados y distribuidos en distintos Sprints.

La idea es mover los requerimientos desde el Backlog hacia los Sprints donde serán ejecutados.

```text
Backlog
    ↓
Sprint 1
Sprint 2
Sprint 3
...
Sprint N
```

Esto permite organizar y controlar la ejecución del trabajo a lo largo del proyecto.

---

# Seguridad en Azure DevOps

Se revisó el modelo de seguridad y acceso dentro de Azure DevOps.

Existen dos conceptos fundamentales:

## Acceso

Determina qué puede visualizar un usuario.

Ejemplos:

- Ver un proyecto.
- Ver Boards.
- Ver Repositories.
- Ver Pipelines.

## Permisos

Determina qué acciones puede realizar un usuario.

Ejemplos:

- Crear Work Items.
- Modificar código.
- Ejecutar Pipelines.
- Administrar configuraciones.

---

# Acceso a Proyectos

Se explicó que los usuarios deben tener acceso explícito al proyecto.

Si un usuario no tiene acceso al proyecto:

- No podrá visualizarlo.
- No aparecerá dentro de la organización.
- No podrá acceder a Boards, Repos o Pipelines de dicho proyecto.

Concepto importante:

> Tener permisos no es suficiente si no existe acceso al proyecto.

---

# Niveles de Acceso

## Stakeholder

Acceso limitado.

Utilizado normalmente para:

- Seguimiento
- Consulta
- Visualización de información

---

## Contributor

Permite trabajar activamente dentro del proyecto.

Puede:

- Crear Work Items
- Modificar elementos
- Colaborar con el desarrollo

---

## Administrator

Control total sobre el proyecto.

Puede administrar:

- Configuración
- Usuarios
- Seguridad
- Recursos del proyecto

---

# Permisos por Grupos

Dentro de cada proyecto existen grupos de seguridad.

Ejemplos:

- Contributors
- Readers
- Administrators
- Build Administrators

Estos grupos determinan las acciones permitidas dentro del proyecto.

---

# Herencia de Permisos

Se explicó que existen dos niveles de control:

## Nivel 1

Acceso al Proyecto.

```text
¿Puede ingresar al proyecto?
```

## Nivel 2

Permisos del Grupo.

```text
¿Qué puede hacer dentro del proyecto?
```

La relación funciona de la siguiente manera:

```text
Acceso al Proyecto
        ↓
Permisos del Grupo
        ↓
Acciones Permitidas
```

Si el usuario no posee acceso al proyecto, los permisos de grupo no tendrán efecto.

---

# Organización, Proyecto y Seguridad

La estructura lógica presentada fue:

```text
Organización
    │
    ├── Proyecto A
    ├── Proyecto B
    └── Proyecto C
```

Un usuario puede:

- Pertenecer a la organización.
- Tener acceso únicamente a algunos proyectos.
- Poseer diferentes permisos en cada proyecto.

Esto permite separar responsabilidades dentro de una misma organización.

---

# Gestión de Usuarios

Para que un usuario pueda trabajar correctamente se requiere:

```text
Usuario
    ↓
Acceso a la Organización
    ↓
Acceso al Proyecto
    ↓
Permisos del Grupo
```

Todos los niveles deben estar correctamente configurados.

---

# SSH para Azure Repos

Se realizaron pruebas utilizando autenticación SSH para conectarse a los repositorios Git de Azure DevOps.

Objetivos:

- Evitar autenticaciones repetitivas.
- Mejorar la experiencia de desarrollo.
- Utilizar conexiones seguras.
- Facilitar operaciones Git.

Comandos y configuraciones más detalladas quedaron pendientes para una siguiente revisión.

---

# Preparación para Azure Pipelines

Se anunció el inicio de la parte más técnica del curso.

Próximo tema:

## Azure Pipelines

Se trabajará con:

- Integración Continua (CI)
- Compilaciones automáticas
- Ejecución de pruebas
- Despliegues automáticos
- Automatización de procesos

---

# Recomendación para los Laboratorios

Se sugirió llevar proyectos propios para practicar.

Ejemplos:

- Java
- Spring Boot
- .NET
- Node.js
- Python

Recomendación:

```text
No utilizar código ni información real de clientes.
```

Trabajar con proyectos de prueba o ejemplos personales.

---

# Ideas Clave de la Sesión

- Se continuó trabajando con Backlogs y Sprints.
- Se aprendió a crear nuevos Sprints y definir sus fechas.
- Se revisó el modelo de seguridad de Azure DevOps.
- Se diferenciaron claramente los conceptos de Acceso y Permisos.
- Se explicó la relación entre Organización, Proyecto y Seguridad.
- Los permisos de grupo dependen primero del acceso al proyecto.
- Se introdujo el uso de SSH para conectarse a Azure Repos.
- La siguiente fase del curso estará enfocada en Azure Repos y Azure Pipelines.
- Azure Pipelines marcará el inicio de la parte práctica de CI/CD dentro del curso.