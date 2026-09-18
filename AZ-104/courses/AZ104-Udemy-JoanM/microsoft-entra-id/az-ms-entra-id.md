# MICROSOFT ENTRA ID
> Anteriormente Azure Active Directory

Es un servicio de **gestión de identidades en la nube** ofecido por Miscrosoft

Esta construido para trabajar en la nube y ofrece una serie de funcionalidades y características dirigidas a aplicaciones web y móviles.

## Características clave
- Gestión de identidades y acceso
- Integración de aplicaciones
- Desarrollo de aplicaciones
- Seguridad e inteligencia
- Servicio enfocado en B2B Y B2C

## TENANT
Un tenat representa una organización, se trta de una **instancia deida de Microsoft Entra ID** que una organización o un desarrollador de aplicaciones recibe al principio de su relación con Microsft.

> Cada tenant de Microsoft Entra ID es distinto e indispensable de otros tenants de Microsoft Entra ID

## Arquitectura híbrida con Microsft Entra ID
Se puede integrar con arquictecturas hibridas con centro de datos locales

## Adminsitración de acceso e identidades multicloud

```
                                       ---------------   -------------------
                                       | Aplicaciones |  | Infraestructura |
                                       |     SaaS     |  |     Cloud       |
                                       ---------------   -------------------
                                                       ^
                                                       |
                                            
------------------------------------         ---------------------             ----------------
| - Recursos humanos                |        |                    |            |              |
| - Identidades externas            | <----> | MICROSOFT ENTRA ID | <--------> | Dispositivos |
| - Identidades de carga de trabajo |        |                    |            |              | 
------------------------------------          ---------------------            ----------------

                                                      ^
                                                      |

                                              ---------------
                                              | Aplicaciones |
                                              |   On-prem    |
                                              ----------------
```


## Portales de adminsitación de identidades en Microsoft

- portal.azure.com
- entra.microsoft.com: centrado en usuarios, grupos, roles acceso condiciona, gobernaza, etc

## Licencias de Microsoft Entra ID
### Qué es una licencia
Permite accede legalmente a sevicios de pago, definen que productos y servicios puede usar cada usuario y son obligatorias para cumplir con los contratos y evitar sanciones.

### Tipos de licencias
- Gratis
- P1
- P2
- Governance (pago por uso)

#### Microsoft Entra ID Gratis
- **Adminsitración** de grupos y usuarios
- **Sincronización** de directores locales
- Informes básicos
- Cambio de contraseñas para usuarios locales y en la nube
- Inicio de sesión único en Azure, Microsoft 365 y aplicaciones SaaS

#### Microsoft Entra
##### Microsoft Entra ID P1
- Incluye todo lo de lla versión Free
- Acceso híbrido a recursos locales y en la nube
- **Adminsitración Avanzada** y grupos de pertenencía dinámicos
- Frupos de autoservicio y Micrososft Identity Manager
- Restablecimeinto de contraseñas en autoservicio

**Funcionalides del plan**
- Autoservicio de grupos: Los usuario crean, adminsitran y solicitan universe a grupos.
- Informes y alertas avanzadas: detección de anomalías y patrones de acceso incoherente
- Autenticación multifactor: compatible con VPN, Azure, Microsoft 365, Dynamics 365, etc
- Micorsoft Identity Manager: Enlaza almacenes locales (AD DS, LDAP, Oracle)
- SLA de **99.9% dedisponibilidad garantizada
- Restablecimeinto de contraseña con escritura diferida
- Cloud App Discovery: detecta aplicaciones en la nube no autorizadas
- Acceso condicional por dispositivo, grupo o ubicaicón
- Enta Connect Health: Monitoriza y entrega alertas sobre Entra ID

##### Microsoft Entra ID P2
- Incluye todo lo Gratis y P1
- Microsoft Entra ID Protection: acceso condicional según riesgos
- Privileged Identity Managment: **destacar, restringir** y supervisasr accesos
- Acceso just-in-tima para adminsitradores

**Funcionalidades del plan**
- Protección de Microsoft Entra ID:
	- Supervisión avanzada de cuentas
	- Directivas de riego de incio de sesión  y comportamiento de usuarios.
- Privileged Identity Managment (PIM)
	- Gestión de accesos con privilegios
	- Permite adminsitradores temporales o permanentes.
	- Define reglas y flujos de aprobación para elevar privilegios.

#### Microsoft Entra ID Governance
- **Gestión avanzada** de identidades para clientes P1 y P2
- Licencias de **Pago por uso**:
	- Microsoft Entra Domain Services
	- CIAM (admisnitración de identidades y acceso para aplicaciones orientadas al cliente)

## LICENCIAS INDIVIDULAES VS EN GRUPO

