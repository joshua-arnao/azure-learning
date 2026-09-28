# Code Scanning
El code scanning usa **CodeQL** para analizar el código de un respoitorio GitHub en buca de vulnerabilidades de seguridad de codificación. El code scanning esta disponible para todos los repositorio públicos y para repositorios privados propiedad de organizaciones que tienen habilitado **GitHub Advanced Security**.
Si el code scanning detecta detecta una posibles vulnerabilidad o error en el código, GitHub muestra una alerta en  la **pestaña de seguridad¨¨ del repositorio.

## Code Scannig con CodeQL
CodeQL es el motor de anális de código desarrollaod por GitHub paraautomatizar las comprobaciones de seguridad. 

### Configuración de CodeQL para code scanning
- Configuración predeterminada, controla la elección de los lenguajes para analizar, el conjunto de consultas que se va a ejecutar y los eventos que desencadenan, se ejecutan como  GitHub Action
- Configuración avanzada para agregar el flujo de trabajo de CodeQL directamente al repositorio genera un archivo de flujo de trabajo personalizable que usa GitHub Action para ejecutar la CLI de CodeQl
- Ejecutar la CLI de CodeQL directamente en un sistema de CI externo y cargue los resultados en GitHub
