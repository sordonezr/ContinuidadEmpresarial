## Automatización de la recuperación ante desastres mediante copias de seguridad y restauración del servicio de Azure API Management con Logic Apps

![APIM_Back_Restore drawio](https://user-images.githubusercontent.com/17581842/171729077-28f220e8-649d-4401-9103-83ce369979d0.png)

## Recursos

![image](https://user-images.githubusercontent.com/17581842/174294064-2563dda6-8a34-4e97-b5b7-8deb6f05a6c6.png)

## Restricciones al realizar una solicitud de copia de seguridad o restauración

- Mientras la copia de seguridad esté en curso, evite hacer cambios de administración en el servicio, como una actualización o un cambio a una versión anterior de una SKU, el cambio en un nombre de dominio, etc.
- La restauración de una copia de seguridad se garantiza solo durante 30 días a partir del momento en que esta se crea.
- Es posible que los cambios que se realicen en la configuración del servicio (por ejemplo, las API, las directivas y la apariencia del portal para desarrolladores) mientras se está realizando la operación de copia de seguridad no se incluyan en la copia de seguridad y se pierdan.
- Es posible que los cambios que se realicen en la configuración del servicio (por ejemplo, las API, las directivas y la apariencia del portal para desarrolladores) mientras se está realizando la operación de copia de seguridad no se incluyan en la copia de seguridad y se pierdan.
- La SKU en la que desea restaurar el servicio debe coincidir con la SKU del servicio del que ha creado una copia de seguridad que desea restaurar.

## Aplicación Lógica

Backup - Restore

![image](https://user-images.githubusercontent.com/17581842/172236651-f62e8159-7d29-4a30-9c6b-1aec47364cdf.png)

## Recurrencia

![image](https://user-images.githubusercontent.com/17581842/172236850-becd0ac0-8eb6-46ff-9c56-c1a352e67270.png)

## Petición http para la generación del backup

![image](https://user-images.githubusercontent.com/17581842/172236995-66d84f54-94de-49e3-ab74-d4af4746f4a4.png)

## Endpoint utilizado para la generación del backup 

https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}


## Body

```javascript
{
    "storageAccount": "{storage account name for the backup}",
    "containerName": "{backup container name}",
    "backupName": "{backup blob name}",
    "accessKey": "{access key for the account}"
}
```
[Documentacion Oficial](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-disaster-recovery-backup-restore)

## Verificación de la respuesta del request

![image](https://user-images.githubusercontent.com/17581842/172274313-e737689e-219a-411d-8b49-72c4a379ff93.png)

## Restauración de la copia de seguridad

![image](https://user-images.githubusercontent.com/17581842/172274441-0c682dab-e80f-4243-9698-44e1d0ddf78e.png)

## Endpoint utilizado para la restauración del backup 

https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}

## Configuración Identidad

![image](https://user-images.githubusercontent.com/17581842/174294783-ba2745d4-64f5-40c2-b8f8-25cb26b86afb.png)

![image](https://user-images.githubusercontent.com/17581842/174296441-058edac9-2535-4ee7-af34-d492b78e30bf.png)

## Comprobación de la asignación del rol

### APIM Origen
![image](https://user-images.githubusercontent.com/17581842/174295355-1492300c-fda3-4a4b-8f06-701d7f871018.png)

### APIM Destino
![image](https://user-images.githubusercontent.com/17581842/174295834-b3354c67-8b1a-4455-8719-e5526121b65d.png)

## Backups Generados
![image](https://user-images.githubusercontent.com/17581842/174296187-0b7749c3-0201-419b-af4f-18f019e7c9d0.png)

## Comprobación restauración APIS

![image](https://user-images.githubusercontent.com/17581842/174297399-097f4843-f29b-4582-a9f0-c84aec999387.png)

