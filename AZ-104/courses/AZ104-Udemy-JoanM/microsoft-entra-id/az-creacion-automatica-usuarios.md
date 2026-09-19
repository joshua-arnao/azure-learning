# CREACIÓN AUTOMÁTICA DE USUARIOS

```

        ---------------------                        ---------------------------------              -------------
        |                   |                        |                               |              |           |              
        | Aplicaicón HCM en |    Datos del usuario   | Servicio de aprovisionamiento |              | Microsoft |
        |    la nube        | <--------------------> |       de Microsoft Entra      | <----------> |  Entra ID |
        |                   |                        |                               |              |           |  
        --------------------                         ---------------------------------              -------------
                                                                     ^
                                                                     |
                                                                     |
                                                                     |
____________________________________________________________________________________________________________________________                                                                     

                         ------------------                --------------------
                         |                |                |                  |
                         | Aplicación HCM |  <---------->  | Active Directory |
                         |     local      |                |                  |
                         |                |                --------------------
                         ------------------
 
                                               HCM = Sistema de adminsitración de capital humano

```

## SCIM: aDMINSITRACIÓN DE IDENTIDADES ENTRE DOMINIOS
**SCIM estándar para aprovisionamiento y desaprovisionamiento** automático de usuarios y grupos.

- Permite integrar aplicaciones y sistemas con Microsoft Entra ID
- Automatiza el ciclo de vida de las identidades

## Componentes principales de SCIM

- Sistema HCM(origen de datos): Apps/tecnología de gestion de capital humano
- Microsoft Entra ID(destion): Repositorio de ususarios e identidades
- Sistema de destino: App o sistema con punto SCIM habilitado
- Miscrosoft Entra Provisioning Service: APIs REST para automatiza alta/baja de usuaarios y grupos
