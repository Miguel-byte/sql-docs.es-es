---
title: '&lt;consulta&gt; de datos de origen | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e523d33da502a971b950e33ec0bd935149ed26f7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892343"
---
# <a name="ltsource-data-querygt"></a>&lt;consulta de datos de origen&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Para entrenar un modelo de minería de datos y crear predicciones a partir de un modelo de minería de datos, tiene que tener [!INCLUDE[msCoName](../includes/msconame-md.md)] acceso a los datos externos a la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos. Utilice la \<cláusula de > de consultas de datos de origen en extensiones de minería de datos (DMX) para definir estos datos externos. La [instrucción INSERT &#40;into&#41;DMX](../dmx/insert-into-dmx.md), [SELECT &#60;from&#62; Model PREDICT &#40;join&#41;DMX](../dmx/select-from-model-prediction-join-dmx.md)y [Select from natural PREDICT join](../dmx/select-from-model-prediction-join-dmx.md) statements All use **\<Source Data Query >** .  
  
## <a name="query-types"></a>Tipos de consulta  
 Las tres formas más habituales de especificar datos de origen son:  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 Esta instrucción consulta datos externos a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usando un origen de datos existente.  
  
 Aunque **OPENQUERY** es similar en función a **OPENROWSET**, **OPENQUERY** tiene las siguientes ventajas:  
  
-   Una consulta DMX es mucho más fácil de escribir con **OPENQUERY**. En lugar de crear una nueva cadena de conexión cada vez que se escribe una consulta, puede aprovechar la cadena de conexión existente del origen de datos. El objeto de origen de datos también puede controlar el acceso a datos para usuarios individuales.  
  
-   El administrador dispone de más control sobre el modo de acceso a los datos del servidor. Por ejemplo, el administrador puede administrar los proveedores que se cargan en el servidor y los datos externos a los que se puede obtener acceso.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 Esta instrucción consulta datos externos a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usando un origen de datos existente.  
  
 [FORMA &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 Esta instrucción consulta varios orígenes de datos para crear una tabla anidada. Mediante el uso de **Shape**, puede combinar datos de varios orígenes en una sola tabla jerárquica. Esto le permite aprovechar la capacidad de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de anidar tablas incrustando una tabla dentro de otra tabla.  
  
 Para especificar los datos de origen, también puede usar las siguientes opciones:  
  
-   Cualquier instrucción DMX válida  
  
-   Cualquier instrucción MDX (Expresiones multidimensionales) válida  
  
-   Una tabla que devuelve un procedimiento almacenado  
  
-   Un conjunto de filas de XML for Analysis (XMLA)  
  
-   Un parámetro de conjunto de filas  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [Tablas &#40;anidadas Analysis Services: minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
