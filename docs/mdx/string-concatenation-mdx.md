---
title: + (Concatenación de cadenas) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4d5f2316e3af5ce3c925ef71e1da5baf5bab868d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036852"
---
# <a name="-string-concatenation-mdx"></a>+ (Concatenación de cadenas) (MDX)


  Realiza una operación de cadena que concatena dos o más cadenas de caracteres, tuplas o una combinación de cadenas y tuplas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *String_Expression*  
 Una expresión multidimensional (MDX) válida que devuelve un valor de cadena.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor con el tipo de datos del parámetro que tiene mayor precedencia.  
  
## <a name="remarks"></a>Comentarios  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si una expresión se evalúa como un valor NULL, el operador devuelve el resultado de la otra expresión.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
