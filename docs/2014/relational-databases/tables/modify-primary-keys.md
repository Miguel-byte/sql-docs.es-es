---
title: Modificación de claves principales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9e19d6d6453acedff16e46dbd2d90d92a3b9587
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211822"
---
# <a name="modify-primary-keys"></a>Modificar claves principales
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , una clave principal puede modificarse mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede modificar la clave principal de una tabla si cambia el orden de las columnas, el nombre del índice, la opción agrupada o el factor de relleno.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una clave principal con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-primary-key"></a>Para modificar una clave principal  
  
1.  Abra el Diseñador de tablas de la tabla cuya clave principal quiere modificar; después, haga clic con el botón derecho en el Diseñador de tablas y elija **Índices o claves** en el menú contextual.  
  
2.  En el cuadro de diálogo **Índices o claves** , seleccione el índice de clave principal en la lista **Índice o clave Primary/Unique seleccionados** .  
  
3.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |En|Siga estos pasos|  
    |--------|------------------------|  
    |Cambiar el nombre de la clave principal|Escriba un nuevo nombre en el cuadro **Nombre** . Asegúrese de que el nuevo nombre no está duplicado en la lista **Índice o clave Primary/Unique seleccionados** .|  
    |Establecer la opción de índice clúster|Para crear un índice agrupado para la clave principal, seleccione **Crear como CLUSTERED**y seleccione la opción en el cuadro de lista desplegable. Solo puede existir un índice clúster por tabla. Si esta opción no está disponible para el índice, antes de nada debe desactivar esta configuración en el índice clúster existente.<br /><br /> Si no está seleccionada esta opción, se crea un índice no agrupado único.|  
    |Definir un factor de relleno|Expanda la categoría **Especificación de relleno** y escriba un número entero de 0 a 100 en el cuadro **Factor de relleno** . Para obtener más información sobre los factores de relleno y sus usos, vea [Especificar el factor de relleno para un índice](../indexes/specify-fill-factor-for-an-index.md).|  
    |Cambiar el orden de las columnas|Haga clic en **Columnas** y, después, haga clic en los puntos suspensivos **(...)** situados a la derecha de la propiedad. En el cuadro de diálogo  **Columnas de índice** , quite las columnas de la clave principal. A continuación, vuelva a agregar las columnas en el orden que desee. Para quitar una columna de la clave, solo tiene que quitar el nombre de la columna de la lista **Nombre de columna** .|  
  
4.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar una clave principal**  
  
 Para modificar una restricción PRIMARY KEY mediante Transact-SQL, primero debe eliminar la restricción PRIMARY KEY existente y, a continuación, vuelva a crearla con la nueva definición. Para obtener más información, consulte [Delete Primary Keys](delete-primary-keys.md) y [Create Primary Keys](create-primary-keys.md).  
  
###  <a name="TsqlExample"></a>  
