---
title: Depurar el código de extensión de procesamiento de datos | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 031dade1cb1f5535a1b0ccacc0efe4ca8b241ccb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194049"
---
# <a name="debugging-data-processing-extension-code"></a>Depurar el código de extensión de procesamiento de datos
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proporciona varias herramientas de depuración que pueden ayudarle a analizar el código de extensión del procesamiento de datos y localizar errores en él. La herramienta más conveniente dependerá de lo que intente llevar a cabo. En este ejemplo se usa [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>Para depurar el código de extensión de procesamiento de datos  
  
1.  Inicie [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] y abra el proyecto de extensión de procesamiento de datos.  
  
2.  Genere el proyecto e implemente el ensamblado de extensión de procesamiento de datos y el archivo .pdb acompañante en el Diseñador de informes. Para más información sobre la implementación, vea [How to: Deploy a Data Processing Extension to Report Designer](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md) (Cómo implementar una extensión de procesamiento de datos en el Diseñador de informes).  
  
3.  Abra un nuevo proyecto de informe en [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] al tiempo que deja el código de la extensión de procesamiento de datos abierto en una ventana independiente de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
4.  Navegue a la ventana de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] que contenga el proyecto de extensión de procesamiento de datos y establezca algunos puntos de interrupción en el código.  
  
5.  Con el proyecto de extensión de procesamiento de datos en la ventana del proyecto activa, haga clic en **Asociar al proceso** desde el menú **Depurar**.  
  
     Se abre el cuadro de diálogo **Asociar al proceso**.  
  
6.  En la lista de procesos, seleccione el proceso devenv.exe que se corresponda con su proyecto de informe y haga clic en **Asociar**.  
  
7.  Defina el origen de datos del informe utilizando la pestaña **Datos de informe** del Proyecto de informe. Probablemente utilizará el Diseñador de consultas genérico para ejecutar una consulta con el origen de datos personalizado. De esta forma se debería invocar el depurador y ejecutar el código correspondiente a sus puntos de interrupción.  
  
8.  Recorra el código con la tecla F11. Para obtener más información sobre cómo utilizar [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] para la depuración, vea la documentación de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Implementación de una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
