---
title: Agregar una referencia de ensamblado a un informe (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e13f6c0d8c4c81a60e1a93898119bbb0884b2d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582149"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Agregar una referencia de ensamblado a un informe (SSRS)
  Al insertar código personalizado que contiene referencias a clases [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que no están en <xref:System.Math> ni en <xref:System.Convert>, necesita proporcionar una referencia de ensamblado al informe para que el procesador de informes pueda resolver los nombres. Para más información, vea [Agregar código a un informe &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Para agregar una referencia de ensamblado a un informe  
  
1.  En la vista **Diseño** , haga clic con el botón derecho en la superficie de diseño (fuera del borde del informe) y, después, haga clic en **Propiedades del informe**.  
  
2.  Haga clic en **Referencias**.  
  
3.  En **Agregar o quitar ensamblados**, haga clic en **Agregar** y, a continuación, haga clic en el botón de puntos suspensivos para buscar el ensamblado.  
  
4.  En **Agregar o quitar clases**, haga clic en **Agregar** y, a continuación, escriba el nombre de la clase y especifique un nombre de instancia para usarlo dentro del informe.  
  
    > [!NOTE]  
    >  Especifique un nombre de clase e instancia solo para miembros basados en instancias. No especifique miembros estáticos en la lista **Clases** . Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)subyacente.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Propiedades del informe (cuadro de diálogo), Referencias](https://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
