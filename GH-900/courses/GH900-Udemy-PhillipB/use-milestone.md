# Use Milestones

---

## 1. ¿Qué es un Milestone?

Un **Milestone (hito)** se usa para **rastrear el progreso** de un conjunto de Issues y/o Pull Requests relacionados. Puedes asignar el **mismo milestone a múltiples elementos** y ver cómo avanzan colectivamente respecto a un plan.

**Idea central:** es una forma de **agrupar** trabajo relacionado bajo un objetivo común y medir avance como porcentaje.

## 2. Crear un Milestone

**Rutas de acceso:**
```
Pestaña "Issues" → Milestones → New milestone
```
o
```
Pestaña "Pull requests" → Milestones → New milestone
```
(Ambas rutas llevan al mismo lugar — los milestones no son exclusivos de issues ni de PRs.)

### Campos al crear uno

| Campo                               | Obligatorio |
|:------------------------------------|:------------|
| **Título**                          | ✅ Sí       |
| **Fecha de vencimiento (due date)** | ❌ Opcional |
| **Descripción**                     | ❌ Opcional |


## 3. Gestión de Milestones existentes

Desde "..." junto a un milestone puedes: **editar, cerrar o eliminar**.

### Opciones de ordenamiento (sort)

- Fecha de vencimiento: más lejana / más cercana
- Actualizado recientemente
- Más completo / menos completo
- Alfabético / alfabético inverso
- Más issues / menos issues


## 4. Vista de detalle de un Milestone

Al abrir un milestone individual se ve:
- **Fecha de vencimiento**
- **% completado** (0% si no tiene issues/PRs asignados aún, o si ninguno se ha cerrado)
- **Issues/PRs abiertos** asignados a ese milestone

## 5. Asignar un Milestone a un Issue/PR

Dos formas:

1. **Masiva**, desde la lista: seleccionar (checkbox) varios issues → "Milestone" → elegir uno.
2. **Individual**, desde dentro del issue: clic en el ícono de rueda (⚙️) junto a "Milestone" en el panel lateral.

### ⚠️ Regla clave

**Un Issue o Pull Request solo puede tener UN milestone asignado a la vez** — a diferencia de las labels, donde puedes tener varias simultáneamente. No es posible asignar un segundo milestone al mismo elemento sin antes quitar el primero.

## 6. Cálculo del % completado

El porcentaje se calcula en base a la proporción de **issues/PRs cerrados vs. abiertos** dentro de ese milestone.

> Ejemplo del video: con 3 issues asignados (0 cerrados) = 0%. Al cerrar 1 de los 3 = **33% completado**, con 2 abiertos y 1 cerrado.

Los números de "issues abiertos/cerrados" que se muestran en la lista de milestones son **hipervínculos** — clic en ellos filtra directamente esos issues específicos.


## 7. Priorizar tareas dentro de un Milestone

Dentro de la vista del milestone, puedes **arrastrar y soltar (drag and drop)** issues/PRs para reordenar su prioridad visualmente.

### ⚠️ Límite importante

**Esta función de reordenamiento por arrastre NO está disponible si el milestone tiene más de 500 issues abiertos.**

## 8. Edición masiva (bulk actions) desde la lista

Al seleccionar uno o varios issues/PRs, puedes en conjunto:

- Marcar como **Open / Completed / Not planned**
- Añadir o quitar **Labels**
- Añadir o quitar **Assignees**
- Asignar a un **Project**
- Asignar a un **Milestone**

## Resumen visual del flujo de Milestones

```
Crear Milestone (título obligatorio, fecha y descripción opcionales)
            │
            ▼
   Asignar Issues/PRs al Milestone (uno por elemento, no múltiples)
            │
            ▼
   % completado = cerrados / (abiertos + cerrados)
            │
            ├─ Reordenar por prioridad (drag & drop) — solo si ≤500 issues abiertos
            ├─ Bulk actions (estado, labels, assignees, project)
            │
            ▼
   Cerrar el Milestone cuando el objetivo se cumple
```