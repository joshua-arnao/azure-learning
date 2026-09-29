# ESPACIO DE DIRECCIONES

Los espacios de direcciones (Address Spaces) son rangos de direcciones IP asignados a las redes virtuales y subredes.

## Qué es un rango de IPs:
- Es un conjunto de direcciones de IP disponibles para asignar a los recursos
	Ejemplo: 10.0.0.0/16 proporciona direcciones dede **10.0.0.1 hasta 10.0.255.254**
	- Indica que los primeros **16** bits de la dirección IP está reservados para identificar la red
	- Con **/1**, se tiene **2^(32-16)** direcciones disponibles o **65536 direcciones totales**
	- Las direcciones 10.0.0.1 y 10.0.255.254 **son reservadas** y **no pueden ser asignadas**

## Qué es una subred:
- Se divide el espacio de direcciones en segmentos más pequeños
	Ejemplo: Subred dentro de 10.0.0.0/16 pordía ser 10.0.1.0/24


