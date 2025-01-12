---
title: 'Inicio rápido: Conexión a una base de datos de Azure SQL y consulta de ella'
titleSuffix: Azure Data Studio
description: En este inicio rápido se muestra cómo usar Azure Data Studio para conectarse a una base de datos SQL y ejecutar una consulta
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: bdb1a9c8efb8ebdf5d2e35c1da00c12578ade7d6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959434"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Inicio rápido: Uso de [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a una base de datos de Azure SQL y consultarla

En este inicio rápido, se usa [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a un servidor de Azure SQL Database. Luego, se ejecutan instrucciones de Transact-SQL (T-SQL) para crear y consultar la base de datos TutorialDB, que se emplea en otros tutoriales de [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="prerequisites"></a>Prerequisites

Para realizar este inicio rápido, se necesita [!INCLUDE[name-sos](../includes/name-sos-short.md)] y un servidor de Azure SQL Database.

- [Instalación de [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Si no tiene un servidor de Azure SQL, complete uno de los siguientes inicios rápidos de Azure SQL Database. Recuerde el nombre completo del servidor y las credenciales de inicio de sesión para los pasos posteriores:

- [Creación de una base de datos con el portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Creación de una base de datos con la CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Creación de una base de datos con PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectar al servidor de Azure SQL Database

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión al servidor de Azure SQL Database.

1. La primera vez que se ejecuta [!INCLUDE[name-sos](../includes/name-sos-short.md)], debe abrirse la **página principal**. Si no ve la **página principal**, seleccione **Ayuda** > **Página principal**. Seleccione **Nueva conexión** para abrir el panel **Conexión**:
   
   ![Icono Nueva conexión](media/quickstart-sql-database/new-connection-icon.png)

2. En este artículo se usa el inicio de sesión de SQL, pero también se admite la autenticación de Windows. Rellene los campos siguientes con el nombre del servidor, el nombre del usuario y la contraseña del servidor de Azure SQL:

   | Configuración       | Valor sugerido | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | Algo como: **servername.database.windows.net**. |
   | **Autenticación** | Inicio de sesión de SQL| En este tutorial se usa la autenticación de SQL. |
   | **User name** | Nombre de usuario de la cuenta de administrador del servidor | Nombre de usuario de la cuenta usada para crear el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Contraseña de la cuenta usada para crear el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione **Sí** si no quiere escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *dejar en blanco* | Solo se está conectando al servidor aquí. |
   | **Grupo de servidores** | Seleccione <Default> | Puede establecer este campo en un grupo de servidores específico que haya creado. | 

   ![Icono Nueva conexión](media/quickstart-sql-database/new-connection-screen.png)  

3. Seleccione **Conectar**.

4. Si el servidor no tiene una regla de firewall que permita a Azure Data Studio conectarse, se abre el formulario **Crear nueva regla de firewall**. Rellene el formulario para crear una nueva regla de firewall. Para obtener detalles, vea [Reglas de firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-database/firewall.png)  

Después de conectarse correctamente, el servidor se abre en la barra lateral **SERVIDORES**.

## <a name="create-the-tutorial-database"></a>Crear la base de datos del tutorial

En las secciones siguientes se crea la base de datos TutorialDB que se usa en otros tutoriales de [!INCLUDE[name-sos](../includes/name-sos-short.md)].

1. Haga clic con el botón derecho en el servidor de Azure SQL en la barra lateral **SERVIDORES** y seleccione **Nueva consulta**.

1. Pegue este SQL en el editor de consultas.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. En la barra de herramientas, seleccione **Ejecutar**. Aparecen notificaciones en el panel **MENSAJES** que muestran el progreso de la consulta.

## <a name="create-a-table"></a>Creación de una tabla

El editor de consultas se conecta a la base de datos **master**, pero lo que se pretende aquí es crear una tabla en la base de datos **TutorialDB**. 

1. Conéctese a la base de datos **TutorialDB**.

   ![Cambio de contexto](media/quickstart-sql-database/change-context2.png)



1. Cree una tabla `Customers`. 

   Reemplace la consulta anterior del editor de consultas por esta y seleccione **Ejecutar**.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>Insertar filas en la tabla

Reemplace la consulta anterior por esta y seleccione **Ejecutar**.

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>Ver el resultado

Reemplace la consulta anterior por esta y seleccione **Ejecutar**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Los resultados de la consulta muestran:

   ![Selección de resultados](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Limpiar recursos

Los artículos de inicio rápido posteriores se basan en los recursos creados aquí. Si planea trabajar en estos artículos, asegúrese de no eliminar estos recursos. De lo contrario, en Azure Portal, elimine los recursos que ya no necesite. Para obtener detalles, vea [Limpieza de recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Pasos siguientes

Ahora que se ha conectado correctamente a una base de datos de Azure SQL y ha ejecutado una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
