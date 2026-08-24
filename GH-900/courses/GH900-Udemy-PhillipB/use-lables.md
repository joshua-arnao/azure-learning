# Use Labels

## 1. ¿Qué es una Label (Etiqueta)?

Las **labels** se usan para **clasificar** Issues, Pull Requests y Discussions. Sirven tanto para categorizar visualmente como para **filtrar** rápidamente el contenido de un repositorio.

## 2. Etiquetas predeterminadas (default labels) que trae GitHub

| Label                | Significado                                          |
|:---------------------|:-----------------------------------------------------|
| **bug**              | Algo no funciona correctamente                       |
| **documentation**    | Mejoras o solicitudes relacionadas con documentación |
| **duplicate**        | El issue/PR es similar a otro ya existente           |
| **enhancement**      | Nueva solicitud de función o mejora                  |
| **good first issue** | Ideal para quienes contribuyen **por primera vez**   |
| **help wanted**      | Se necesita ayuda extra en este issue/PR             |
| **invalid**          | El issue/PR no es válido                             |
| **question**         | Se necesita más información                          |
| **wontfix**          | No se va a trabajar / no se continuará con esto      |


## 3. "Good first issue" — su función especial

Este label tiene un comportamiento particular: si el repositorio usa una **página de contribución (contributing page)**, los issues marcados como `good first issue` se **muestran automáticamente ahí**, como sugerencia para nuevos colaboradores.

**Cómo acceder a la página de contribución:**
```
github.com/usuario/repositorio/contribute
```

## 4. Crear una Label nueva

Al crear una label, defines 3 elementos:

| Campo           | Detalle                                                                                                                |
|:----------------|:-----------------------------------------------------------------------------------------------------------------------|
| **Name**        | Nombre de la etiqueta                                                                                                  |
| **Description** | Explica qué representa la etiqueta                                                                                     |
| **Color**       | Se puede elegir entre **16 colores predefinidos**, un **color hexadecimal** personalizado, o generar uno **aleatorio** |


## 5. Editar / Eliminar una Label

Desde la lista de labels, clic en **"..."** junto a una etiqueta existente para **editarla** o **eliminarla**.


## 6. Labels a nivel de Organización (Default labels organizacionales)

Las organizaciones pueden definir, editar y eliminar **etiquetas predeterminadas** que aplican a nivel general, no solo a un repo individual:

```
Foto de perfil (esquina superior derecha) → Your organizations → 
[seleccionar organización] → Settings → Repository → Repository defaults
```

> Esto permite estandarizar labels **across** todos los repositorios de una organización, en vez de configurarlas repo por repo.

---

## 7. Asignar una Label a un Issue/PR

Dos formas equivalentes:

1. Desde la **lista** de issues: marcar el checkbox del issue → aplicar label.
2. Desde **dentro** del issue: clic en el ícono de rueda (⚙️) junto a la palabra "Labels" en el panel lateral → seleccionar.

---

## 8. Filtrar por Labels — el punto más importante de esta sección

Al hacer clic en una label, se filtra la lista mostrando solo los elementos con esa etiqueta — equivalente a ir a la sección "Labels" y hacer clic ahí directamente.

### ⚠️ El comportamiento contraintuitivo: seleccionar múltiples labels = AND, no OR

Esta es la trampa clásica de examen en este tema:

**Si seleccionas 2 labels desde el filtro estándar (ej. `label:enhancement label:"good first issue"`), GitHub busca issues que tengan AMBAS etiquetas a la vez — no una u otra.**

Si ningún issue individual tiene las dos etiquetas simultáneamente, el resultado será **0 issues**, aunque existan issues con cada etiqueta por separado.

### Cómo cambiar la lógica a OR (unión, no intersección)

| Sintaxis                                     | Comportamiento                                |
|:---------------------------------------------|:----------------------------------------------|
| `label:enhancement label:"good first issue"` | **AND** — debe tener ambas etiquetas a la vez |
| `label:"enhancement,good first issue"`       | **OR** — debe tener al menos una de las dos   |

**Detalle de sintaxis importante:** al usar la forma OR (una sola palabra clave `label:` seguida de una lista separada por comas), **no debe haber espacio** después de la coma — un espacio ahí rompe la búsqueda y no filtra como se espera.

```
✅ Correcto:   label:"enhancement,good first issue"
❌ Incorrecto: label:"enhancement, good first issue"   (con espacio después de la coma)
```


## Resumen visual — AND vs OR al filtrar labels

```
label:bug label:documentation
        │
        ▼
   Busca issues con BUG *Y* DOCUMENTATION simultáneamente (AND)
   → Resultado: probablemente 0, salvo que exista ese caso exacto


label:"bug,documentation"
        │
        ▼
   Busca issues con BUG *O* DOCUMENTATION (OR)
   → Resultado: todos los issues que tengan cualquiera de las dos
```