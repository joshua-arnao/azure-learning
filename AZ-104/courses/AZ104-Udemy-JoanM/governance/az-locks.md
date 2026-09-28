# Locks

Protegen los recursos de Azure evitando su eliminación accidental o modificacióm

## Tipos
- Read-only: bloquea modificaciones
- Deleate: Bloquea elimincaiones

## Asignación
Se puede aplicar a nivel de recursos, grupo de recursos o suscripción.

## Jerarquía de aplicación
- Puedes configurar un Lock en un recurso específico, o un grupo de recursos o a una inclusión completa.
- Si un grupo de recursos tiene un Lock y se intenta eliminar o modificar cualquier recurso dentro de ese grupo, la operación será bloqueada.

