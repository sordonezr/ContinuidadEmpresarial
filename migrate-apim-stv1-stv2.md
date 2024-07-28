---
Migración de una instancia de API Management insertada en la red virtual hospedada en la plataforma stv1 a stv2
---

## ¿Qué ocurre durante la migración?

La migración de la plataforma de API Management desde stv1 a stv2 implica actualizar solo el proceso subyacente y no tiene ningún impacto en la configuración del servicio o api persistente en la capa de almacenamiento.

- El proceso de actualización implica la creación de un nuevo proceso en paralelo al proceso anterior, que puede tardar hasta 45 minutos.
- El estado de API Management en el Azure Portal será Actualizado.
- La dirección VIP (o direcciones, para una implementación de varias regiones) de la instancia cambiará.
- Azure administra el DNS del punto de conexión de administración y actualiza el nuevo proceso inmediatamente después de la migración correcta.
- El DNS de puerta de enlace sigue apuntando al proceso anterior si se usa un dominio personalizado.
- Si el DNS personalizado no está en uso, el DNS de puerta de enlace y de portal apunta al nuevo proceso inmediatamente.
- En el caso de una instancia en modo de red virtual interna, el cliente administra el DNS, por lo que las entradas DNS continúan apuntando al proceso antiguo hasta que el cliente lo actualice.
- Es el DNS que apunta al proceso nuevo o antiguo y, por tanto, no hay tiempo de inactividad de las API.
- Los cambios son necesarios para las reglas de firewall, si los hay, para permitir que la nueva subred de proceso llegue a los back-end.
- Después de una migración correcta, el proceso anterior se retira automáticamente después de aproximadamente 15 minutos de forma predeterminada. Puede habilitar una configuración de migración para conservar la puerta de enlace antigua durante 48 horas. La opción de retraso de 48 horas solo está disponible para los servicios insertados en la red virtual.
