# Collaborate Using GitHub — Fork Repositories

---

## 1. El problema que resuelve el Fork

Editar directamente en la rama principal (`main`) es riesgoso porque **esa rama suele representar producción** la versión final y estable del código. Un cambio ahí puede romper algo para todos.

**La solución en GitHub no es solo "crear una rama"** cuando **no tienes permisos de escritura** sobre el repositorio, la vía es **bifurcar (fork)**: creas tu propia copia del repositorio, haces tus cambios ahí, y luego propones esos cambios de vuelta al original mediante un **Pull Request**.

## 2. Fork vs Clone

|                            | **Fork**                                                                                               | **Clone**                                                             |
|:---------------------------|:-------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------|
| ¿Dónde vive la copia?      | En **GitHub** (nube → nube)                                                                            | En tu **máquina local** (nube → disco)                                |
| Velocidad                  | Más rápido — es una copia servidor a servidor                                                          | Depende del tamaño del repo y tu conexión                             |
| Relación con el original   | Mantiene vínculo con el repositorio **upstream** (original)                                            | Copia independiente, aunque también puede tener un remoto configurado |
| Cómo devuelves cambios     | Vía **Pull Request** hacia el repositorio original                                                     | Vía `push` (si tienes permisos) o también PR si no los tienes         |
| Restricciones de seguridad | **Hereda las restricciones del repositorio upstream** — por eso es preferible en términos de seguridad | No hereda restricciones automáticamente de la misma forma             |

## 3. Reglas sobre quién puede Forkear qué

| Escenario                                          | ¿Se puede?                                                                                                                         |
|:---------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------|
| Forkear un repositorio **público**                 | ✅ Sí                                                                                                                              |
| Forkear un repositorio **privado**                 | ✅ Solo si el propietario lo permite explícitamente                                                                                |
| Forkear a una **organización**                     | ✅ Sí, pero la organización necesita un **plan de pago** — no aplica en el plan gratuito de GitHub                                 |

## 4. Comportamiento y nomenclatura del Fork

- Por defecto, un fork **hereda el mismo nombre** que el repositorio original (upstream).
    - Ej: `philip-do-data/mi-repositorio` → forkeado por Jane → `jane-do-data/mi-repositorio`
- Al crear el fork, puedes elegir **copiar solo la rama principal** (útil si solo te interesa contribuir sobre `main`, sin traer todas las demás ramas).
- Un fork es funcionalmente **un repositorio completo**: puede tener sus propias ramas, colaboradores, Pull Requests, tags/etiquetas — todo igual que cualquier otro repo.

---

## 5. Sincronización entre el Fork y el repositorio original (Upstream)

Con el tiempo, tanto tu fork como el repositorio original pueden avanzar de forma independiente:

```
Repo original (upstream)  ──── nuevo commit ────►  ahora tiene 1 commit que tu fork no tiene
Tu fork                   ──── 2 nuevos commits ──► adelante en 2, pero atrás en 1 respecto al original
```

GitHub muestra este estado explícitamente: *"X commits ahead, Y commits behind"*.

**Opción de sincronización — "Sync fork" / sincronizar:**
- Actualiza tu fork trayendo los cambios nuevos del repositorio original.
- ⚠️ **Advertencia importante:** sincronizar puede **descartar tus commits recientes** si generan conflicto con la actualización, por eso no es una acción automática ni "gratis", hay que evaluarla antes de ejecutarla.

## 6. Flujo típico cuando no tienes permisos de escritura

Si intentas crear/editar un archivo directamente en un repositorio donde no tienes acceso de escritura, **GitHub te lo impide** y te ofrece automáticamente la alternativa:

```
Intento de editar/crear archivo
         │
         ▼
GitHub: "Necesitas hacer un fork para proponer cambios"
         │
         ▼
Se crea automáticamente un fork en tu cuenta personal
         │
         ▼
Editas ahí libremente (con permisos completos sobre tu copia)
         │
         ▼
Pull Request de vuelta al repositorio original
```

---

## 7. Fork desde GitHub Desktop

**Detalle importante:** GitHub Desktop **no tiene una opción directa de "Fork"** en su menú — solo permite **clonar**.

Sin embargo, el flujo se resuelve igual:

1. Clonas el repositorio normalmente (aunque no tengas permisos de escritura).
2. Haces cambios localmente y confirmas (commit).
3. Al intentar hacer **push**, GitHub Desktop detecta que no tienes acceso de escritura y pregunta: *"¿Quieres crear un fork en su lugar?"*
4. Si aceptas, te pregunta el propósito: **contribuir al proyecto padre** o **usarlo como base de un nuevo repositorio propio**.
5. El fork se crea automáticamente (en GitHub, del lado remoto) y puedes hacer push hacia ahí.

## Resumen visual — cuándo usar Fork vs Branch

```
¿Tienes permisos de escritura sobre el repo?
        │
   ┌────┴────┐
  SÍ         NO
   │          │
   ▼          ▼
Crear una   Crear un FORK
BRANCH      (copia en tu cuenta)
   │          │
   ▼          ▼
Pull Request  Pull Request
(mismo repo)  (hacia el repo original/upstream)
```
