---
title: Celdas del cubo (Analysis Services datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d9ca444c4e889c68f90abf4cf76c07d1c2d574a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887914"
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Celdas de cubos (Analysis Services - Datos multidimensionales)
  Un cubo se compone de celdas organizadas por grupos de medida y dimensiones. Una celda representa la intersección lógica única de un miembro de cada dimensión del cubo en el mismo. Por ejemplo, el cubo que se describe en el siguiente diagrama contiene un grupo de medida con dos medidas, organizadas en tres dimensiones llamadas Source, Route y Time.  
  
 ![Diagrama de cubo que identifica una sola celda](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro5.gif "Diagrama de cubo que identifica una sola celda")  
  
 La celda sombreada única del diagrama es la intersección de los siguientes miembros:  
  
-   El miembro air de la dimensión Route.  
  
-   El miembro Africa de la dimensión Source.  
  
-   El miembro 4th quarter de la dimensión Time.  
  
-   La medida Packages.  
  
## <a name="leaf-and-nonleaf-cells"></a>Celdas hoja y no hoja  
 El valor de una celda en un cubo se puede obtener de varias formas. En el ejemplo anterior, el valor de la celda se puede recuperar directamente de la tabla de hechos del cubo, ya que todos los miembros que se usan para identificar esa celda son *miembros hoja*. Un miembro hoja no tiene miembros secundarios, jerárquicamente hablando, y normalmente hace referencia a un solo registro de una tabla de dimensiones. Este tipo de celda se conoce como *celda hoja*.  
  
 Sin embargo, una celda también puede identificarse mediante el uso de *miembros no hoja*. Un miembro no hoja es un miembro que tiene uno o más miembros secundarios. En este caso, el valor de la celda se deriva normalmente de la agregación de miembros secundarios asociados al miembro no hoja. Por ejemplo, la intersección de los siguientes miembros y dimensiones hace referencia a una celda cuyo valor suministra la agregación:  
  
-   El miembro air de la dimensión Route.  
  
-   El miembro Africa de la dimensión Source.  
  
-   El miembro 2nd half de la dimensión Time.  
  
-   El miembro Packages.  
  
 El miembro 2nd half de la dimensión Time es un miembro no hoja. Por lo tanto, todos los valores asociados a él deben ser valores agregados, como se muestra en el siguiente diagrama.  
  
 ![celdas 3rd y 4th Quarter para la segunda mitad del miembro](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro6.gif "celdas 3rd y 4th Quarter para la segunda mitad del miembro")  
  
 Si consideramos que las agregaciones de los miembros 3rd quarter y 4th quarter son sumas, el valor de la celda especificada es 400, que es el total de todas las celdas hoja sombreadas del diagrama anterior. Dado que el valor de la celda se deriva de la agregación de otras celdas, la celda especificada se considera una *celda no hoja*.  
  
 Los valores de celdas derivados para miembros que utilizan grupos de miembros y resúmenes personalizados, además de miembros personalizados, se controlan de la misma manera. Sin embargo, los valores de celdas derivados para miembros calculados se basan totalmente en la expresión MDX (Expresiones multidimensionales) utilizada para definir el miembro calculado; en algunos casos, puede que no intervenga ningún dato de celda real. Para obtener más información, vea [operadores de resúmenes personalizados en dimensiones](../multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md)de elementos primarios y secundarios, [definir fórmulas de miembro personalizado](../multidimensional-models/attribute-properties-define-custom-member-formulas.md)y [cálculos](../multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Celdas vacías  
 No es necesario que todas las celdas de un cubo contengan un valor; puede haber intersecciones del cubo sin datos. Estas intersecciones, denominadas celdas vacías, se dan con frecuencia en los cubos debido a que no todas las intersecciones de un atributo de dimensión con una medida de un cubo contienen un registro correspondiente en una tabla de hechos. La relación entre las celdas vacías de un cubo y el número total de celdas de un cubo suele denominarse *dispersión* de un cubo.  
  
 Por ejemplo, la estructura del cubo que aparece en el siguiente diagrama es parecida a otros ejemplos de este tema. Sin embargo, en este ejemplo, no existían embarques aéreos a Africa en el tercer trimestre (3rd quarter) o a Australia en el cuarto (4th quarter). No existen datos en la tabla de hechos que admitan las intersecciones de estas dimensiones y medidas, por lo que las celdas de estas intersecciones están vacías.  
  
 ![Diagrama de cubo que identifica celdas vacías](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro7.gif "Diagrama de cubo que identifica celdas vacías")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una celda vacía es una celda que tiene cualidades especiales. Como las celdas vacías pueden sesgar los resultados de combinaciones cruzadas, recuentos, etc. muchas funciones de MDX proporcionan la capacidad de omitir las celdas vacías para los cálculos. Para obtener más información, vea [referencia &#40;MDX&#41; de expresiones multidimensionales](/sql/mdx/multidimensional-expressions-mdx-reference)y [conceptos clave de &#40;Analysis Services&#41;MDX](../multidimensional-models/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Seguridad  
 El acceso a los datos de las celdas se administra en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el nivel de rol y se puede controlar con precisión mediante el uso de expresiones MDX. Para obtener más información, vea [conceder acceso personalizado a &#40;datos&#41;de dimensión Analysis Services](../multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)y [conceder acceso personalizado &#40;a&#41;los datos de celda Analysis Services](../multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services de &#40;almacenamiento de cubos: datos multidimensionales&#41;](../multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Agregaciones y diseños de agregaciones](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
