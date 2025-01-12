---
title: Unorder, (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097260"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  Quita cualquier orden impuesto sobre un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **Unorder** función quita cualquier ordenación impuesta en las tuplas contenidas en el conjunto por cualquier otra función o instrucción, como el [orden](../mdx/order-mdx.md) función. El orden de las tuplas en el conjunto devuelto por la **Unorder** función es indeterminado.  
  
 El **Unorder** función se utiliza como una sugerencia para optimizar la consulta para el procesamiento de conjunto. Si el orden de las tuplas de un conjunto no es significativo en una consulta o cálculo, utilizando el **Unorder** función puede proporcionar una mejora del rendimiento en estos casos. Por ejemplo, el [NonEmpty (MDX)](../mdx/nonempty-mdx.md) función puede funcionar mejor cuando el conjunto especificado a esta función está ordenado que si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tiene que conservar el orden, aunque con [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], el procesador de consultas intenta realizar Esta función automáticamente para muchas funciones, como **suma** y **agregado**. La ventaja de rendimiento de usar **Unorder** es probable que sea notable en los conjuntos muy grandes que constan de millones de tuplas.  
  
## <a name="example"></a>Ejemplo  
 El siguiente pseudocódigo muestra la sintaxis de esta función.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
