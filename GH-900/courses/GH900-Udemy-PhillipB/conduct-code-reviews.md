# Conduct Code Reviews

## 1. ¿Qué es un Code Review, exactamente?

**Definición clave**: Es una revisión de código **no es una función separada** es, literalmente, **un Pull Request con uno o más revisores asignados**. No hay un objeto "code review" independiente del PR.

## 2. Paso previo: mantener el fork sincronizado

Antes de trabajar sobre un fork desactualizado, se usa **"Sync fork" → "Update branch"** para traer los últimos cambios del upstream.

## 3. Crear el PR y solicitar revisor

Al crear el Pull Request, en la sección de **Reviewers**, GitHub suele **sugerir automáticamente** al dueño del repositorio original como revisor candidato. También puedes agregar manualmente a **cualquier usuario** haciendo clic en el ícono de rueda (⚙️).

## 4. Comment vs Start a Review

Al comentar sobre un archivo dentro de un PR, hay **dos botones distintos**, con comportamiento muy diferente:

| Opción             | Comportamiento                                                                                                                                                                             |
|:-------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Comment**        | El comentario se **publica de inmediato**, visible para todos al instante — es un comentario individual y aislado.                                                                         |
| **Start a review** | El comentario queda **pendiente/oculto**, visible **solo para ti**, hasta que decidas **enviar (submit)** toda la revisión formal — permite agrupar varios comentarios en un solo paquete. |

> **Regla mental:** *"Comment" = hablar en el chat en vivo. "Start a review" = escribir un borrador de reporte que nadie ve hasta que lo publiques completo.*

Mientras tienes una revisión en progreso, verás un contador (ej. "1 pending") junto al botón **"Review changes"**, indicando cuántos comentarios están acumulados sin enviar todavía.

## 5. Niveles de granularidad al comentar

| Nivel                             | Cómo se hace                                                                                                         |
|:----------------------------------|:---------------------------------------------------------------------------------------------------------------------|
| **Comentar el archivo completo**  | Botón general "Comment" a nivel de archivo                                                                           |
| **Comentar una línea específica** | Clic en el ícono "+" junto a la línea (funciona en líneas añadidas `+` o eliminadas `-`, e incluso en líneas vacías) |
| **Comentar un rango de líneas**   | Clic y **arrastrar** desde la línea inicial hasta la línea final — un solo comentario cubre todo el rango            |

---

## 6. Suggested Changes (Sugerencias de cambio)

Al comentar sobre una línea, puedes hacer clic en el ícono de **"Add a suggestion"**:
- Se pre-carga el texto actual de esa línea.
- Puedes **editarlo directamente** dentro del comentario, proponiendo el reemplazo exacto.
- Esto genera un **"suggested change"** que el autor puede aceptar con un clic (no es solo una sugerencia en texto libre — es un cambio de código aplicable directamente).

---

## 7. Marcar archivos como revisados ("Viewed")

Dentro de la pestaña **"Files changed"**, cada archivo tiene un checkbox **"Viewed"**. Al marcarlo:
- El archivo se **colapsa visualmente** — útil para llevar control de qué ya revisaste en un PR con muchos archivos.

## 8. Finalizar la revisión — "Submit review"

Al hacer clic en **"Review changes"** (arriba del PR), se resumen todos los comentarios acumulados durante la revisión, y debes elegir **uno de 3 veredictos**:

| Veredicto           | Significado                                                                         |
|:--------------------|:------------------------------------------------------------------------------------|
| **Comment**         | Opinión general, sin aprobar ni rechazar formalmente                                |
| **Approve**         | Apruebas los cambios — habilita que el PR pueda fusionarse (si el repo lo requiere) |
| **Request changes** | Pides que se hagan modificaciones antes de que el PR pueda avanzar                  |

> Solo al hacer clic en **"Submit review"** es que todos los comentarios "pendientes" (los que hiciste con "Start a review") se **publican de golpe** y se notifica al autor.

## 9. Notificaciones al autor del PR

Si el autor tiene las notificaciones activas, recibe **un correo electrónico** consolidado con todos los comentarios de la revisión.

## 10. Resolver conversaciones (Resolve conversation)

Cada hilo de comentarios individual tiene un botón **"Resolve conversation"**:
- Marca esa conversación específica como **cerrada/resuelta**.
- **Las conversaciones resueltas se ocultan automáticamente** de la vista — aunque siguen existiendo y se pueden volver a mostrar si es necesario.

## 11. Aplicar una sugerencia de cambio (Suggested Change) — 2 formas

**⚠️ Importante: solo disponible desde la pestaña "Files changed"** (no desde "Conversation").

| Opción | Qué hace |
|---|---|
| **Commit suggestion** | Aplica la sugerencia **inmediatamente** como un commit individual |
| **Add suggestion to batch** | Agrega la sugerencia a un **lote (batch)** — se acumulan varias sugerencias para aplicarlas **todas juntas en un solo commit** al confirmar |

> Con "Add to batch", nada se guarda de verdad hasta que haces clic en **"Commit changes"** para confirmar el lote completo — es el mismo principio de "nada es definitivo sin commit" que vimos en secciones anteriores.

---

## 12. Quién puede comentar/revisar (dato importante)

**No solo las personas explícitamente solicitadas como reviewers pueden opinar.** Cualquier colaborador con acceso puede:
- Ir a "Review changes"
- Agregar comentarios y hacer "Submit review"

**Restricción real:** alguien que no fue solicitado como reviewer formal **puede comentar**, pero **no necesariamente puede Aprobar o Solicitar cambios** con el mismo peso formal — en el video se muestra que esas opciones (Approve / Request changes) pueden no estar disponibles para ciertos usuarios, dejando solo la opción de "Comment".


## 13. Fusionar el Pull Request

Una vez completado el proceso de revisión (y si tienes **permisos suficientes**), puedes desplazarte al final del PR y hacer clic en **"Merge pull request"**, agregar mensaje/descripción, y confirmar la fusión — mismo flujo que vimos en la sección de "Manage, review and merge pull requests".
