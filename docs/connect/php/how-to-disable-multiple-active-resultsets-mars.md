---
title: 'Cómo: Deshabilitar conjuntos de resultados activos múltiples (MARS) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c5edf63a654b21d080e48f93c71553b8909ce8fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993560"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>Cómo deshabilitar los conjuntos de resultados activos múltiples (MARS)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Si necesita conectarse a un origen de datos de SQL Server que no habilite conjuntos de resultados activos múltiples (MARS), puede utilizar la opción de conexión MultipleActiveResultSets para deshabilitar o habilitar MARS.  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-disable-mars-support"></a>Pasos para deshabilitar la compatibilidad con MARS  
  
-   Utilice la opción de conexión siguiente:  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    Si la aplicación trata de ejecutar una consulta en una conexión que tiene un conjunto de resultados activo pendiente, el segundo intento de consulta devolverá la información de error siguiente:  
  
    La conexión no puede procesar esta operación porque no hay una instrucción con resultados pendientes.  Para que la conexión esté disponible en otras consultas, capture todos los resultados, o bien cancele o libere la instrucción. Para obtener más información sobre la opción de conexión MultipleActiveResultSets, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra cómo deshabilitar la compatibilidad con MARS utilizando el controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra cómo deshabilitar la compatibilidad con MARS con el controlador PDO_SQLSRV de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)  
  
