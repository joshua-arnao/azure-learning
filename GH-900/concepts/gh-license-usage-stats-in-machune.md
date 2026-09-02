# ESTADÍSTICAS DE USO DE LICENCIAS EN DISPOSITIVOS PERIFÉRICOS Y Y MACHINE ACCOUNT
Las **Machine account**(usadas para la automatización) y los **Servicios periféricos**(como CI/CD, integraciones y consumidores de API) pueden consumir licencias, lo que afecta a los costos empresariales y a la administración de recursos.

## MACHINE ACCOUNT
Son cuentas de GitHub que se usan para la automatización, la ejecución de scripts o la integración con herramientas de terceros.

### CARACTERÍSTICAS
- Actuán **independiente de los usuarios humanos**
- A menudo se usa en las herramientas de CI/CD(GitHub Actions, Jenkins, CircleCI)
- **Cada machine account** consume una licencia de GitHub como un usuario estándar.

## SERVICIOS PERIFÉRICOS
Son integraciones externas que interactuán con GitHub a través de **solicitudes de API**.

**Ejemplos**: 
- **CI/CD Pipeline**(GitHub Actions, GitHub Runner, Jenkis)
- **Herramientas de scanneo de seguridad**(Dependabot, Snyk, CodeQL)
- **Integración de terceros**(Slack, Jira, Datalog)
- **Ejecutores de GitHub autohospedados**

### ¿Por qué realizar un seguimiento de estos?

- Para **identificar licencias sin usar o excesivas**.
- Para **optimizar los costos*** y evitar gastos innecesarios.
- Para **supervisar los riesgos de seguridad** de cuentas de automatización inactivas o mal configuradas.

## BÚSQUEDA DE ESTADÍSTICAS DE USO DE LICENCIAS PARA CUENTAS DE MÁQUINA

### MÉTODO1 : CONSOLA DE ADMINSITRACIÓN DE GITHUB ENTERPRISE
1. Vaya a Configuración de empresa. 
2. Seleccione **Billing & License Management**. 
3. Busque una sección **Cuentas de equipo** (si está disponible).
4. Identifique:
   - Número de cuentas de máquina activas. 
   - Consumo de licencias por cuenta de máquina. 
   - Última fecha activa.

### MÉTODO 2: CONSULTA DE GRAPHQL API PARA CUENTAS DE MÁQUINAS
Para obtener estadísticas sobre el uso de cuentas de máquina, use la API de GraphQL:
```
{
  enterprise(slug: "enterprise-name") {
    organizations(first: 50) {
      nodes {
        name
        machineAccounts {
          totalCount
          nodes {
            login
            createdAt
            lastActiveAt
          }
        }
      }
    }
  }
}
```
**¿Por qué realizar un seguimiento de estos?**

- Para identificar **machine account inactivas**.
- Para realizar un seguimiento de cada machine account y saber cuando estuvo activa por última vez.
Para ayudar a reducir la asignación de licencias innecesaria.

## BÚSQUEDA DEL USO DE LICENCIAS PARA SERVICIOS PERIFÉRICOS
### MÉTODO 1: MÉTRICAS DE USO DE ACCIONES Y EJECUTORES DE GITHUB
1. Vaya a Configuración de empresa** → Acciones. 
2. Vista:
   - Total de minutos de ejecutor hospedados en GitHub.
   - Uso del ejecutor autohospedado. 
   - Facturación de minutos adicionales del ejecutor.

## PROCEDIMIENTOS RECOMENDADOS PARA ADMINISTRAR CUENTAS DE MÁQUINA Y LICENCIAS DE SERVICIOS PERIFÉRICOS
- **Auditar machine accounts** periodicamente: Garantiza que solo existen cuentas **activas** y **necesarias.
- **Supervisar el uso de api**: Realizar seguimiento de las herramientas de terceros que consumen licencias empresariales.
- **Optimización del uso del ejecutor**: Idenficar los ejecutores autohospedados inactivos y reduzca los costos del ejecutor hospedado en GitHu ya que funcionan de forma **pago por uso**.