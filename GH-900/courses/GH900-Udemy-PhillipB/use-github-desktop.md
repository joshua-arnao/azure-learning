#  Use GitHub Desktop for File Management

---

## 1. ¿Qué es GitHub Desktop?

Aplicación de escritorio (Windows/Mac) que permite gestionar repositorios **sin usar la línea de comandos ni la interfaz web**, trabajando directamente con archivos locales en tu computadora.

| Requisito | Detalle                                          |
|:----------|:-------------------------------------------------|
| Windows   | Windows 10 o superior, 64-bit                    |
| Mac       | macOS 11.0 o superior                            |
| Login     | Con cuenta de github.com **o** GitHub Enterprise |

> **GitHub Enterprise** es un **plan organizacional de pago** (~$21 USD por usuario/mes), diferencia relevante frente a github.com (cuenta individual gratuita/Pro).

### Autorización al iniciar sesión

Al conectar GitHub Desktop con tu cuenta, autorizas acceso a:
- Repositorios **públicos** y **privados**
- Datos de usuario personales
- Archivos de workflow de **GitHub Actions** (usados para automatización)

## 2. Las 4 formas de crear un repositorio local en GitHub Desktop

| Método                      | Qué hace                                                                                |
|:----------------------------|:----------------------------------------------------------------------------------------|
| **Fork**                    | Bifurca un repositorio ajeno a tu cuenta.                                               |
| **Clone**                   | Descarga una copia completa de un repositorio **remoto** existente.                     |
| **Create new repository**   | Crea un repositorio nuevo directamente en tu disco local.                               |
| **Add existing repository** | Vincula una carpeta que ya existe en tu disco (que ya es un repo Git) a GitHub Desktop. |

> Desde la perspectiva de **GitHub Desktop**, tu computadora es el repositorio **local**, y **github.com** es el repositorio **remoto**.

## 3. El flujo de trabajo: Local ↔ Remoto

**Los cambios NO se sincronizan automáticamente entre local y remoto**. Existen 3 pasos separados y explícitos:

```markdown
1. Crear/editar archivo en tu disco (fuera de Git)
         │
         ▼
2. GitHub Desktop detecta el cambio → Commit (mensaje + descripción)
         │  ← en este punto, el cambio SOLO vive en tu repositorio LOCAL
         ▼
3. Push → recién aquí el cambio llega a github.com (remoto)
```

### El camino inverso: cuando el cambio se hace primero en GitHub.com

Si creas un archivo directamente en la interfaz web (github.com), ese cambio existe en el remoto pero **no aparece automáticamente en tu copia local** de GitHub Desktop. Se necesita:

```
Fetch (detecta que hay cambios nuevos en el remoto)
         │
         ▼
Pull (trae esos cambios a tu copia local)
```


## 4. Elementos clave de la interfaz de GitHub Desktop

| Elemento                                 | Qué muestra/permite                                                                   |
|:-----------------------------------------|:--------------------------------------------------------------------------------------|
| **Panel de cambios (izquierda)**         | Lista de archivos modificados, nuevos o eliminados, con el diff visual de cada cambio |
| **Repositorio y rama actual (arriba)**   | Puedes cambiar de repositorio o de rama activa                                        |
| **Pull requests**                        | Visibilidad de PRs asociados al repo actual                                           |
| **Última vez que se hizo fetch**         | Indicador de cuándo se sincronizó por última vez con el remoto                        |
| **Historial de commits**                 | Registro de confirmaciones ya realizadas                                              |
| **Abrir en editor externo**              | Ej. abrir el repo directamente en Visual Studio Code                                  |
| **Mostrar en el explorador de archivos** | Abre la carpeta local del repo en el Explorador de Windows / Finder                   |
| **Ver en GitHub**                        | Atajo directo a la versión web del repositorio                                        |

## 5. Commit en GitHub Desktop — estructura del mensaje

Igual que en la web, cada commit necesita:
- **Resumen (summary):** obligatorio — sin él, no puedes confirmar el commit.
- **Descripción (description):** opcional, para dar contexto adicional.

> Puedes agrupar **múltiples archivos modificados** (ej. uno editado + uno eliminado) en un **solo commit**, tal como vimos también en la web.
