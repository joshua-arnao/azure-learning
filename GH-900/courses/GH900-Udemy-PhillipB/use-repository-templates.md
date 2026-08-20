# Use Repository Templates

---

## 1. ¿Qué es un Repository Template?

**El problema que resuelve:** normalmente, al crear un repositorio se empieza desde cero. Pero si quieres que **todos tus proyectos nuevos** partan con una estructura de archivos determinada, por ejemplo, un `CODE_OF_CONDUCT.md`, guías de contribución, una estructura de carpetas específica, repetir eso manualmente cada vez es ineficiente y propenso a inconsistencias.

**La solución:** convertir un repositorio existente en una **plantilla (template)**. Cualquier repositorio nuevo creado "a partir de" esa plantilla **hereda automáticamente** su estructura de archivos y carpetas — sin tener que copiar y pegar nada manualmente.

## 2. Cómo habilitar un repositorio como plantilla

| Paso | Acción                                                                  |
|:-----|:------------------------------------------------------------------------|
| 1    | Se requieren **permisos de administrador** sobre el repositorio.        |
| 2    | Ir a **Settings** del repositorio.                                      |
| 3    | En la pestaña **General**, marcar la casilla **"Template repository"**. |

**Dato clave:** esta opción **no está activada por defecto**, sin haberla marcado antes, el botón "Use this template" simplemente no existe/no aparece en el repositorio.

## 3. Cómo crear un nuevo repositorio a partir de una plantilla

Una vez habilitada la opción de plantilla:

1. En el repositorio (ya convertido en plantilla), aparece el botón **"Use this template"**.
2. Clic en **"Create a new repository"**.
3. Configurar el nuevo repositorio:

| Opción                   | Detalle                                                                                         |
|:-------------------------|:------------------------------------------------------------------------------------------------|
| **Nombre**               | Nombre del nuevo repositorio.                                                                   |
| **Include all branches** | Puedes elegir traer **todas las ramas** de la plantilla, no solo la rama principal por defecto. |
| **Descripción**          | Opcional.                                                                                       |
| **Visibilidad**          | Público o Privado.                                                                              |

4. Clic en **"Create repository"** — GitHub genera el nuevo repo con la estructura heredada (ej. el mismo `README.md` y contenido inicial de la plantilla).

## 4. Qué SÍ y qué NO se copia desde la plantilla

| Se copia                                 | No se copia                                              |
|:-----------------------------------------|:---------------------------------------------------------|
| Archivos y carpetas del repositorio      | **Archivos almacenados en Git LFS** (Large File Storage) |
| Estructura general del proyecto          | —                                                        |
| Todas las ramas (si se marca esa opción) | —                                                        |

**Sobre Git LFS (Large File Storage):** es un almacén especial para archivos pesados, típicamente **muestras de audio, video, datasets y gráficos**. Al crear un repositorio desde una plantilla, **estos archivos NO se incluyen**, es una excepción importante a tener en cuenta si tu plantilla dependía de recursos grandes almacenados ahí.

## 5. Diferencia clave: Template vs Clone vs Fork

Usar una plantilla **NO es lo mismo** que clonar o hacer fork:

| Acción                | ¿Qué genera?                                                                                                | ¿Mantiene conexión/historial con el original?                                        |
|:----------------------|:------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------|
| **Use this template** | Un repositorio **completamente nuevo e independiente**, con la estructura de archivos como punto de partida | ❌ No, empieza con un historial de commits limpio, sin relación con el repo original |
| **Fork**              | Una copia vinculada al repositorio original                                                                 | ✅ Sí, mantiene relación con el "upstream", pensado para contribuir de vuelta        |
| **Clone**             | Una copia local de un repositorio existente                                                                 | ✅ Sí — mismo historial completo, mismo remoto                                       |

**Por qué esto importa:** una plantilla es para **empezar proyectos nuevos con una base estandarizada**, no para colaborar en un proyecto compartido ni para mantener sincronización con el original.