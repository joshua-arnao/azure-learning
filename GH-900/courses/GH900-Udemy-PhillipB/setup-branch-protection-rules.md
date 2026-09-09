# Set Up Branch Protection Rules

## ¿Qué resuelve?
Por defecto, CUALQUIER rama (incluida `main`) NO está protegida: cualquiera con permiso de escritura puede hacer force-push o borrar la rama directamente. Branch Protection Rules evita que le pasen "cosas no deseadas" a una rama crítica.

## Dos formas de llegar a configurarlo
1. Desde la vista de ramas → botón "Protect this branch"
2. Settings del repo → menú izquierdo → **Rules** → **Rulesets** → **New branch ruleset**

## Crear un Ruleset — pasos base
1. Ponerle un **nombre** al ruleset
2. Por defecto se crea **Disabled** (inactivo), hay que cambiarlo a **Active** para que realmente aplique

## Bypass list (excepciones)
Se pueden excluir roles, equipos o apps específicas, a ellos el ruleset NO les aplicará. Botón **"Add bypass"**.

## Target branches (a qué ramas aplica)
Botón **"Add target"**, con opciones:
- Include default branch (tu rama principal, ej. `main`)
- Include all branches
- Include/Exclude por **patrón** (wildcard):

| Patrón | A qué apunta |
|:---|:---|
| `*dev*` | Cualquier rama que contenga "dev" en el nombre |
| `prod/*` | Ramas que empiecen con "prod/" seguido de cualquier cosa (SIN incluir más barras `/`) |

> El asterisco (`*`) = cualquier cantidad de caracteres, EXCEPTO barras `/`.

## Prioridad cuando varias reglas afectan la misma rama
Orden de desempate:
1. La regla que menciona la rama **específica por nombre** gana sobre una que la alcanza por patrón (ej. `develop` explícito le gana a `*dev*`)
2. Si siguen empatadas → gana el ruleset **creado primero**

## Reglas disponibles para aplicar

| Regla | Qué hace |
|:-|:---|
| Restrict creations/updates/deletions | Solo quien tenga permiso de bypass puede crear/actualizar/borrar esas ramas |
| Require linear history | Bloquea merge commits — obliga a usar **squash merge** o **rebase merge** (el repo debe tener esas opciones habilitadas) |
| Require deployments to succeed | Exige que el deploy a un ambiente (ej. staging) sea exitoso ANTES de poder mergear a la rama por defecto. Se especifica qué ambientes cuentan |
| Require signed commits | Exige firma electrónica en los commits |
| Require a pull request before merging | Ver detalle abajo ↓ |
| Require status checks to pass | Exige que los checks (CI/CD, tests) pasen antes de mergear |
| Require branches to be up to date | La rama debe estar actualizada con la base antes de mergear |
| Block force pushes | Bloquea force-push directo |
| Require code scanning results | Exige resultados de escaneo de código de herramientas externas (ej. CodeQL) |

## Detalle: "Require a pull request before merging"
Sub-opciones configurables:
- **Número de aprobaciones requeridas**: de 0 a 10
- **Dismiss stale reviews**: si al subir nuevos commits se deben descartar las aprobaciones previas (obliga a re-revisar)
- **Require review from Code Owners**: los dueños del código definidos deben aprobar
- **Require approval of the most recent push**: alguien DISTINTO a quien hizo el último push debe aprobar (evita auto-aprobación)
- **Require conversation resolution**: todos los comentarios/hilos deben quedar resueltos antes de poder mergear
- **Require Copilot code review**: Copilot revisa automáticamente cada PR nuevo
- Métodos de merge permitidos: squash / rebase (se elige cuáles se aceptan)

## Confirmación de identidad
Al crear el ruleset, GitHub puede pedir verificación (GitHub Mobile o contraseña) antes de guardar, es una medida extra de seguridad para cambios de esta sensibilidad.

## Gestión de rulesets existentes
- Vista de "Rulesets" → click en el ruleset para **editarlo**
- Click en el `...` (punto) → **Export** o **Delete**

## Resumen en una línea
Un Ruleset define A QUÉ ramas aplica (por nombre exacto o patrón), QUÉ restricciones se activan (PRs obligatorios, checks, firma, bloqueo de force-push, etc.) y QUIÉN queda exento, pero recuerda que nace **Disabled** y no hace nada hasta que lo actives.