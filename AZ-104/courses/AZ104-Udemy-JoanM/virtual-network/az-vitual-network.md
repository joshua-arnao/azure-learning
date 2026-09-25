# AZURE VIRTUAL NETWORK
Proporciona una red privada ailada en el cloud y altamente configurable para ejecutar recursos y serviicos de Azure

Permite: 
-  **crear y gestionar subredes dentro de la red virtual** para organizar y segmentar recursos de manera efectiva.
- Proteger los recursos y datos utilizando **filtros de red y servicios de seguridad avanzados**.
- Permite la **asignación y gestión de bloqueos de direcciones IP privadas**


## Subredes
Permiten particionar tu red dentro de Azure Virtual Network
	- Una **subred pública** es una subred accesible desde Internet
	- Una **subred privada** es una sub red a la que no se puede acceder desde internet.

Cada subred **debe de tener un intervalo de direcciones único, es pecificado en formato CIDR, en el espacio de direccones de la red virtual.
	- Este intervalo de direcciones no puede superponerse con otras subredes de la red virtual.

