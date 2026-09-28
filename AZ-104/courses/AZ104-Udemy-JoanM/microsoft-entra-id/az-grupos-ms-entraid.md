# GRUPOS EN MICROSOFT ENTRA ID
Los grupos ayyudas a **orgnizar usuarios**  y permisos, permite poder asignar **permisos a todos los miembros** a la vez

## Tipos de grupos en Microsoft Entra ID

## Grupos de seguridad
- Comunes Azure Entra
- Controla acceso a recursos compartidos
- Asignan permisos según políticas de seguridad
- Pueden incluir usuarios y dispositivos
- Requieren adminsitración por un admin de Entra ID

## Grupos de Microsft 365
- Usados por colaboración y productividad
- Proporcionan acceso a:
	- Buzón y calendario compartido
	- Archivos y sitios de SharePoint
	- Teams y otras apps M365
- permiten usuarios externos (colaboración B2B)

## TIPOS DE PERTENENCIA
### Asignado (Assigned)
- Miembros agregados y gestionados manualmente
- Disponible en todas las ediciones (Free, P1, ...)
- útil cuando el número de usuario es reducido o se require control manual

### Dinámico (Dynamic)
- Miembros agregados automáticamente según **reglas basadas en atributos** (departamento, cargo, ubicación.
- Requiere licencia Premium P1 o P2
- Se aplica a grupos de seguridad o Microsoft 365
- La membresía se **actualiza automáticamente** cuando los atributos cambian
- Un grupo dinámico no admite miembros asignados manualmente.
