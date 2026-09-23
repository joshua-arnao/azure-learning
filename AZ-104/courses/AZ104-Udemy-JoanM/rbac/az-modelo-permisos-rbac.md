# AZURE RBAC ES UN MODELO DE PERMISOS
Al asignar un **rol**, el usuaario/grupo/aplicación **obtiene permisos para realizar acciones específicas**
Azure RBAC uso dos conjuntos en cada rol:

- Actions -> Operaciones permitidas
- NotActions -> Operaciones que se niegam

> Permisos efectivos = Actions - NotActions
