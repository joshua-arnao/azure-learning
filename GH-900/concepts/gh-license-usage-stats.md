# ESTADÍSTICAS DE USO DE LINCENCIAS

Como **adminstrador de GitHub Enterprise** el seguimiento al **uso de licencias** es fundamental para administrar los **costos**, **optimizar recursos** y **mantenerse en objetivos**

> Para los planes prepago(basados en suscripciones) verá un número establecido de licencias disponibles. En caso de los planes Pay-As-You-Go(PAYG)no existe el concepto de "licencias disponibles" por ello la facturación se basa en el uso real y se cobra cada vez según su uso.

## USO DE LICENCIA PARA UNA ORGANIZACIÓN ESPECÍFICA
Uso de la consola de administración de GitHub Enterprise Cloud (GHEC)

1. Vaya al Panel de administración de GitHub Enterprise Cloud. 
2. Vaya a Configuración > Facturación y planes. 
3. Busque la sección Uso de licencias. 
4. Revise los detalles, como:
   - Total de puestos asignados 
   - Usuarios activos en uso 
   - Invitaciones pendientes 
   - Licencias disponibles (solo se muestran para las cuentas de prepago)

Alternativa de línea de comandos (GraphQL API):
```
{
  organization(login: "org-name") {
    billingInfo {
      totalSeats
      seatsUsed
      seatsAvailable
    }
  }
}
```

## BÚSQUEDA DEL USO DE LICENCIAS EN VARIAS ORGANIZACIONES
Uso de la página de facturación de la cuenta de empresa
1. Vaya a La configuración de GitHub Enterprise Cloud > Enterprise. 
2. Vaya a Facturación > Uso de Licencia.
3. Revise el uso de licencias para cada organización en la cuenta de empresa.

Consulta de GraphQL API para todas las organizaciones:
```
{
  enterprise(slug: "enterprise-name") {
    organizations(first: 50) {
      nodes {
        name
        billingInfo {
          totalSeats
          seatsUsed
          seatsAvailable
        }
      }
    }
  }
}
```

## BÚSQUEDA DEL USO DE LICENCIAS PARA CUENTAS EMPRESARIALES
Uso del panel de GitHub Enterprise Server (GHES)
1. Inicie sesión en la consola de administración del servidor de GitHub Enterprise. 
2. Vaya a Configuración Uso > de licencia. 
3. Revisión:
   - Total de licencias asignadas 
   - Usuarios activos 
   - Usuarios disponibles 
   - Tendencias históricas de uso de licencias 
Alternativa a la API REST
```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprises/YOUR-ENTERPRISE/license"
```

## BÚSQUEDA DEL USO DE LICENCIAS EN VARIAS INSTANCIAS DE GITHUB
Uso de la API de métricas de GitHub Enterprise
1. Acceda a la configuración de administración de GitHub Enterprise Server. 
2. Use la API de métricas:
   ```bash
   curl -H "Authorization: token YOUR-TOKEN" \
   "https://api.github.com/enterprise/settings/licenses"
   ```
3. Revisión:
Total de licencias de toda la empresa
Uso por instancia de GitHub
Capacidad disponible por región

## PROCEDIMIENTOS RECOMENDADOS PARA LA ADMINISTRACIÓN DEL USO DE LICENCIAS
- **Automatice la supervisión**: use consultas de GraphQL o API REST para realizar un seguimiento de las tendencias de uso. 
- **Reclamar puestos no utilizados**: identifique a los usuarios inactivos y libere licencias no usadas. 
- **Habilitar la facturación basada en el uso**: alinee la facturación con el consumo real. 
- **Auditar periódicamente**: realice revisiones mensuales o trimestrales para controlar los costos.
