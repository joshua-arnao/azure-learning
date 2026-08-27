# Use GitHub Actions for Automation

## 1. ¿Qué es GitHub Actions?

Es la herramienta de GitHub para **automatizar CI/CD** (Continuous Integration / Continuous Delivery). Permite:

- **Construir, probar y desplegar** código automáticamente.
- Ejecutar **pruebas automáticas** cuando hay cambios en el repositorio.
- Desplegar automáticamente a producción cuando se fusiona un Pull Request.
- Desplegar código a **Microsoft Azure**.
- Crear infraestructura mediante código — esto se llama **Infrastructure as Code (IaC)**.


## 2. ¿Qué es YAML?

Los workflows de GitHub Actions se escriben en sintaxis **YAML**.

> **Origen del nombre :** originalmente "YAML" significaba *"Yet Another Markup Language"*, pero hoy significa **"YAML Ain't Markup Language"** — un acrónimo recursivo que refleja que YAML está enfocado en **representar datos**, no en marcado de documentos (a diferencia de HTML/XML).

## 3. Estructura de un Workflow — los 2 componentes principales

| Componente | Qué define                                                |
|:-----------|:----------------------------------------------------------|
| `name`     | El nombre del workflow                                    |
| `on`       | Los **triggers** cuándo se ejecuta el workflow            |
| `jobs`     | Las **acciones/tareas** que se ejecutan cuando se dispara |

---

## 4. Tipos de Triggers (`on`)

### Triggers basados en eventos del repositorio

| Trigger                                               | Se dispara cuando...                                                                                                                                |
|:------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|
| **push**                                              | Se hace push de un commit o tag a una rama (ej. `main`)                                                                                             |
| **pull_request**                                      | Hay actividad en un Pull Request                                                                                                                    |
| **create / delete**                                   | Se crea o elimina una rama o tag                                                                                                                    |
| **discussion**                                        | Se crea, edita o responde una discussion                                                                                                            |
| **discussion_comment**                                | Se crea, edita o elimina un comentario en una discussion                                                                                            |
| **fork**                                              | Alguien forkea el repositorio                                                                                                                       |
| **issues**                                            | Se crea o modifica un issue                                                                                                                         |
| **issue_comment**                                     | Se crea, edita o elimina un comentario en un issue **o en un pull request**                                                                         |
| **merge_group**                                       | Un PR se añade a una cola de fusión (merge queue)                                                                                                   |
| **milestone**                                         | Se crea, edita, elimina, cierra o abre un milestone                                                                                                 |
| **public**                                            | La visibilidad del repositorio cambia de privado a público (**no existe el evento inverso** — no hay trigger para cuando pasa de público a privado) |
| **pull_request_review / pull_request_review_comment** | Actividad de revisión/comentarios en un PR                                                                                                          |
| **pull_request_target**                               | Similar a pull_request pero con contexto de seguridad distinto                                                                                      |
| **status**                                            | Cambia el estado de un commit de Git (error, failure, pending, success)                                                                             |
| **workflow_run**                                      | Cuando otro workflow ha sido solicitado, completado o está en ejecución                                                                             |

### `issue_comment` vs `pull_request` comment

> **GitHub recomienda usar `issue_comment` en lugar de un evento específico de "comentario de PR"**, porque, técnicamente, un Pull Request **es tratado como un tipo especial de Issue** internamente en la API de eventos. Por eso `issue_comment` cubre comentarios tanto de issues como de PRs.

### Triggers externos al repositorio

- **repository_dispatch**, evento disparado externamente vía API hacia GitHub.

### Trigger manual y programado

| Trigger               | Detalle                                                         |
|:----------------------|:----------------------------------------------------------------|
| **workflow_dispatch** | Ejecución **manual** del workflow                               |
| **schedule**          | Ejecución en **horarios programados**, usando sintaxis **cron** |

---

## 5. Sintaxis Cron (para el trigger `schedule`) — profundización técnica

Un cron tiene **5 valores** en este orden:

```
minuto  hora  día-del-mes  mes  día-de-la-semana
```

| Símbolo         | Significado                               |
|:----------------|:------------------------------------------|
| `0`             | Ese valor exacto (literalmente cero)      |
| `*` (asterisco) | "Todos" — cualquier valor válido          |
| `,` (coma)      | Lista de valores específicos (ej. `0,12`) |
| `-` (guión)     | Rango de valores (ej. `0-12`)             |

### Ejemplos

| Cron                      | Significado                                                                          |
|:--------------------------|:-------------------------------------------------------------------------------------|
| `0 0 * * *`               | Medianoche, todos los días del mes, todos los meses, todos los días de la semana     |
| `0 0,12 * * *`            | Medianoche **y** mediodía, todos los días                                            |
| `0 0-12 * * *`            | Cada hora, desde medianoche hasta mediodía (13 ejecuciones: 0,1,2...12)              |
| `0 0,12 * * 1-5`          | Medianoche y mediodía, **solo de lunes a viernes**                                   |
| `0 0,12 * * mon-fri`      | Igual que arriba — se puede usar el nombre abreviado del día en vez del número       |
| `0 0,12 * * mon,fri`      | Medianoche y mediodía, **solo lunes y viernes** (no todo el rango, solo esos 2 días) |
| `0 0,12 1 jan *`          | Medianoche y mediodía, día 1 de enero (se puede usar el nombre del mes)              |
| `0 0,12 1,8,15,22,29 * *` | Medianoche y mediodía, los días 1, 8, 15, 22 y 29 de cada mes                        |

## 6. Jobs — qué hace el workflow

| Elemento del Job        | Qué define                                                        |
|:------------------------|:------------------------------------------------------------------|
| **Identificador único** | Nombre técnico del job                                            |
| `name`                  | Nombre legible (ej. "build", "test")                              |
| `runs-on`               | El tipo de máquina/sistema operativo (ej. Ubuntu, Windows, macOS) |
| `steps`                 | Las tareas reales dentro del job                                  |

### Dentro de `steps`

| Campo  | Qué es                                                                                         |
|:-------|:-----------------------------------------------------------------------------------------------|
| `uses` | Referencia a una **acción predefinida** que se ejecutará (creada por el usuario o de terceros) |
| `name` | Nombre del paso específico                                                                     |
| `run`  | El comando de línea de comandos que se ejecutará directamente                                  |

> **Los jobs, por defecto, se ejecutan en paralelo (al mismo tiempo)**, no de forma secuencial, salvo que se configure explícitamente una dependencia entre ellos.


## 7. Dónde se puede usar/obtener Actions

- Puedes **crear y usar** acciones dentro de tu propio repositorio.
- Puedes **publicarlas en el GitHub Marketplace** para que otros las descarguen y usen.

### Qué más se encuentra en el Marketplace (además de Actions)

- Extensiones de **Copilot**
- **Modelos de IA**
- **Apps** que se integran con GitHub

## Resumen visual de la estructura de un Workflow YAML

```yaml
name: [nombre del workflow]

on:                          # TRIGGERS
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:                        # ACCIONES
  build:                     # identificador único del job
    runs-on: ubuntu-latest   # tipo de máquina
    steps:
      - name: [nombre del paso]
        uses: [acción predefinida]
      - name: [otro paso]
        run: [comando de línea de comandos]
```