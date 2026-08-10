# Azure DevOps - Sesión 01

---

## Azure DevOps

Azure DevOps es una plataforma que permite gestionar todo el ciclo de vida de desarrollo de software.

No está enfocada únicamente en CI/CD, sino que cubre desde la gestión de requerimientos hasta la puesta en producción de una solución.

---

## Componentes de Azure DevOps

### Overview
Permite visualizar información general del proyecto:

- Resumen del proyecto
- Métricas
- Indicadores
- Estadísticas

### Dashboard

Permite crear paneles personalizados para monitorear:

- Estado del proyecto
- Actividades
- Indicadores
- Avance de sprints

### Wiki

Repositorio de documentación del proyecto.

Se utiliza para:

- Documentación funcional
- Documentación técnica
- Procedimientos
- Manuales

### Boards

Equivalente a Jira dentro de Azure DevOps.

Permite gestionar:

- Épicas
- Features
- Historias de Usuario
- Bugs
- Tareas
- Sprint Backlog
- Product Backlog

### Repos

Sistema de control de versiones basado en Git.

Incluye:

- Commits
- Push
- Pull Requests
- Branches
- Tags

También puede integrarse con GitHub y otros repositorios externos.

### Pipelines

Permite implementar procesos CI/CD.

#### Continuous Integration (CI)

- Compilación automática
- Validaciones
- Ejecución de pruebas

#### Continuous Delivery / Deployment (CD)

- Publicación
- Despliegues
- Automatizaciones

### Test Plans

Permite administrar:

- Casos de prueba
- Ejecuciones
- Evidencias
- Reportes

### Artifacts

Repositorio de paquetes y dependencias.

Puede reemplazar herramientas como:

- JFrog Artifactory
- Maven Repository

---

## Licenciamiento

La versión gratuita permite:

- Hasta 5 usuarios
- Creación de múltiples proyectos
- Uso de Boards
- Uso de Repos
- Uso de Pipelines
- Uso de Test Plans

Incluye aproximadamente:

- 2 GB de almacenamiento compartido


---

## DevOps

DevOps es la integración de **Personas**, **Procesos** y **Productos** para permitir la entrega de valor al cliente final.

### Personas

- Desarrolladores
- QA
- Operaciones
- Product Owner
- Arquitectos

### Procesos

- Metodologías ágiles
- Flujos de trabajo
- Automatización

### Productos

- Soluciones entregadas al cliente

---

## Ciclo DevOps

El ciclo presentado fue:

```text
Plan
↓
Code
↓
Build
↓
Test
↓
Release
↓
Operate
↓
Monitor
↓
Improve
```

Es un proceso continuo de mejora.

---

## Azure DevOps dentro del SDLC (**Software Development Life Cycle**)

| Etapa          | Herramienta   |
|:---------------|:--------------|
| Requerimientos | Boards / Wiki |
| Planificación  | Boards        |
| Desarrollo     | Repos         |
| Testing        | Test Plans    |
| Despliegue     | Pipelines     |
| Monitoreo      | Dashboard     |

---

## Work Items

Es el elemento principal de Azure DevOps.

Un Work Item representa una unidad de trabajo.

Puede ser:

- Epic
- Feature
- User Story
- Task
- Bug
- Test Case

Toda la gestión del proyecto se realiza mediante Work Items.

---

## Procesos Disponibles para cada proyecto creado en Azure DevOps

### Basic
Tipificación de lo que se puede abarcar, Incluye:

- Epic
- Issue
- Task

Proceso básico con pocas opciones.

### Scrum

Incluye elementos propios de Scrum, es decir se puede rastrear el trabajo con Items de backlog de producto:

- Task
- Epic
- Features
- Errors


### Agile

Proceso recomendado para el curso.

Permite:

- Más Work Items
- Mayor flexibilidad
- Mayor personalización

### CMMI

Orientado a organizaciones con procesos más formales.

---

## Integración del Ecosistema

Azure DevOps permite conectar todos sus componentes.

Ejemplo:

```text
Work Item
    ↓
Commit
    ↓
Pull Request
    ↓
Pipeline
    ↓
Deploy
```

Esto proporciona trazabilidad completa entre gestión, desarrollo y despliegue.

---

## Organización y Proyecto

Estructura básica:

```text
Organización
    └── Proyecto
            ├── Boards
            ├── Repos
            ├── Pipelines
            ├── Test Plans
            └── Artifacts
```

Durante el laboratorio se creó:

- Una organización
- Un proyecto privado
- Repositorio Git
- Proceso Agile

---

## Configuración Inicial

### Zona Horaria

Configurar:

```text
Lima
```

Para mantener consistencia en logs y registros.

### Proceso Recomendado

```text
Agile
```

Porque habilita todas las funcionalidades utilizadas durante el curso.

### Activación de Epics

Se habilitó el nivel de Épicas dentro de la configuración del proyecto.

---

## Jerarquía de Trabajo

La estructura utilizada fue:

```text
Epic
    ↓
Feature
    ↓
User Story
    ↓
Task
```

Cada nivel descompone el trabajo en mayor detalle.

---

## Epic

Representa una funcionalidad grande del sistema.

Ejemplo:

```text
Implementar Login
```

Puede contener varios Features relacionados.

---

## Feature

Representa una funcionalidad específica derivada de una Epic.

Ejemplo:

```text
Maquetado de Login
```

Puede contener varias Historias de Usuario.

---

## User Story

Representa una necesidad concreta del usuario.

Normalmente incluye:

- Descripción
- Objetivo
- Criterios de aceptación

---

## Gherkin

Formato utilizado para documentar escenarios funcionales.

Estructura:

```gherkin
Feature:

Scenario:

Given
When
Then
```

Es ampliamente utilizado en automatización de pruebas.

---

## Información de un Work Item

Cada Work Item puede contener:

- Título
- Descripción
- Responsable
- Estado
- Prioridad
- Riesgo
- Esfuerzo
- Fechas
- Comentarios
- Adjuntos
- Relaciones

---

## Relaciones entre Work Items

Azure DevOps soporta:

```text
Parent
Child
Dependency
Related
Blocked
```

Permitiendo construir relaciones entre los elementos del proyecto.

---

## Colaboración

Los Work Items permiten:

- Comentarios
- Conversaciones
- Menciones mediante @usuario
- Seguimiento de cambios

---

## Trazabilidad

Se registran automáticamente:

- Modificaciones
- Usuario que realizó el cambio
- Fecha del cambio
- Historial completo

Esto facilita auditoría y seguimiento.

---

## Tags

Los Work Items pueden etiquetarse para mejorar la organización.

Ejemplos:

```text
Backend
Frontend
Campus
Seguridad
```

---

## Filtros

Se pueden realizar búsquedas por:

- Estado
- Responsable
- Área
- Etiquetas
- Tipo de Work Item

---

## Backlog

Es el repositorio central del trabajo pendiente.

Permite:

- Priorizar actividades
- Organizar funcionalidades
- Gestionar dependencias
- Preparar sprints

---

## Board Kanban

Permite visualizar el flujo de trabajo.

Ejemplo de estados:

```text
New
Active
QA
Integration
Production
Closed
```

Las columnas son personalizables.

---

## Sprint Planning

Las historias se distribuyen entre distintos sprints.

Ejemplo:

```text
Sprint 1
Sprint 2
Sprint 3
```

Cada sprint contiene el trabajo comprometido para ese período.

---

## Capacity Planning

Permite definir la capacidad de trabajo de cada integrante.

Se utiliza para:

- Balancear carga
- Evitar sobreasignaciones
- Planificar correctamente el sprint

---

## Esfuerzo vs Capacidad

### Esfuerzo

Puntos necesarios para completar una historia.

### Capacidad

Trabajo real que puede asumir una persona o equipo.

La planificación debe considerar ambos factores.

---

## IA y MCP

Azure DevOps puede integrarse con herramientas de IA mediante MCP.

Permite:

- Consultar proyectos
- Crear Work Items
- Automatizar tareas
- Operar utilizando lenguaje natural

---

## Ideas Clave de la Sesión

- Azure DevOps es una plataforma integral y no solamente CI/CD.
- Boards es el equivalente a Jira.
- Work Item es la unidad central de trabajo.
- Agile fue el proceso recomendado para el curso.
- La jerarquía principal es:

```text
Epic
→ Feature
→ User Story
→ Task
```

- Azure DevOps integra planificación, desarrollo, pruebas y despliegue en una sola plataforma.
- La trazabilidad entre requerimientos, código y despliegues es uno de sus principales beneficios.