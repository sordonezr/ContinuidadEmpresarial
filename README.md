# Automatización del procedimiento para implementar la recuperación ante desastres mediante copias de seguridad y restauración del servicio en Azure API Management

![APIM_Back_Restore drawio](https://user-images.githubusercontent.com/17581842/171729077-28f220e8-649d-4401-9103-83ce369979d0.png)

## APIM - Origen

![image](https://user-images.githubusercontent.com/17581842/172230750-41772321-f8be-400e-8ae8-378a85aea5f6.png)

## APIM - Destino

![image](https://user-images.githubusercontent.com/17581842/172232262-658833d7-c53e-4137-87fa-3ff0ac1bbba0.png)


## Recursos

- Storage Account
- API Management Origen
- API Management Destino
- Logic Apps


## Restricciones al realizar una solicitud de copia de seguridad o restauración

- Mientras la copia de seguridad esté en curso, evite hacer cambios de administración en el servicio, como una actualización o un cambio a una versión anterior de una SKU, el cambio en un nombre de dominio, etc.
- La restauración de una copia de seguridad se garantiza solo durante 30 días a partir del momento en que esta se crea.
- Es posible que los cambios que se realicen en la configuración del servicio (por ejemplo, las API, las directivas y la apariencia del portal para desarrolladores) mientras se está realizando la operación de copia de seguridad no se incluyan en la copia de seguridad y se pierdan.
- Es posible que los cambios que se realicen en la configuración del servicio (por ejemplo, las API, las directivas y la apariencia del portal para desarrolladores) mientras se está realizando la operación de copia de seguridad no se incluyan en la copia de seguridad y se pierdan.
- La SKU en la que desea restaurar el servicio debe coincidir con la SKU del servicio del que ha creado una copia de seguridad que desea restaurar.


![image](https://user-images.githubusercontent.com/17581842/172231271-6fd5a256-8f96-4587-b6f7-86248cdca76e.png)

## Aplicacion Logica

Backup - Restore

![image](https://user-images.githubusercontent.com/17581842/172236651-f62e8159-7d29-4a30-9c6b-1aec47364cdf.png)


# Recurrencia

![image](https://user-images.githubusercontent.com/17581842/172236850-becd0ac0-8eb6-46ff-9c56-c1a352e67270.png)


# Peticion Http para la generacion del Backup

![image](https://user-images.githubusercontent.com/17581842/172236995-66d84f54-94de-49e3-ab74-d4af4746f4a4.png)

# Endpoint utilizado para la generacion del backup: 

POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}


Enlace de referencia: https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-disaster-recovery-backup-restore

## Verificacion de la respuesta del request

![image](https://user-images.githubusercontent.com/17581842/172274313-e737689e-219a-411d-8b49-72c4a379ff93.png)


## Restauracion de la copia de seguridad

![image](https://user-images.githubusercontent.com/17581842/172274441-0c682dab-e80f-4243-9698-44e1d0ddf78e.png)

# Endpoint utilizado para la restauracion del backup: 

POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}


## Configuracion Identidad
![image](https://user-images.githubusercontent.com/17581842/172233436-7688b63e-ccbc-496d-b425-05789bd50675.png)

![image](https://user-images.githubusercontent.com/17581842/172235480-9a762c7b-41b1-4040-9ce2-1b11a5a50e72.png)
