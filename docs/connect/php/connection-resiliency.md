---
title: Resistencia de conexión inactiva
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265171"
---
# <a name="idle-connection-resiliency"></a>Resistencia de conexión inactiva
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

La [resistencia de conexión](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) es el principio de que se puede restablecer una conexión inactiva interrumpida, dentro de ciertas restricciones. Si se produce un error en una conexión a Microsoft SQL Server, la resistencia de conexión permite al cliente intentar restablecer la conexión automáticamente. La resistencia de conexión es una propiedad del origen de datos; solo SQL Server 2014 y versiones posteriores y Azure SQL Database admiten la resistencia de la conexión.

La resistencia de conexión se implementa con dos palabras clave de conexión que se pueden agregar a las cadenas de conexión: **ConnectRetryCount** y **ConnectRetryInterval**.

|Palabra clave|Valores|Valor predeterminado|Descripción|
|-|-|-|-|
|**ConnectRetryCount**| Un entero comprendido entre 0 y 255, ambos incluidos|1|Número máximo de intentos para restablecer una conexión interrumpida antes de abandonarla. De forma predeterminada, se realiza un único intento de restablecer una conexión cuando se interrumpe. Un valor de 0 significa que no se intentará ninguna reconexión.|
|**ConnectRetryInterval**| Un entero comprendido entre 1 y 60, ambos incluidos|1| El tiempo, en segundos, entre los intentos para restablecer una conexión. La aplicación intentará volver a conectarse inmediatamente al detectar una conexión interrumpida y, después, esperará **ConnectRetryInterval** segundos antes de volver a intentarlo. Esta palabra clave se omite si **ConnectRetryCount** es igual a 0.

Si el producto de **ConnectRetryCount** multiplicado por **ConnectRetryInterval** es mayor que **LoginTimeout**, el cliente dejará de intentar conectarse una vez que se alcance **LoginTimeout** ; de lo contrario, seguirá intentando volver a conectarse hasta que se alcance **ConnectRetryCount** .

#### <a name="remarks"></a>Notas

La resistencia de la conexión se aplica cuando la conexión está inactiva. Los errores que se producen al ejecutar una transacción, por ejemplo, no desencadenarán intentos de reconexión; de lo contrario, se producirá un error como cabría esperar. Las siguientes situaciones, que se conocen como Estados de sesión no recuperable, no desencadenarán intentos de reconexión:

* Tablas temporales
* Cursores globales y locales
* Bloqueos de transacciones de nivel de sesión y contexto de transacción
* Bloqueos de aplicaciones
* EJECUTAR como/revertir contexto de seguridad
* Identificadores de automatización OLE
* Identificadores XML preparados
* Marcas de seguimiento

## <a name="example"></a>Ejemplo

El código siguiente se conecta a una base de datos y ejecuta una consulta. La conexión se interrumpe al eliminar la sesión y se intenta realizar una nueva consulta mediante la conexión interrumpida. En este ejemplo se utiliza la base de datos de ejemplo [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx).

En este ejemplo, se especifica un cursor almacenado en búfer antes de interrumpir la conexión. Si no se especifica un cursor almacenado en búfer, la conexión no se restablecerá porque hubiera un cursor de servidor activo y, por lo tanto, la conexión no estará inactiva cuando se interrumpa. Sin embargo, en ese caso podríamos llamar a sqlsrv_free_stmt () antes de interrumpir la conexión para eliminar el cursor y la conexión se restablecería correctamente.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
Salida esperada:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>Consulte también
[Resistencia de conexión en el controlador Windows ODBC](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
