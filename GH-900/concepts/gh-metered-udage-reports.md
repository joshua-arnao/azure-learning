# REPORTE DE USO SEGÚN CONSUMO
GitHub proporciona informes detallados de facturación y consumo para realizar un seguimiento del uso de **productos por consumo**. Esots informes ayudan a los administradores a supervisar los costos, asignar recursos de forma eficaz.

## CONSUMO POR MINUTO EN GITHUB ACTIONS
GitHub actions es una herramienta de automatización de CI/CD donde los flujos de trabajo se ejecutan en máquinas virtuales. Los minutos consumidos en estos flujos de trabajo se miden en función del tipo de **repositorio** el **tipo de ejecutor** y el **uso**.

### SEGUIMIENTO DE CONSUMO
- Vaya a Configuración → Facturación en la organización o cuenta de GitHub. 
- En la sección GitHub Actions, puede ver el número de minutos usados. 
- El uso se desglosa por repositorio, tipo de ejecutor (Linux, macOS, Windows) y cuota restante.

### DETALLES DE FACTURACIÓN
- Asignación gratuita
  - Los repositorios públicos obtienen minutos **gratuitos ilimitados**
   Los repositorios privados recibe minutos gratuitos en función del plan

    | Plan              | minutos/mes |
    |:------------------|:-----------:|
    | GitHub Gratis     |    2000     |
    | GitHub Pro        |    3000     |
    | GitHub Team       |    3000     |
    | GitHub Enterprise |    50000    |
  
   - Precios por tipo de Ejecutor
  
     | Ejecutor | precio/minuto |
     |:---------|:-------------:|
     | Linux    |   0.008 USD   |
     | Windows  |   0.016 USD   |
     | macOS    |   0.08 USD    |

### ESTRATEGIAS DE  OPTIMIZACIÓN

- Usar **ejecutores autohospedados** para flujos de trabajo de gran volumen para reducir los costos.
- Optimizar los scripts de flujo de trabajo mediante el almacenamiento en caché de dependencias y reduzca los trabajos redundantes.
- Limite de flujos de trabajo para que **solo se desencadenen cuando sea necesario**(por ejemplo, insertar solo en la rama `main`)

## ALMACENAMIENTO PARA PAQUETES DE GITHUB
Los paquetes de GitHub permite almacenar artefactos, imágenes de contenedor y dependencias. El almacenamiento se mide en función del volumen de datos almacenados y el uso de transferencía de datos.

## LICENCIAS DE GITHUB ENTERPRICE(GHE)
GHE proporciona características avanzadas para las organizaciones y el número de **usuarios activos** determina el consumo de licencias.

### SEGUIMIENTO DE CONSUMO

- Ir a **configuración de empresas** -> **Facturación** para ver **los informes de uso de licencias**
- Supervisar los usuarios activos frente a las licencias asignadas.

### DETALLES DE FACTURACIÓN
- Modelo de precios:
  - Cada usuario con acceso a repositorios privados consume **una licencia**.
  - Las organizaciones pagan por usuario anualmente o mensualmente.
- Usuarios inactivos:
  - Si un administrador **quita** un usuario, la licencia permanece **asignada** durante el período de facturación, pero se puede reasignar.

### ESTRATEGÍAS
- Audite a los usuarios inactivos y revoque el acceso para liberar licencias.
- Utilice SSO y el aprovisionamiento SCIM para automatizar la administración de usuarios.

## LICENCIAS DE GITHUB ADVANCED SECURITY (GHAS)
Ofrece **análisis de código**, **análisis de secretos** y **Revisión de dependencias** para mejorar la seguridad.

### SEGUIMIENTO DEL CONSUMO
- Para ver el uso de GitHub Advanced Security(GHAS), en [GitHub]("https://GitHub.com"), seleccione Empresas en el panel de navegación lateral, seleccione su empresa en la lista y a continuación vaya a facturación -> Advanced security,
  - Un confirmador activo es cualquier persona que haya insertado al menos un commit en un repositorio con GitHub Advanced Security(GHAS) habilitada en los últimos 90 días, independientemente de cuándo se creó originalmente la confirmación.
  - La facturación de GHAS se basa en el número de **confirmadores activos** únicos por período de facturación.