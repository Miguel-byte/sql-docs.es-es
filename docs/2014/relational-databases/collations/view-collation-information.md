---
title: Ver información de intercalación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9cb0f104d1555b18d18df38027c240a392d2ac66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918745"
---
# <a name="view-collation-information"></a>Ver información de intercalación
    
##  <a name="Top"></a> Puede ver la intercalación de un servidor, una base de datos o una columna en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante las opciones de menú del Explorador de objetos o mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="Procedures"></a> Cómo ver una configuración de intercalación  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para ver una configuración de intercalación de un servidor (instancia de SQL Server) en el Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Haga clic con el botón derecho en la instancia y seleccione **Propiedades**.  
  
 **Para ver una configuración de intercalación de una base de datos en el Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos y seleccione **Propiedades**.  
  
 **Para ver una configuración de intercalación de una columna en el Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, la base de datos y, por último, **Tablas**.  
  
3.  Expanda la tabla que contiene la columna y, a continuación, **Columnas**.  
  
4.  Haga clic con el botón derecho en la columna y seleccione **Propiedades**. Si la propiedad collation está vacía, la columna no es un tipo de datos de caracteres.  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver la configuración de intercalación de un servidor**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y, en la barra de herramientas, haga clic en **Nueva consulta**.  
  
2.  En la ventana de consulta, escriba la siguiente instrucción que usa la función de sistema SERVERPROPERTY.  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  También puede usar el procedimiento almacenado del sistema sp_helpsort.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **Para ver todas las intercalaciones admitidas por [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y, en la barra de herramientas, haga clic en **Nueva consulta**.  
  
2.  En la ventana de consulta, escriba la siguiente instrucción que usa la función de sistema SERVERPROPERTY.  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **Para ver la configuración de intercalación de una base de datos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y, en la barra de herramientas, haga clic en **Nueva consulta**.  
  
2.  En la ventana de consulta, escriba la siguiente instrucción que usa la vista de catálogo del sistema sys.databases.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  También puede usar la función del sistema DATABASEPROPERTYEX.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **Para ver la configuración de intercalación de una columna**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y, en la barra de herramientas, haga clic en **Nueva consulta**.  
  
2.  En la ventana de consulta, escriba la siguiente instrucción que usa la vista de catálogo del sistema sys.columns.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>Vea también  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [Prioridad de intercalación &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [sp_helpsort &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsort-transact-sql)  
  
  
