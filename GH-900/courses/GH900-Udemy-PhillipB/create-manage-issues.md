# Create and Manage Issues

---

## 1. ¿Qué es un Issue?

Los **Issues** permiten discutir elementos de trabajo: reportar errores (bugs), sugerir nuevas funciones/ideas, o recopilar opiniones. Se pueden ampliar agregando **sub-issues** (subtemas).

## 2. Permisos necesarios

| Acción                                | Permiso requerido                                                                   |
|:--------------------------------------|:------------------------------------------------------------------------------------|
| **Crear un issue**                    | Acceso de **lectura** es suficiente (no necesitas escritura)                        |
| **Que el repositorio permita issues** | La función **Issues debe estar habilitada** en Settings → Features del repositorio  |

## 3. Formas de crear un Issue

| Método                         | Cómo                                                                                        |
|:-------------------------------|:--------------------------------------------------------------------------------------------|
| **Directo**                    | Pestaña "Issues" → "New Issue"                                                              |
| **Desde un comentario**        | Clic en "..." junto a un comentario → "Reference in new issue" → crear                      |
| **Desde una Discussion**       | Se genera un issue vinculado en la barra lateral derecha de la discusión                    |
| **Desde un Project (tablero)** | Clic en el "+" al final de una columna/tabla → "Create new issue"                           |
| **Vía Copilot Chat**           | Disponible tanto en GitHub web como en GitHub mobile                                        |
| **Vía GitHub Mobile**          | App móvil, generalmente usada para lectura, pero también permite crear issues y discussions |

## 4. Issue Templates

Si el repositorio tiene plantillas configuradas, puedes usarlas para **pre-rellenar** título y descripción con una estructura estándar (útil para reportes de bugs consistentes, por ejemplo).

## 5. Interacciones sobre un Issue ya creado

Desde el menú "..." junto al issue puedes:
- Copiar enlace directo
- Citar en una respuesta
- Editar
- Reportar contenido (report content)
  También puedes:
- Marcar/desmarcar ítems del task list directamente
- Reaccionar con emojis (cara sonriente, etc.)
---

## 6. Sub-Issues (relación padre-hijo entre issues)

**Cómo crear la relación:**
- Al crear un issue nuevo, puedes asignarle un **issue padre** directamente.
- Desde un issue existente con task list, puedes convertir un ítem de la lista en **sub-issue** haciendo clic en "..." junto a esa tarea.
- También existe el botón directo **"Create sub-issue"**, y puedes **añadir un issue ya existente** como sub-issue (no solo crear uno nuevo).

### Límites

| Límite                           | Cantidad                                                  |
|:---------------------------------|:----------------------------------------------------------|
| **Sub-issues máximos por issue** | **100**                                                   |
| **Niveles de anidación máximos** | **8 niveles** (un sub-issue con sub-issue, hasta 8 veces) |

**Permiso necesario para añadir sub-issues:** al menos permisos de **Triage** en el repositorio.


## 7. Cerrar un Issue

### Razones de cierre disponibles

| Categoría             | Opciones                                       |
|:----------------------|:-----------------------------------------------|
| **Completado (Done)** | Completed / Fixed / Resolved                   |
| **No planeado**       | Won't fix / Can't reproduce / Stale (obsoleto) |
| **Duplicado**         | Duplicate (de otro issue específico)           |

### ¿Quién puede cerrar un issue?

Puedes cerrar issues que **tú abriste**, pero también los que **abrió otra persona**, si cumples alguna de estas condiciones:
- Eres **propietario (owner)** del repositorio
- Eres **colaborador** en un repositorio de cuenta personal
- Tienes al menos permisos de **Triage** en un repositorio de organización

### Cierre automático

Un issue también se cierra automáticamente si está **vinculado a un Pull Request** y ese PR se fusiona (merge).

## 8. Eliminar un Issue

| ¿Quién puede?                                 | Condición             |
|:----------------------------------------------|:----------------------|
| Propietario del repositorio                   | Repos personales      |
| Administrador del repositorio de organización | Repos de organización |

**Consecuencia:** al eliminar un issue, la página del issue muestra un error de "página no encontrada" — a diferencia de cerrar, **eliminar es irreversible** y quita el issue por completo (no se puede reabrir porque ya no existe).

## 9. Pin (Anclar) un Issue

| Detalle                                       | Valor                                                            |
|:----------------------------------------------|:-----------------------------------------------------------------|
| **Máximo de issues anclados por repositorio** | **3**                                                            |
| **Permiso necesario**                         | Al menos acceso de **escritura**                                 |
| **Efecto**                                    | El issue anclado aparece **encima** de la lista normal de issues |

## 10. Otras acciones sobre un Issue

| Acción                           | Detalle                                                                                      |
|:---------------------------------|:---------------------------------------------------------------------------------------------|
| **Lock conversation (bloquear)** | Usuarios sin acceso de escritura ya no pueden comentar. Se puede desbloquear después.        |
| **Transfer (transferir)**        | Mover el issue a otro repositorio — requiere permisos de **escritura en ambos repositorios** |
| **Duplicate**                    | Copiar el issue (crear uno nuevo con el mismo contenido)                                     |
| **Subscribe / Unsubscribe**      | Activar o desactivar notificaciones sobre ese issue específico                               |

## Resumen visual del ciclo de vida de un Issue

```
Crear Issue (lectura es suficiente + Issues habilitado en el repo)
        │
        ├─ Con plantilla (opcional)
        ├─ Con Task List (checkboxes)
        ├─ Con Labels / Assignees / Projects / Milestones
        │
        ▼
   Issue abierto ── puede tener hasta 100 sub-issues, 8 niveles de anidación
        │
        ├─ Comentarios / Reacciones
        ├─ Pin (máx. 3 por repo, requiere write access)
        ├─ Lock/Unlock conversación
        ├─ Transfer a otro repo (requiere write en ambos)
        │
        ▼
   Cerrar Issue
        ├─ Completed / Fixed / Resolved
        ├─ Won't fix / Can't reproduce / Stale
        ├─ Duplicate
        └─ Automático (si vinculado a PR que se fusiona)
        │
        ▼
   (Opcional) Delete Issue — irreversible, solo owner/admin
```
