# Adding a CODEOWNERS File


## 1. El problema que resuelve CODEOWNERS

Hacer un PR hay que agregar un reviewer esta es una acción **manual** depende de que quien crea el PR se acuerde de asignar a alguien. **¿Qué pasa si quieres *exigir* automáticamente** que ciertas personas revisen ciertos archivos, sin depender de que alguien lo recuerde?

**La solución**: un archivo especial llamado **CODEOWNERS**, que asigna reviewers **automáticamente** según qué archivos/carpetas fueron modificados en el PR.

## 2. Dónde se puede colocar el archivo CODEOWNERS

Hay **3 ubicaciones válidas**, y GitHub las evalúa en este **orden de prioridad**:

| Prioridad  | Ubicación                        |
|:----------:|:---------------------------------|
|     1      | Carpeta `.github/`               |
|     2      | Carpeta **raíz** del repositorio |
|     3      | Carpeta `docs/`                  |

> **Regla clave:** si existen **varios archivos CODEOWNERS** en distintas ubicaciones al mismo tiempo, **GitHub solo usa el primero según este orden**, no los combina ni los suma.

### Restricción de tamaño

El archivo CODEOWNERS debe pesar **menos de 3 MB**.

## 3. Sintaxis del archivo — Patrones de rutas

El formato usa **patrones tipo `.gitignore`** para indicar qué archivos le pertenecen a quién.

| Patrón      | Qué cubre                                                                                                                              |
|:------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| `*`         | **Todos los archivos** de la carpeta raíz y **todas las subcarpetas** (todo el repo)                                                   |
| `*.js`      | Todos los archivos con extensión `.js`, en la raíz **y en todas las subcarpetas**                                                      |
| `carpeta/*` | Todos los archivos **dentro de esa carpeta específica** — **NO incluye subcarpetas**                                                   |
| `/docs/*`   | Todos los archivos dentro de `docs/` **y también sus subcarpetas** (la barra final tiene un comportamiento distinto al de `carpeta/*`) |

### Ejemplo

```
*           @philip       → Philip revisa TODO
*.js        @jane         → Jane revisa todos los .js (raíz + subcarpetas)
kevin-folder/*  @kevin    → Kevin revisa solo los archivos DIRECTOS de esa carpeta
/docs/*     @susan        → Susan revisa docs/ y sus subcarpetas
```

## 4. Regla de resolución cuando varias líneas coinciden con el mismo archivo

Si un archivo (ej. `docs/mi-archivo.js`) coincide con **varias reglas de revisión a la vez** (con `*`, `*.js`, y `/docs/*`), **¿se agregan los 4 revisores?**

**Respuesta: NO.** Cuando varios patrones coinciden con el mismo archivo, **gana el ÚLTIMO patrón que coincide** en el archivo (no todos se suman, no gana el primero — gana el **más específico/último en orden de aparición**).


## 5. Formatos válidos para nombrar a un revisor

| Formato                     | Sintaxis                                | Ejemplo                 |
|:----------------------------|:----------------------------------------|:------------------------|
| **Nombre de usuario**       | `@usuario`                              | `@kevin`                |
| **Nombre de equipo (team)** | `@organizacion/equipo`                  | `@nttdata/backend-team` |
| **Correo electrónico**      | `usuario@dominio.com` (sin @ al inicio) | `kevin@midata.com`      |

> **Restricción importante:** el formato de **correo electrónico NO funciona con cuentas de usuario gestionadas (managed user accounts)**, es decir, cuentas donde una organización controla los privilegios del usuario. En esos casos, se debe usar el formato `@usuario`.


## 6. Múltiples revisores en una misma línea

Se pueden asignar **varios revisores a la misma regla**, separados por coma y espacio:

```
*.js   @jane, @philip
```

**Pregunta clave:** si hay 2 revisores en la misma línea, ¿se necesitan **2 aprobaciones**?

**Respuesta: NO.** Basta con que **UNO** de los revisores listados apruebe, no se requiere que todos aprueben.

## 7. Límite total de reviewers

Al igual que vimos en la sección anterior de PRs, el límite sigue siendo **hasta 15 revisores** en total — CODEOWNERS no cambia ese tope, solo automatiza cómo se agregan algunos de ellos.

## 8. Riesgo de seguridad: proteger el propio archivo CODEOWNERS

**Pregunta clave y contraintuitiva del video:** ¿qué pasa si alguien **edita el propio archivo CODEOWNERS** para convertirse en su propio revisor automático?

**Respuesta: funciona — se convertiría efectivamente en el revisor automático de ese archivo**, a menos que tú lo hayas prevenido.

**La medida de seguridad recomendada:** **agregar una regla específica que asigne CODEOWNERS como reviewer de sí mismo**, para que cualquier cambio al archivo también dispare revisión obligatoria — evitando que alguien lo modifique sin autorización para auto-asignarse control.