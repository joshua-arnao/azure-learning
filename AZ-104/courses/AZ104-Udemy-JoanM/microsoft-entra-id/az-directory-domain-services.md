# AZURE ACTIVE DIRECTORY DOMAIN SERVICES(AZURE AD DS)
Es un servicio gestiionado que facilita la implementación de servicios de dominio en Azure

## Permite
- Autenticación, autorización y aplicación de políticas de seguridad para aplicaicones y usuarios.


- Es esencial para las organizaciones que desean migrar aplicaicones al cloud **sin perder las funcionalidades del Active Directory Domain Services(AD DS) tradicional**
- Permite unificar el manejo de las identidades corporativas en entornos híbridos
- Soporta protocolos de autenticación antiguos(NTLM y Kerberos) esenciales para aplicaicones legacy

## Como funciona Azure AD DS
Es uns ervicio autogestionado, no requiere configuración/gestion del sistema operatico

- Crear un nombre de dominio/espacio de nombres único
	- Dominio independiente, **no** es una extensión del dominio AD local

- Sincronización unidireccional de Micrososft Entra Id a Azure AD DS
	- Sincroniza usuarios, grupos y credenciales
	- Microsoft Entra ID también puede sincronizar bidireccionalmente con AD local



```
                
                 ----------------------------
                 |                          |
                 |     Active Directory     |
                 |                          |
                 ---------------------------
                              ^
                              |
                              |
                              ˅
                 ----------------------------
                 |                          |
                 |         Entra ID         |
                 |                          |
                 ---------------------------
                              |
                              |
                              ˅
                 ----------------------------
                 |                          |
                 |        AZURE AD DS       |
                 |                          |
                 ---------------------------
  
```
 
## Casos de usos Azure AD DS
- mIgración de aplicaicones
- Desarrollo de pruebas


## Microsoft Entra ID vs Azure AD DS


| Criterio / Característica | Microsoft Entra ID | Active Directory Domain Services (AD DS) |
| :--- | :--- | :--- |
| **Tipo de Solución** | Solución de **identidad en la nube**. | Servicio de **directorio jerárquico (X.500)**. |
| **Protocolos Web** | Basado en **HTTP/HTTPS** (puertos 80 y 443). | Usa **DNS** para buscar/controlar recursos. |
| **Arquitectura de Gestión** | Servicio **multinquilino** (multi-tenant). | Administración con **LDAP**. |
| **Estructura Organizativa** | Usuarios y grupos en **estructura plana** (sin OU ni GPO). | Incluye **unidades organizativas (OU) y GPO** (Políticas de Grupo). |
| **Protocolos de Identidad** | **No usa LDAP**, sino API REST + HTTP/HTTPS. No usa Kerberos. | Autenticación con **Kerberos**. |
| **Relaciones de Confianza** | Admite **federación con terceros** (ej. Facebook). | **Confianzas entre dominios** para administración delegada. |
| **Implementación en Azure** | Nativo de la nube. | Puede implementarse en **VM de Azure** (pero sin integrar con Entra ID). |

