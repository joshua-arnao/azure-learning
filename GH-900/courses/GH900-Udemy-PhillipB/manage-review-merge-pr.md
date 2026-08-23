# Manage, Review and Merge Pull Requests

---

## 1. La vista de lista de Pull Requests — filtros disponibles

Desde la pestaña **"Pull requests"** puedes filtrar por:

- Autor
- Etiquetas (labels)
- Proyectos
- Hitos (milestones)
- Revisores (reviewers)
- Asignado (assignee)
- Estado: **abiertos** o **cerrados** (por defecto se muestran los **abiertos**)

**Atajos útiles de filtro:**
- `assigned to you` → PRs/issues asignados a ti
- `@usuario` (mención) → PRs donde te mencionaron
- Puedes combinar sintaxis avanzada de búsqueda para filtros más específicos.

> **Dato importante:** si un PR ya está **cerrado (merged o closed)**, no aparecerá en la vista por defecto — necesitas cambiar manualmente el filtro a "Closed" para volver a verlo.

## 2. Reviewers 

| Plan                                     | Máximo de revisores permitidos |
|:-----------------------------------------|:-------------------------------|
| **General (la mayoría de los casos)**    | Hasta **15 revisores**         |
| **Repositorio privado en plan gratuito** | Solo **1 revisor**             |

**Rol del revisor:** examinar el código y luego **comentar, aprobar, o solicitar cambios adicionales** — se profundiza en una sección posterior sobre "code review".

### Diferencia entre Reviewer y Assignee

| Rol          | Función                                                                                                                      |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------|
| **Reviewer** | Debe examinar el código formalmente y dar su veredicto (aprobar/solicitar cambios/comentar)                                  |
| **Assignee** | Persona responsable del PR (ej. el dueño o quien debe completarlo) — **no se le pide obligatoriamente que comente o revise** |

> **Punto de examen:** si tú eres agregado como **reviewer** de un PR, verás un aviso en la parte superior de la pantalla indicando que **ese PR está esperando tu revisión**.

## 3. Acciones disponibles al interactuar con un PR

| Acción                                  | ¿Cierra el PR?                        |
|:----------------------------------------|:--------------------------------------|
| **Agregar un comentario**               | ❌ No                                 |
| **"Close pull request"** (sin comentar) | ✅ Sí — cierra sin fusionar           |
| **"Merge pull request"**                | ✅ Sí — cierra fusionando los cambios |

## 4. Los 3 métodos de Merge

Al hacer clic en "Merge pull request", el desplegable ofrece 3 opciones distintas de cómo se integra el historial:

### 4.1 — Merge Commit (Create a merge commit)

- Agrega **todos los commits** del PR a la rama base tal cual son.
- Crea además **un commit adicional de fusión** que une ambas historias.
- **Resultado**: historial **no lineal** — se ve la bifurcación real que existió (los commits de la rama separada, más el commit de merge que los junta).

```
main:     A ── B ─────────────── M (merge commit)
                   \             /
feature:            C ── D ─────
```

### 4.2 — Squash and Merge

- Toma **todos los commits** del PR y los combina en **un solo commit nuevo**.
- Ese commit nuevo:
    - Tiene un **mensaje por defecto editable**.
    - Incluye, en la descripción, **todos los mensajes de commit originales** (como referencia).
- **Resultado:** historial lineal y limpio — un solo commit representa todo el PR, sin importar cuántos commits intermedios tuvo el trabajo real.

```
main:     A ── B ── S (squash: contiene C+D combinados)
```

### 4.3 — Rebase and Merge

- **Reescribe** todos los commits del PR como **nuevos commits** aplicados sobre la punta de la rama base.
- Esto genera **nuevos SHA** (hashes distintos) para cada commit — técnicamente son objetos diferentes a los originales, aunque el contenido final sea equivalente.
- **Resultado:** historial lineal, pero **conservando cada commit individual** (a diferencia de squash, que los combina en uno solo).

```
main:     A ── B ── C' ── D'   (C' y D' son versiones reescritas de C y D)
```

### ⚠️ Restricción importante de Rebase and Merge

**No se puede usar si el PR tiene conflictos de fusión** (merge conflicts) — es decir, si algo cambió tanto en el repositorio original como en tu rama, generando choque de contenido.

Además, GitHub lo considera **potencialmente inseguro** en ciertos escenarios, porque **los resultados pueden diferir** de lo que se obtendría con un merge commit tradicional (al reescribir el historial, hay más margen para inconsistencias sutiles).

---

## 5. Tabla comparativa de los 3 métodos (para memorizar rápido)

| Método | ¿Cuántos commits nuevos crea? | ¿Historial lineal? | ¿Conserva commits originales? | ¿Funciona con conflictos? |
|---|---|---|---|---|
| **Merge commit** | 1 commit de fusión (+ mantiene los originales) | ❌ No — muestra la bifurcación real | ✅ Sí | ✅ Sí |
| **Squash and merge** | 1 commit (combinado) | ✅ Sí | ❌ No — se combinan en uno solo | ✅ Sí |
| **Rebase and merge** | N commits nuevos (uno por cada commit original, reescrito) | ✅ Sí | ⚠️ Contenido sí, pero con **SHA nuevo** | ❌ No, si hay conflictos |

---

## 6. Después de fusionar (Post-Merge)

- Se puede añadir un **mensaje y descripción** al commit de fusión.
- Una vez completado el PR, puedes (opcionalmente) **eliminar la rama** que se usó para esos commits — ya cumplió su propósito.
- Si estás **suscrito** al PR, recibes una **notificación por correo** cuando se completa la fusión.

---

## 7. Verificación visual del resultado

Después de fusionar, al revisar los archivos del repositorio:
- Se ve el **ícono distinto** en los archivos modificados por otra persona (ej. Jane).
- Al pasar el mouse sobre el hipervínculo del autor, se confirma **quién hizo esa modificación específica**.

---

## Resumen visual completo del ciclo de vida de un PR

```
Lista de PRs (filtrable por autor, label, milestone, reviewer, assignee, open/closed)
            │
            ▼
   Abrir un PR específico
            │
      ┌─────┴──────────────────────┐
      ▼                            ▼
  Comentar                    Ver: Conversation / Commits /
  (no cierra el PR)            Checks / Files changed
      │
      ▼
  Reviewer aprueba / solicita cambios
      │
      ┌───────────┴───────────┐
      ▼                       ▼
  Close (sin merge)      Merge pull request
  → puede reabrirse           │
                    ┌─────────┼─────────┐
                    ▼         ▼         ▼
              Merge commit  Squash   Rebase
                                        │
                              (bloqueado si hay
                               conflictos de merge)
```

---