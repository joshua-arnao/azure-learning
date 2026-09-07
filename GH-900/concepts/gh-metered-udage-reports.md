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