Procedimiento para implementar la recuperación ante desastres mediante copias de seguridad y restauración del servicio en Azure API Management

Crear una copia de seguridad del servicio API Management

Inicio de sesión con Azure PowerShell.

En los siguientes ejemplos:

Una instancia de API Management denominada myapim está en el grupo de recursos apimresourcegroup.
Una cuenta de almacenamiento denominada backupstorageaccount está en el grupo de recursos storageresourcegroup. La cuenta de almacenamiento tiene un contenedor denominado backups.
Se creará un blob de copia de seguridad con el nombre ContosoBackup.apimbackup.

Establezca las variables en PowerShell:

$apiManagementName="myapim";
$apiManagementResourceGroup="apimresourcegroup";
$storageAccountName="backupstorageaccount";
$storageResourceGroup="storageresourcegroup";
$containerName="backups";
$blobName="ContosoBackup.apimbackup"

Acceso mediante la clave de acceso de almacenamiento

$storageKey = (Get-AzStorageAccountKey -ResourceGroupName $storageResourceGroup -StorageAccountName $storageAccountName)[0].Value

$storageContext = New-AzStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageKey

Backup-AzApiManagement -ResourceGroupName $apiManagementResourceGroup -Name $apiManagementName -StorageContext $storageContext -TargetContainerName $containerName -TargetBlobName $blobName


Restaurar el servicio API Management

En los siguientes ejemplos:

Se restaura una instancia de API Management denominada myapim del blob de copia de seguridad denominado ContosoBackup.apimbackup en la cuenta de almacenamiento backupstorageaccount.
El blob de copia de seguridad está en un contenedor denominado backups.
Establezca las variables en PowerShell:

$apiManagementName="myapim";
$apiManagementResourceGroup="apimresourcegroup";
$storageAccountName="backupstorageaccount";
$storageResourceGroup="storageresourcegroup";
$containerName="backups";
$blobName="ContosoBackup.apimbackup"


Acceso mediante la clave de acceso de almacenamiento

$storageKey = (Get-AzStorageAccountKey -ResourceGroupName $storageResourceGroup -StorageAccountName $storageAccountName)[0].Value

$storageContext = New-AzStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageKey

Restore-AzApiManagement -ResourceGroupName $apiManagementResourceGroup -Name $apiManagementName -StorageContext $storageContext -SourceContainerName $containerName -SourceBlobName $blobName
