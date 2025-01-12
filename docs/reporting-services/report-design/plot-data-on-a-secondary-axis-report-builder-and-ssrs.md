---
title: Trazar datos en un eje secundario (Generador de informes y SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 86d73f2ab16bdb7ee801e333f3a75c96a2a1c360
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578191"
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>Trazar datos en un eje secundario (Generador de informes y SSRS)

El gráfico tiene dos tipos de ejes: el principal y el secundario. El eje secundario resulta de gran utilidad cuando se comparan dos conjuntos de valores con dos intervalos de datos definidos que comparten una categoría común.  
  
 Por ejemplo, imagine que tiene un gráfico que calcula los ingresos frente a los impuestos durante el año 2008. En este caso, el período de tiempo 2008 es común a ambos conjuntos de valores. Sin embargo, si ambas series se trazan en el mismo eje Y, no podremos realizar una comparación útil porque la escala del eje Y se optimiza para los valores más altos del conjunto de datos. Si mostramos los ingresos en el eje principal, y los impuestos en el eje secundario, podremos mostrar cada serie en su propio eje Y con su propia escala de valores. Las series siguen compartiendo un eje X común.  
  
 En aquellas situaciones en las que se necesita comparar más de dos series, considere un enfoque diferente para comparar y mostrar dichas series. Para más información, vea [Mostrar varias series en un gráfico](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Un ejemplo de este gráfico está disponible como informe de ejemplo. Para más información acerca de cómo descargar este y otros informes de ejemplo, consulte el tema sobre [informes de ejemplo del Generador de informes y el Diseñador de informes](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>Para trazar una serie en el eje secundario  
  
1.  Haga clic con el botón derecho en la serie del gráfico o en un campo del área **Valores** que quiera mostrar en el eje secundario y, después, haga clic en **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  Haga clic en **Ejes y área del gráfico**y seleccione los ejes secundarios que desea habilitar, el eje de valores o el eje de categorías.  

## <a name="next-steps"></a>Pasos siguientes

[Aplicar formato a las etiquetas de los ejes de un gráfico](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
[Especificar un intervalo de eje](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
