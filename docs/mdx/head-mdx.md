---
title: HEAD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906008"
---
# <a name="head-mdx"></a>Head (MDX)


  Devuelve el primer número de elementos especificado en un conjunto y retiene los duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
## <a name="remarks"></a>Comentarios  
 El **Head** función devuelve el número especificado de tuplas desde el principio del conjunto especificado. Se conserva el orden de los elementos. El valor predeterminado de Count es 1. Si el número especificado de tuplas es menor que 1, el **Head** función devuelve un conjunto vacío. Si el número especificado de tuplas supera al número de tuplas del conjunto, la función devuelve el conjunto original.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **Head** función se utiliza para devolver solo los 5 primeros conjuntos del resultado después de que el resultado se ordena mediante la **orden** función.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Elemento &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Elemento &#40;miembro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Rango &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
