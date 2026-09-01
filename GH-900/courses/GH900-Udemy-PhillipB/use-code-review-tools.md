# Use GitHub's Code Review Tools

## 1. Herramientas ya conocidas

Dentro de un Pull Request puedes:
- Añadir **comentarios**
- Crear **sugerencias de código** (suggested changes)
- **Discutir** los resultados esperados de la revisión

## 2. Blame View — aplicado a la revisión de código

Permite ver **quién modificó cada línea** de un archivo y **en qué commit**, pasando el mouse sobre el commit para ver al autor.

## 3. GitHub Copilot como herramienta de Code Review

### Qué puede hacer Copilot en el contexto de revisión de código

| Función                                             | Detalle                                                                                                                                       |
|:----------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------|
| **Revisar código de forma general**                 | Puedes delegarle issues abiertos para que los analice                                                                                         |
| **Crear y probar respuestas**                       | Genera una propuesta de solución, que puede seguir iterando según feedback                                                                    |
| **Usar GitHub Actions**                             | Puede usar Actions como parte del flujo para crear el Pull Request                                                                            |
| **Resumir cambios de un PR**                        | Genera un resumen legible de qué cambió                                                                                                       |
| **Escribir descripciones de PR**                    | Redacta automáticamente la descripción del Pull Request                                                                                       |
| **Analizar código, encontrar y corregir errores**   | Detección y corrección de bugs                                                                                                                |
| **Chat de Copilot**                                 | Preguntas generales de programación — ej. "¿qué es YAML?", "dame ejemplos de sintaxis cron", "escribe JavaScript para obtener la hora actual" |
| **Sugerencias y correcciones de código**            | Autocompletado inteligente                                                                                                                    |
| **Documentar código**                               | Genera comentarios/documentación                                                                                                              |
| **Crear ejemplos / pruebas unitarias (unit tests)** | Genera casos de prueba automáticamente                                                                                                        |
## 4. Planes y precios de GitHub Copilot

| Plan     | Costo                      | Chat / Completions                                        | Solicitudes Premium              | Extras                                                |
|:---------|:---------------------------|:----------------------------------------------------------|:---------------------------------|:------------------------------------------------------|
| **Free** | Gratis                     | Hasta **50 chat requests** y **2,000 completions** al mes | Hasta **50 premium requests**    | —                                                     |
| **Pro**  | **$10/mes** o **$100/año** | Ilimitado                                                 | Hasta **300 premium requests**   | Acceso a agentes de revisión de código y codificación |
| **Pro+** | **$39/mes** o **$390/año** | Ilimitado                                                 | Hasta **1,500 premium requests** | Acceso a **más modelos**                              |

> **Dato importante de examen:** el plan **Pro es gratuito** para: **estudiantes, profesores, instituciones educativas, y mantenedores de proyectos open source populares.**


## Punto clave

**Copilot no reemplaza al reviewer humano** — es una **herramienta de apoyo** dentro del flujo de code review: resume, sugiere, corrige y documenta, pero el proceso formal de aprobación (Approve / Request changes) sigue dependiendo de personas (reviewers o CODEOWNERS).

Los **números de planes de Copilot** (50/2000, 300, 1500 requests; $10 y $39) son el tipo de dato específico que el examen suele preguntar directo — vale la pena memorizarlos en tabla.
