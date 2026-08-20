# Add, Edit, and Delete Files

---

## 1. Permisos necesarios

**El requisito base:** necesitas **acceso de escritura (write access)** al repositorio para crear, editar o eliminar archivos directamente.

Si solo tienes permiso de **lectura**, no puedes editar directamente. GitHub resuelve esto mediante:

```
Repo original (solo lectura para ti)
        │
        │ GitHub lo bifurca (fork) automáticamente a tu cuenta
        ▼
Tu copia (fork) — aquí sí tienes acceso de escritura
        │
        │ haces tus cambios y confirmas
        ▼
Envías un Pull Request al repositorio original
```

**Fork + Pull Request**: **no necesitas permisos de escritura para proponer cambios**, solo para aplicarlos directamente.


## 2. Crear un nuevo archivo

### Pasos en la interfaz de GitHub

1. Clic en **"Add file"**.
2. Elegir entre:
    - **Upload files** (subir archivos existentes desde tu computadora)
    - **Create new file** (crear uno desde cero en el navegador)
3. Escribir el nombre del archivo y su contenido.
4. Clic en **"Commit changes"**.

### La pantalla de confirmación (commit) — opciones disponibles

| Opción                                          | Detalle                                                                                            |
|:------------------------------------------------|:---------------------------------------------------------------------------------------------------|
| **Mensaje de commit**                           | GitHub sugiere uno por defecto (ej. "Create archivo.txt"), pero puedes personalizarlo.             |
| **Descripción extendida**                       | Campo opcional para dar más contexto sobre el cambio.                                              |
| **Commit directo a la rama principal**          | Aplica el cambio inmediatamente a `main`/`master`.                                                 |
| **Crear una nueva rama + iniciar Pull Request** | En vez de tocar `main` directamente, el cambio se aísla en una rama nueva para revisión posterior. |

> **Punto clave:** en todos los casos, crear, editar o eliminar— **el cambio no se aplica hasta hacer commit**. Simplemente escribir o marcar "eliminar" en la interfaz no modifica nada por sí solo.


## 3. Editar un archivo existente

### Cómo acceder a la edición

Al hacer clic en un archivo, por defecto solo puedes **verlo** (modo lectura) — no editarlo directamente ahí. Para editar tienes dos rutas:

| Opción                       | Qué hace                                                        |
|:-----------------------------|:----------------------------------------------------------------|
| **Ícono de edición (lápiz)** | Edita el archivo directamente "in place", dentro del navegador. |
| **Open with GitHub Desktop** | Abre el archivo en la aplicación de escritorio.                 |

### La vista "Blame"

Además de ver y editar, cada archivo tiene una **vista de Blame**, que muestra:
- Cada línea del archivo
- El mensaje de commit asociado a esa línea
- Quién la modificó y cuándo

### Comportamiento del editor (detalles de formato)

- **Tab:** al presionarlo dentro del editor, añade espacios de indentación (no necesariamente un carácter de tabulación literal — depende de la configuración).
- **Soft wrap (envoltura suave):** cuando una línea de texto es muy larga, el editor la "envuelve" visualmente a la siguiente línea **sin insertar un salto de línea real** — sigue siendo, técnicamente, la misma línea/párrafo. Es solo una cuestión de visualización, no de contenido real del archivo.

### Vista previa  antes de confirmar

Al editar, puedes hacer clic en **"Preview"** para ver el diff exacto de tus cambios — GitHub muestra las líneas como **eliminadas (rojo)** y **añadidas (verde)**, incluso si técnicamente solo modificaste una palabra dentro de la misma línea (internamente se representa como "borrar línea completa + añadir línea completa nueva").


## 4. Crear subcarpetas (Subfolders)

### Cómo funciona

Al nombrar un nuevo archivo, si escribes:
```
subcarpeta/mi-archivo.txt
```
El símbolo `/` (slash) le indica a GitHub que debe crear una **carpeta** llamada `subcarpeta` y colocar el archivo dentro de ella. Puedes anidar múltiples niveles:
```
subcarpeta/otra-subcarpeta/archivo.txt
```

### Navegación entre carpetas

- **Breadcrumb (migas de pan):** la ruta de navegación en la parte superior te permite subir de nivel haciendo clic en carpetas anteriores de la ruta.
- **Clic en "..." (los dos puntos / carpeta padre):** también te permite subir un nivel.

### Mover un archivo de carpeta (editando la ruta)

Al editar un archivo, puedes **cambiar su ubicación** modificando el nombre/ruta en la parte superior del editor:

| Acción                                   | Sintaxis                                   | Resultado                                   |
|:-----------------------------------------|:-------------------------------------------|:--------------------------------------------|
| Mover a otra subcarpeta                  | Escribir `nueva-carpeta/` antes del nombre | El archivo se reubica dentro de esa carpeta |
| Subir un nivel (salir de una subcarpeta) | Borrar el segmento de ruta con Backspace   | El archivo regresa a la carpeta padre       |
| Subir un nivel usando notación relativa  | Escribir `../` al inicio del nombre        | Sube un nivel en la jerarquía de carpetas   |

> **Consecuencia importante:** si una carpeta se queda **sin ningún archivo dentro** (porque moviste el único archivo que contenía), **esa carpeta se elimina automáticamente**. Git no rastrea carpetas vacías, solo archivos. Esto es coherente con cómo Git modela internamente los directorios: no existen como objetos independientes, solo existen en la medida en que contienen archivos.

---

## 5. Eliminar un archivo

### Pasos

1. Abrir el archivo.
2. Clic en el menú de **"..."** (tres puntos) en la esquina superior derecha — desde ahí también puedes descargar el archivo, saltar a una línea específica, copiar la ruta, activar wrap de texto, o centrar el contenido.
3. Seleccionar **"Delete file"**.
4. **Debes confirmar el commit** para que el borrado sea real.

### Punto crítico para el examen

> GitHub muestra el mensaje "this file has been deleted" **antes** de que el borrado sea efectivo — pero si **cancelas** el commit en ese punto, el archivo **NO se elimina**, sigue existiendo intacto en el repositorio.

Esto refuerza el mismo principio que vimos en toda esta sección: **ninguna acción sobre archivos (crear, editar, eliminar) es definitiva hasta que se confirma (commit)**. Es exactamente el mismo comportamiento que en Git local — la diferencia es que aquí la "zona de staging" está oculta detrás de la interfaz web, pero el principio de fondo es idéntico.