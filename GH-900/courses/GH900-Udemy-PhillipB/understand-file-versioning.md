# Understand File Versioning

---

## 1. Cómo Git guarda las instantáneas (el concepto central)

Cuando confirmas (commit) un cambio, Git crea una **nueva instantánea (snapshot)** del contenido de los archivos modificados.

**Optimización clave**: si un archivo **no cambió** en ese commit, Git **no lo vuelve a copiar**, en su lugar guarda una **referencia** al contenido existente (al blob que ya tenía). Esto evita duplicar información y desperdiciar espacio.

Un commit **no es "una copia completa del proyecto"**, es una foto que reutiliza todo lo que no cambió y solo añade lo nuevo.


## 2. Blame View

La vista **Blame** muestra, línea por línea:
- Quién confirmó esa línea
- Cuándo se confirmó
- El mensaje de commit asociado

**Utilidad:** rastrear el origen exacto de cada línea de código, útil para auditoría o para entender el "por qué" de una línea específica.

**Función especial — "Blame antes de este commit" (retroceder versión):** desde Blame puedes pedir ver el archivo tal como estaba **antes** de un commit específico. Al hacerlo, GitHub genera automáticamente una vista de una rama/estado anterior, no es una rama real persistente, es una forma de navegar el historial en ese punto.

---

## 3. Commit Hash / SHA — identificador único

Cada commit tiene un identificador único llamado **SHA (Secure Hash Algorithm)**.

| Dato                              | Detalle                                                                                       |
|:----------------------------------|:----------------------------------------------------------------------------------------------|
| Longitud completa                 | **40 caracteres** hexadecimales                                                               |
| Forma abreviada mostrada en la UI | **7 caracteres** (suficiente para identificarlo de forma práctica en la mayoría de los repos) |
| Se puede copiar completo          | Sí, desde la vista de historial                                                               |


## 4. History View — historial completo de un archivo

Desde el botón **"History"** de un archivo puedes ver:
- Todos los commits que afectaron ese archivo específico (no todo el repo)
- El SHA de cada uno
- Filtros disponibles: **por usuario** y **por rango de fechas**

**Navegación desde el historial:**
- Puedes ver el **código completo del repositorio** tal como estaba justo después de un commit específico (no solo el archivo, el repo entero en ese punto del tiempo).
- Puedes ver específicamente **qué cambió** en un commit dado (el diff de ese commit).


## 5. Diff — cómo se representan los cambios de un commit

Al ver un commit específico, GitHub muestra el diff con codificación de color:

| Color                | Significado     |
|:---------------------|:----------------|
| 🔴 Rojo/rosa con `-` | Línea eliminada |
| 🟢 Verde con `+`     | Línea añadida   |

**Cómo Git representa una edición**: cuando editas una sola palabra dentro de una línea, Git **no muestra "modificación parcial"** — internamente lo representa como **eliminar la línea completa vieja + añadir la línea completa nueva**. Esto es coherente con el principio de que Git trabaja por instantáneas de contenido, no por "parches de texto" a nivel de palabra.

### Dos vistas para revisar un diff

| Vista                   | Qué muestra                                                        |
|:------------------------|:-------------------------------------------------------------------|
| **Unified (unificada)** | Todo en una sola columna, eliminaciones y adiciones intercaladas   |
| **Split (dividida)**    | Dos columnas lado a lado, contenido "antes" y "después" del commit |


## Punto clave para el examen
  
**Un commit nunca duplica contenido innecesariamente.** Git optimiza guardando solo lo que cambió y referenciando lo que no — este es el mecanismo que hace que un repositorio con miles de commits no crezca de forma descontrolada en tamaño.

**El versionado de archivos en GitHub se puede rastrear desde 2 puntos de entrada equivalentes:**
1. **Blame** → enfoque línea por línea, "¿quién escribió esto?"
2. **History** → enfoque cronológico, "¿qué commits tocaron este archivo y en qué orden?"

Ambos terminan llevándote al mismo lugar: un commit específico identificado por su **SHA**, con su diff correspondiente.