# Git — Comandos Esenciales (Guía GH-900)

---

## 1. Configuración y Setup

| Comando                                          | Qué hace                                                                         |
|:-------------------------------------------------|:---------------------------------------------------------------------------------|
| `git --version`                                  | Muestra la versión de Git instalada.                                             |
| `git help` / `git -h`                            | Ayuda general de Git.                                                            |
| `git help [comando]`                             | Documentación de un comando específico.                                          |
| `git config --global user.name "[name]"`         | Registra el nombre del autor para tus commits (global).                          |
| `git config --global user.email "[email]"`       | Registra el correo del autor para tus commits (global).                          |
| `git config user.name` / `git config user.email` | Consulta el usuario/correo configurado.                                          |
| `git config --global --list`                     | Lista toda la configuración global activa.                                       |
| `git config --global -e`                         | Abre el archivo de configuración global para editarlo directamente.              |
| `git config --global init.defaultBranch <name>`  | Define el nombre de rama por defecto (ej. `main`) para nuevos repos.             |
| `git init`                                       | Inicializa un repositorio Git vacío, creando la carpeta oculta `.git`.           |
| `git clone <url>`                                | Copia un repositorio remoto completo (con todo su historial) a tu máquina local. |

---

## 2. Inspección de Estado (Seguimiento)

| Comando | Qué hace |
|---|---|
| `git status` | Diagnóstico de las 3 zonas: qué está *modified*, *staged* y *untracked*. Es tu punto de partida antes de cualquier decisión. |
| `git log` | Bitácora cronológica de commits: hash, autor, fecha, mensaje. Solo muestra commits **alcanzables** desde HEAD (ver sección 7). |
| `git log --oneline` | Igual que `git log`, pero comprimido a una línea por commit (hash corto + mensaje). |
| `git log --oneline --merges` | Filtra el historial para ver únicamente los commits de fusión (merges). |
| `git diff` | Muestra las diferencias línea por línea entre Working Directory y Staging Area (cambios *unstaged*). |
| `git diff --staged` | Muestra las diferencias entre Staging Area y el último commit (cambios ya *staged*, pendientes de commit). |
| `git blame <archivo>` | Desglosa un archivo línea por línea, indicando autor y commit responsable de cada línea. |
| `git show <commit_id>` | Muestra el contenido completo y metadata de un commit específico. Ideal para inspeccionar hashes recuperados con `git reflog`. |

---

## 3. Las 3 Zonas de Git

```
------------------                  ----------------                   -------------
|Working Directory|  --(git add)--> | Staging Area | --(git commit)--> | Repository |
|   (Modified)    |                 |   (Staged)   |                   | (Committed)|
-------------------                 ----------------                   --------------
```

| Zona                     | Contiene                                                         |
|:-------------------------|:-----------------------------------------------------------------|
| **Working Directory**    | Archivos tal cual los editas en tu carpeta local.                |
| **Staging Area / Index** | Sala de espera antes del commit — lo que marcaste con `git add`. |
| **Repository (.git)**    | Historial permanente — lo que confirmaste con `git commit`.      |

### Estados de archivo: 

`Untracked` (nuevo, sin seguimiento) → `Modified` (editado, unstaged) → `Staged` (preparado) → `Committed` (confirmado).

---

## 4. Preparar y Confirmar Cambios (Staging & Commit)

| Comando                         | Qué hace |
|---------------------------------|---|
| `git add <archivo1> <archivo2>` | Mueve archivos específicos de *Modified/Untracked* a *Staged*. |
| `git add .`                     | Mueve **todos** los cambios (modified + untracked) al Staging Area. |
| `git add *.html`                | Agrega solo los archivos que coincidan con el patrón (ej. todos los `.html`). |
| `git add <carpeta>/*`           | Agrega todos los archivos dentro de una carpeta específica. |
| `git commit -m "[mensaje]"`     | Confirma lo que está en Staging Area como un nuevo commit permanente en el Repository. |
| `git rm <archivo>`              | Elimina un archivo |rastreado, tanto del disco como del historial futuro. |

---

## 5. Restaurar y Limpiar el Working Directory

| Comando | Qué hace | ¿Destructivo? |
|---|---|---|
| `git restore .` / `git checkout -- .` | Descarta cambios *unstaged* en archivos ya rastreados (tracked), regresándolos a la última versión confirmada. No afecta archivos *untracked*. | ⚠️ Sí — pierdes ediciones no confirmadas |
| `git clean -fd` | Elimina de forma forzada (`-f`) y recursiva (`-d`) archivos y carpetas **untracked**. | ⚠️ Sí |
| `git clean -fx` | Igual que `-fd`, pero además elimina archivos ignorados por `.gitignore` (ej. `.env`, `node_modules`). | ⚠️⚠️ Muy destructivo |
| `git stash` | Guarda temporalmente todos los cambios pendientes (staged + unstaged) en una pila oculta, dejando el Working Directory limpio. | No — es reversible |
| `git stash pop` | Restituye el último stash guardado al Working Directory actual. | No |

---

## 6. Reset — Los 3 Modos (comparativa completa)

`git reset` mueve el puntero de la rama actual hacia un commit específico. Lo que cambia entre modos es **hasta dónde limpia** las otras 2 zonas.

| Comando | Rama / HEAD | Staging Area | Working Directory |
|---|---|---|---|
| `git reset` (sin ID, equivale a `reset HEAD`) | No se mueve | Se vacía (unstage todo) | Recibe lo desmarcado, queda como *modified* |
| `git reset --mixed <hash>` *(default si no pones flag)* | Se mueve a `<hash>` | Se vacía | Recibe la diferencia como *modified* (no staged) |
| `git reset --soft <hash>` | Se mueve a `<hash>` | **Conserva** la diferencia, como *staged* | No se toca |
| `git reset --hard <hash>` | Se mueve a `<hash>` | Se vacía | **Se sobrescribe por completo** (se pierde todo lo no confirmado) |

**Termómetro de "profundidad de limpieza":** `--soft` (solo mueve el marcador) → `--mixed` (+ limpia Staging) → `--hard` (+ sobrescribe Working Directory).

**Dato clave:** `reset` nunca borra el commit de inmediato — solo mueve el puntero de la rama. El commit "abandonado" queda huérfano pero recuperable vía `git reflog` hasta que el garbage collector lo limpie (por defecto 30–90 días).

---

## 7. HEAD y Recuperación (Reflog)

| Comando | Qué hace |
|---|---|
| `git reflog` | Bitácora **local** de todos los movimientos de HEAD (commits, resets, checkouts), sin importar si el commit sigue siendo alcanzable desde una rama. Es tu red de seguridad definitiva. |
| `git reset --soft/--hard <hash-huérfano>` | Permite "resucitar" un commit huérfano encontrado en el reflog, apuntando la rama directamente a su hash. |
| `git cherry-pick <commit_id>` | Extrae un commit aislado (de cualquier rama, incluso huérfano) y lo aplica como commit nuevo sobre tu rama actual. |

**Conceptos clave:**
- **HEAD** es un puntero que normalmente apunta al *nombre de la rama actual*, y esa rama apunta al último commit. No apunta directo a un commit — hay una capa de indirección.
- **`git log`** solo muestra commits *alcanzables*: caminando hacia atrás desde HEAD, siguiendo la cadena de padres (parent commits). Un commit sin nada apuntándolo (ni rama, ni tag) **no aparece**, aunque siga existiendo en `.git/objects`.
- **Detached HEAD**: ocurre cuando HEAD apunta directamente a un commit (no a una rama). Si confirmas ahí, ese commit queda sin protección de ninguna rama — puede perderse si no creas una rama nueva (`git branch <nombre>`) antes de moverte.

---

## 8. Branching y Merging

| Comando | Qué hace |
|---|---|
| `git branch` | Lista las ramas locales. |
| `git branch -r` | Lista las ramas remotas. |
| `git branch -a` | Lista todas las ramas (locales + remotas). |
| `git branch <nombre>` | Crea una nueva rama partiendo de la posición actual (no cambia a ella). |
| `git branch -d <nombre>` | Borra una rama de forma segura (Git no deja si tiene cambios sin fusionar). |
| `git branch -D <nombre>` | Borra una rama a la fuerza, sin validar si está fusionada. |
| `git branch -m <nuevo-nombre>` | Renombra la rama en la que estás parado. |
| `git branch -m <viejo> <nuevo>` | Renombra una rama específica (sin necesidad de estar en ella). |
| `git branch --merged` | Lista ramas ya integradas (fusionadas) en la rama actual. |
| `git branch --no-merged` | Lista ramas con commits que **aún no** se han fusionado a la rama actual. |
| `git branch -vv` | Detalle de ramas locales: último commit y estado respecto al remoto (sincronizada, adelantada, atrasada). |
| `git switch <rama>` | Comando moderno para cambiar de rama (reemplaza a `checkout` para este uso). |
| `git merge <rama>` | Integra el historial de `<rama>` dentro de la rama activa actual. |

### Tabla de flags — `git branch`

| Corta | Larga | Significado | ¿Se puede forzar? |
|---|---|---|---|
| `-d` | `--delete` | Borrar | Sí (`-D`) |
| `-m` | `--move` | Renombrar/Mover | Sí (`-M`) |
| `-a` | `--all` | Todas | No aplica |
| `-r` | `--remotes` | Remotas | No aplica |
| `-v` | `--verbose` | Detalle | No fuerza, duplica detalle (`-vv`) |

**Anatomía de un comando Git:**
```
| programa base | subcomando | flag | argumento/objeto |
|:---------------|:-----------|:-----|:------------------|
| git            | branch     | -d   | feature-login     |
```

---

## 9. Sincronización con Remoto (Sharing & Updating)

| Comando | Qué hace |
|---|---|
| `git remote -v` | Lista los alias y URLs de los repositorios remotos conectados. |
| `git fetch` | Descarga historial y metadata del remoto **sin** fusionar ni sobrescribir nada local. |
| `git pull` | Descarga cambios remotos **y** los fusiona automáticamente (equivale a `fetch` + `merge`). |
| `git push` | Sube tus commits locales confirmados al repositorio remoto. |

---

## 10. Reescritura de Historial (Patching)

| Comando | Qué hace | ¿Reescribe historial? |
|---|---|---|
| `git rebase <rama>` | Reaplica los commits de tu rama actual, uno por uno, sobre la base del último commit de `<rama>` — produce un historial lineal. | Sí |
| `git revert <commit_id>` | Crea un **nuevo commit** que anula los cambios de un commit pasado, sin borrar ni alterar la cronología original. | No — es seguro para historial compartido |
| `git cherry-pick <commit_id>` | Copia un commit aislado de cualquier punto del historial y lo aplica como commit nuevo en tu rama actual. | No |

---

## Notas rápidas para el examen

- `git status` → siempre tu primer diagnóstico antes de decidir cualquier acción.
- `restore`/`checkout --` y `reset --hard` son los comandos con mayor riesgo de **pérdida de trabajo no confirmado** — memorízalos como el grupo "destructivo".
- `git revert` es la alternativa **segura** a `reset` cuando el commit ya fue compartido/pusheado con el equipo (no reescribe historial ajeno).
- `reflog` es local — no se sube al remoto ni se comparte con el equipo.
