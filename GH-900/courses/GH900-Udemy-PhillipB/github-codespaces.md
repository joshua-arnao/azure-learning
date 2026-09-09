# What Are GitHub Codespaces?

## 1. ¿Qué es un Codespace?

Un **Codespace** es un **entorno de desarrollo basado en la nube** — se aloja en un **contenedor Docker** que ejecuta **Linux** dentro de una **máquina virtual**.

> Se clasifica como herramienta de "code review" porque permite abrir y probar el código de un PR **en un entorno completo y aislado**, sin necesidad de clonar nada localmente.

## 2. Especificaciones técnicas del contenedor

| Recurso             | Rango                 |
|:--------------------|:----------------------|
| **Núcleos (cores)** | Entre **2 y 32**      |
| **RAM**             | Entre **8 y 64 GB**   |
| **Almacenamiento**  | Entre **32 y 128 GB** |

## 3. Asignación gratuita — Cuentas personales (GitHub Free)

| Recurso            | Cantidad gratuita mensual    |
|:-------------------|:-----------------------------|
| **Core hours**     | **120 horas**                |
| **Almacenamiento** | Promedio de **15 GB** al mes |

### ¿Qué es una "core hour"?

**No es simplemente "una hora de uso"** — se calcula multiplicando el tiempo de uso por la cantidad de núcleos activos.

> Como el contenedor mínimo tiene **2 núcleos**, con 120 horas de núcleo disponibles, el tiempo real de uso continuo sería de **máximo 60 horas**, si usas la configuración mínima.

## 4. Asignación gratuita — Plan GitHub Pro

| Recurso            | Cantidad gratuita mensual    |
|:-------------------|:-----------------------------|
| **Core hours**     | **180 horas**                |
| **Almacenamiento** | Promedio de **20 GB** al mes |

> **Sobre el "promedio mensual" de almacenamiento:** no es un tope fijo de una sola vez, se evalúa como un **promedio a lo largo del mes**, recalculado mensualmente.

## 5. Notificaciones y bloqueo de uso

- Recibes un **correo electrónico** al alcanzar **75%, 90% y 100%** de tu asignación gratuita.
- Al llegar al 100%, el uso de Codespaces se **bloquea** — **a menos que** tengas configurado un **método de pago** y un **presupuesto (budget)** establecido.


## 6. Costos por uso adicional (más allá de la asignación gratuita)

| Recurso                                         | Costo         |
|:------------------------------------------------|:--------------|
| **Por hora de núcleo adicional**                | **$0.09 USD** |
| **Por GB de almacenamiento (promedio mensual)** | **$0.07 USD** |

> **Detalle importante**: se cobra **tanto si el Codespace está activo como inactivo** (mientras exista y ocupe espacio/recursos asignados). Sin embargo, **los contenedores basados en la imagen por defecto NO cuentan como almacenamiento usado**.

## 7. Formas de crear un Codespace

| Método                                  | Detalle                                                                                                                |
|:----------------------------------------|:-----------------------------------------------------------------------------------------------------------------------|
| **Desde una plantilla (template repo)** | "Use this template" → "Open in a Codespace"                                                                            |
| **Desde la pestaña "Code"**             | "Codespaces" → "Create codespace on [rama]"                                                                            |
| **Desde un Pull Request**               | Botón de Codespace visible en la revisión de archivos modificados (útil para probar los cambios de un PR directamente) |
| **Desde una rama específica**           | Se puede elegir la rama al crear                                                                                       |
| **Desde un commit específico**          | También es posible crearlo desde un commit puntual                                                                     |
| **Desde Visual Studio Code**            | Integración directa                                                                                                    |
| **Desde GitHub CLI**                    | Línea de comandos                                                                                                      |

## 8. Opciones avanzadas al crear un Codespaces

| Opción                | Qué permite configurar                                                                   |
|:----------------------|:-----------------------------------------------------------------------------------------|
| **Branch**            | Rama sobre la que se crea                                                                |
| **Region**            | Región geográfica del servidor                                                           |
| **Machine type**      | Tipo/tamaño de máquina                                                                   |
| **Dev container**     | Edita el archivo `devcontainer.json` — define la configuración del entorno de desarrollo |
| **Prebuild settings** | Configuración de **pre-construcción** para acelerar la creación de Codespaces futuros    |

### Prebuild

Las **prebuilds** ejecutan de antemano todas las tareas necesarias para construir el entorno de desarrollo, **acelerando** la creación de nuevos Codespaces.

Configuraciones disponibles para prebuilds:
- **Cuándo se ejecuta:** en cada push, según un calendario (schedule), o cuando cambia la configuración
- **Qué regiones** se usarán
- **Cuántas versiones de prebuild conservar** — **máximo 5**
- **Quién es notificado** si una prebuild falla

## 9. Codespaces a nivel de Organización

- Si eres **dueño de una organización** en un plan de pago (GitHub Team o GitHub Enterprise Cloud), puedes **habilitar o deshabilitar** el uso de Codespaces para los miembros — configurable en **Settings de la organización**.

> **Dato importante**: **las organizaciones NO tienen asignación gratuita de Codespaces** — la cuota gratuita (120h/180h) **es exclusiva de cuentas personales**. En una organización, el uso se cobra directamente según la configuración de facturación establecida.

## 10. Dónde se clona el repositorio dentro del Codespace

Al crear un Codespace, el repositorio se clona automáticamente dentro de la carpeta:

```
/workspaces/
```