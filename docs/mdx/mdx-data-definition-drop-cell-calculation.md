---
title: Instrucción DROP CELL CALCULATION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bccdd6efcf17af9d485e155b6653bab52bbcbd3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038218"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Definición de datos de MDX: DROP CELL CALCULATION


  Quita el cálculo de celda especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona el nombre de una expresión de cubo.  
  
 *CellCalc_Name*  
 Expresión de cadena válida que proporciona el nombre del cálculo de celda que se va a quitar.  
  
## <a name="see-also"></a>Vea también  
 [CREATE CELL CALCULATION &#40;Instrucción, MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
