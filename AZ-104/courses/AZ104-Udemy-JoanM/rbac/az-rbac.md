# RBAC - Control de acceso basado en role 
Admistra accesos especificos a los recursos de Azure, asignar roles a usuario, grupos o aplicaciones. Define **qué acciones se pueden realizar**.

## Visión general
- Los roles se asignan en distintos niveles jérarquicos.
- Los **permisos se hereda** de niveles superiores a inferiores.
- Un rol definido en un nivel superior **aplica a todos los niveles** inferiores.

## Que se puede hacer con RBAC
- Define quién puede hacer qué en qué recursos
- Se aplica a => usuarios, grupos y aplicaciones

## Como funciona
Una asiganción de rol define **quién** puede hacer **qué** sobre qué recurso

### Entidad de seguridad (Quién) 
Es la entidad a la que se le asigna un rol:

- Usuario -> Persona individula
- Grupo -> Conjunto de usuarios
- Entidad de servicio -> Aplicaciones o servicios

### Definición del rol (qué)
- Conjunto de permisos
- Determinan qué acciones puede realizar la entindad de seguridad
- Roles más comunes en Azure:
	- **Propietario** -> Acceso total
	- **Colaborador** -> Crear y administrar recursos existentes
	- **Lector** -> Ver recursos existentes
	- **Adminsitrador de acceso de usuario** -> Gestiona permisos

### Ambito (Dónde)
- Nivel al que se aplica el acceso
- Define en qué parte de Azure se aplican los permisos:
	- **Grupo de adminsitración** -> Nivel más alto
	- **Suscripción** -> Contiene grupos de recursos y recursos
	- **Grupo de recursos** -> Conjunto de recursos relacionados
	- **Recurso individual** -> VM, BD o app

> Important: Los ámbitos son jerárquicos si das acceso en un nievel superior, se hereda a los niveles inferiores.

### Asignación de roles en Azure RBAC
Proceso de unir:
- Entidad de seguridad
- Definción del rol
- Ámbito

> Aplicar el principio del mínimo privilegio
