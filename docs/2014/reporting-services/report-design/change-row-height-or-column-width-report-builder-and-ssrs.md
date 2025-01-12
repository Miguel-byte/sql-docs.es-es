---
title: Cambiar el alto de fila o el ancho de columna (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b51e18e4b652dde230c9f5421e27d219695987e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106338"
---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Cambiar el alto de fila o el ancho de columna (Generador de informes y SSRS)
  Cuando se establece un alto de fila, se está especificando el alto máximo para la fila en el informe representado. Sin embargo, de forma predeterminada, los cuadros de texto de la fila están configurados para crecer verticalmente con objeto de dar cabida a sus datos en tiempo de ejecución, y esto puede ocasionar que una fila crezca más allá del alto especificado. Para establecer un alto de fila fijo, debe cambiar las propiedades del cuadro de texto de modo que no se expandan automáticamente.  
  
 Cuando se establece un ancho de columna, se está especificando el ancho máximo para la columna en el informe representado. Las columnas no se ajustan horizontalmente de forma automática para dar cabida al texto.  
  
 Si una celda de una fila o columna contiene un rectángulo o una región de datos, el alto y el ancho mínimos de la celda están determinados por el alto y el ancho del elemento contenido. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>Para cambiar la altura de la fila moviendo los identificadores de columna  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de fila grises en el borde externo de la región de datos Tablix.  
  
2.  Mantenga el mouse sobre el borde del identificador de fila que desea expandir. Aparece una flecha de dos puntas.  
  
3.  Haga clic para arrastrar el borde de la fila y muévalo más arriba o más abajo para ajustar el alto de fila.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>Para cambiar la altura de la fila configurando las propiedades de la celda  
  
1.  En la vista Diseño, haga clic en una celda de la fila de la tabla.  
  
     ![Celda seleccionada en una tabla](../media/table-selectcell.png "Celda seleccionada en una tabla")  
  
2.  En el panel **Propiedades** que aparece, modifique la propiedad **Alto** y, después, haga clic en cualquier parte que no sea el panel **Propiedades** .  
  
     ![Panel Propiedades para la celda de la tabla seleccionada](../media/cell-propertiespane.png "Panel Propiedades para la celda de la tabla seleccionada")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>Para evitar que una fila se expanda verticalmente de forma automática  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de fila grises en el borde externo de la región de datos Tablix.  
  
2.  Haga clic en el identificador de fila para seleccionar esta.  
  
3.  En el panel de propiedades, establezca CanGrow en **False**.  
  
    > [!NOTE]  
    >  Si no puede ver el panel Propiedades, haga clic en **Propiedades** en el menú **Ver**.  
  
### <a name="to-change-column-width"></a>Para cambiar el ancho de columna  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de columna grises en el borde externo de la región de datos Tablix.  
  
2.  Mantenga el mouse sobre el borde del identificador de columna que desea expandir. Aparece una flecha de dos puntas.  
  
3.  Haga clic para arrastrar el borde de la columna y muévalo hacia la derecha o hacia la izquierda para ajustar el ancho de columna.  
  
## <a name="see-also"></a>Vea también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Las columnas, filas y celdas de la región de datos Tablix &#40;generador de informes&#41; y SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
