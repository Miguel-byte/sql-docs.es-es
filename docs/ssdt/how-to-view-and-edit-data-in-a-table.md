---
title: 'Procedimientos: Ver y editar datos de una tabla | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d6a59755f3c6675830324a314cbf364333e105c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140999"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>Procedimientos: Consulta y edición de datos de una tabla
Puede ver, editar y eliminar datos de una tabla existente mediante un Editor de datos visual.  
  
> [!WARNING]  
> Los procedimientos siguientes usan entidades creadas en procedimientos anteriores de la sección [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md).  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>Para editar datos de una tabla visualmente usando el Editor de datos  
  
1.  Haga clic con el botón derecho en la tabla **Products** en el **Explorador de objetos de SQL Server** y seleccione **Ver datos**.  
  
2.  Se iniciará el Editor de datos. Observe las filas que agregamos a la tabla en procedimientos anteriores.  
  
3.  Haga clic con el botón derecho en la tabla **Fruits** en el Explorador de objetos de SQL Server y seleccione **Ver datos**.  
  
4.  En el Editor de datos, escriba **1** en **Id** y **True** en **Perishable**; después, presione ENTRAR o TAB para alejar el foco de la nueva fila y confirmarla en la base de datos.  
  
5.  Repita el paso anterior para escribir **2**, **False** y **3**, **False** en la tabla.  
  
    Mientras edita una fila, siempre puede revertir los cambios de una celda presionando ESC.  
  
6.  Puede ver las modificaciones como un script si hace clic en el botón **Script** de la barra de herramientas. O bien, puede usar el botón **Generar script en archivo** para guardarlas en un archivo de script .sql que se ejecutará más adelante.  
  
7.  Haga clic con el botón derecho en la base de datos **Trade** en el **Explorador de objetos de SQL Server** y seleccione **Nueva consulta**. En el editor, escriba `select * from dbo.PerishableFruits` y haga clic en el botón **Ejecutar consulta** para devolver los datos representados por la vista `PerishableFruits`.  
  
