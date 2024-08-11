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

## Procedimiento

1. Vaya a la instancia de API Management en Azure Portal.

2. En el menú izquierdo, en Configuración, seleccione Migración de plataforma.

3. En la página Migración de plataforma, en Paso 1, revise los requisitos y prerrequisitos de la migración.

4. En Paso 2, elija la configuración de la migración:

- Seleccione una ubicación para migrar.

- Seleccione la Red virtual, Subred y, opcionalmente, la Dirección IP pública a la que quiere migrar.

![image](https://github.com/user-attachments/assets/20bdecce-fc8f-4279-a8b1-38a84667cecd)

- Seleccione Volver a la subred original lo antes posible o Quedarse en la nueva subred y mantener el proceso stv1 durante 48 horas después de la migración. Si elige la primera opción, el proceso de stv1 se eliminará aproximadamente 15 minutos después de la migración, lo que le permitirá proceder directamente con la migración de vuelta a la subred original si así lo desea. Si elige la segunda opción, el proceso de stv1 se conservará durante 48 horas. Puede usar este período para validar la configuración de red y la conectividad.

![image](https://github.com/user-attachments/assets/f9a7aa0c-b960-4d92-9d46-d0b96d2ecb03)

5. En Paso 3, confirme que quiere migrar y seleccione Migrar. El estado de la instancia de API Management cambia a Actualizando. El proceso de migración tarda aproximadamente 45 minutos en completarse. Cuando el estado cambia a En línea, se completa la migración.

Si la instancia de API Management se implementa en varias regiones, repita los pasos anteriores para continuar con la migración de la configuración de red virtual para las ubicaciones restantes de la instancia.
