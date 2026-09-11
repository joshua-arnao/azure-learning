# Privacy, Security, and Administration — Member Roles in Detail


```
Read → Triage → Write → Maintain → Admin
(cada flecha = "todo lo anterior + esto nuevo")
```


## 1. Read (Lectura) — el nivel base

**Idea central:** ver, participar en discusión, y hacer cosas que no modifican el repositorio principal.

| Puede hacer |
|---|
| Pull, clone o fork de los repos asignados |
| Enviar pull requests **desde tus propios forks** |
| Enviar reviews sobre PRs (comentar/opinar) |
| Editar/eliminar **tus propios** comentarios |
| Abrir issues; cerrar o reabrir **solo los que tú abriste** |
| Ver releases publicados, ver Actions y workflow runs |
| Editar wikis **en repos públicos** |
| Reportar contenido abusivo/spam |
| Ver e instalar packages |
| Ver reglas del repositorio (rulesets) |
| Crear discussions nuevas y comentar en existentes |
| Crear Codespaces (públicos o privados) |
| Ver alertas de code scanning en PRs |


## 2. Triage — gestión de Issues y PRs, sin tocar código

**Lo nuevo respecto a Read:** ahora puedes gestionar el trabajo de **cualquiera**, no solo el tuyo — pero **sigues sin poder escribir código**.

| Puede hacer (adicional) |
|---|
| Aplicar o quitar labels |
| Cerrar, reabrir y **asignar** cualquier issue o PR (no solo los propios) |
| Aplicar milestones |
| Marcar issues/PRs como duplicados |
| Solicitar reviews de PR |
| Ocultar comentarios **de cualquier persona** |
| Mover discussions a otra categoría |
| Bloquear/desbloquear discussions individuales |
| Convertir issues en discussions, y eliminar una discussion |

> ** Triage = **"control administrativo sobre la conversación y organización del trabajo, sin acceso de escritura al código."**

## 3. Write — puede hacer push

**Lo nuevo respecto a Triage:** por fin puedes **escribir código** (push) a los repos asignados, y ganas permisos operativos importantes sobre PRs.

| Puede hacer (adicional) |
|---|
| Editar wikis en repos **privados** (Read solo permitía en públicos) |
| Crear, editar, eliminar **labels y milestones** (Triage solo podía aplicarlos, no crearlos) |
| **Aprobar o solicitar cambios** en un PR |
| Aplicar suggested changes en PRs (con revisiones obligatorias) |
| Activar/desactivar **auto-merge** en un PR |
| **Fusionar (merge) un PR** |
| Marcar un draft PR como "ready for review" y viceversa |
| **Push/escribir** en los repos asignados |
| Editar/eliminar comentarios **de cualquier persona** en commits, PRs e issues |
| Bloquear conversaciones, transferir issues |
| Actuar como **Code Owner designado** de un repositorio |
| Crear status checks para Actions |
| Crear, editar, ejecutar, re-ejecutar y cancelar **workflows de Actions** |
| Crear/actualizar/eliminar Actions secrets y variables vía REST API |
| Crear y editar releases, ver draft releases |
| Publicar packages |
| **Definir Code Owners** de un repositorio (el archivo CODEOWNERS que vimos antes) |
| Renombrar ramas — **excepto la rama por defecto** |
| Crear/editar categorías de discussions, transferir una discussion, gestionar discussions ancladas |
| **Alertas de Dependabot:** recibir alertas de dependencias inseguras, descartar la lista de alertas |
| **Code scanning / secret scanning:** descartar y borrar alertas de code scanning, ver y descartar alertas de secret scanning |

> **Punto de examen clave:** Write es el primer nivel donde puedes **fusionar PRs, hacer push, y ser Code Owner** — es el salto de "solo gestionar conversación" a "modificar el código real".

## 4. Maintain — gestión amplia, sin acciones destructivas/sensibles

**Lo nuevo respecto a Write:** control sobre la **configuración general** del repositorio, pero **sin** poder hacer acciones sensibles o destructivas (esas son exclusivas de Admin).

| Puede hacer (adicional) |
|---|
| Editar la **descripción** del repositorio |
| Gestionar **topics** (etiquetas temáticas del repo) |
| Habilitar wikis y **restringir quién puede editarlas** |
| Configurar opciones de **merge de PRs** (ej. qué métodos de merge se permiten) |
| Configurar la fuente de publicación de **GitHub Pages** |
| Ver la configuración de **exclusión de contenido para Copilot** |
| **Push a ramas protegidas** — *nota: esto no aplica a "rulesets", que usan un modelo de bypass distinto* |
| Crear/editar **social preview cards** del repositorio |
| Limitar interacciones en un repositorio (ej. modo restringido temporal) |
| Habilitar GitHub Discussions en el repo |

> **Frase clave para el examen:** Maintain = **"puede configurar cómo se comporta el repositorio, pero no puede destruirlo, transferirlo, ni tocar su seguridad de fondo."**


## 5. Admin — control total

**Lo nuevo respecto a Maintain:** todo lo que falta, especialmente **acciones destructivas, de seguridad y de gobernanza**.

| Puede hacer (adicional) |
|---|
| Gestionar acceso individual, de equipos y de colaboradores externos |
| Crear/actualizar/eliminar Actions secrets y variables desde **github.com** (no solo vía API, como Write) |
| **Eliminar y restaurar packages** |
| Gestionar **branch protection rules** y **rulesets** del repositorio |
| **Fusionar PRs en ramas protegidas, incluso sin aprobaciones** (salta las reglas) |
| **Eliminar un issue** |
| Añadir el repositorio a un equipo |
| Gestionar acceso de colaboradores externos |
| **Cambiar la visibilidad** del repositorio (public/private/internal) |
| **Convertir el repo en template** (recordando la sección de Repository Templates) |
| Cambiar la configuración general del repositorio |
| Gestionar acceso de equipos y colaboradores |
| **Editar o renombrar la rama por defecto** (la única acción de renombrado que Write no podía hacer) |
| Gestionar **webhooks** y **deploy keys** |
| Gestionar política de forking |
| **Transferir el repositorio** dentro o fuera de la organización |
| **Archivar** repositorios |
| Mostrar botón de "Sponsor" |
| Crear referencias de autolink a recursos externos (ej. Jira, Zendesk) |
| Editar **custom properties** del repositorio |
| Crear **security advisories** |
| Activar el **dependency graph** en un repo privado |

> **Frase clave para el examen:** Admin = **"todo lo anterior, más cualquier acción que sea irreversible, de seguridad crítica, o que cambie la identidad/gobernanza del repositorio (visibilidad, transferencia, eliminación, ramas protegidas)."**

## Punto clave para el examen

Si una pregunta describe una acción específica y te pide identificar el **rol mínimo necesario**, usa esta lógica:

1. **¿Solo necesita ver o comentar sobre su propio trabajo?** → Read
2. **¿Necesita organizar/etiquetar/cerrar el trabajo de otros, sin tocar código?** → Triage
3. **¿Necesita escribir código, aprobar o fusionar PRs?** → Write
4. **¿Necesita cambiar configuración general del repo (no destructiva)?** → Maintain
5. **¿Implica eliminar, transferir, cambiar visibilidad, o saltarse protecciones?** → Admin
