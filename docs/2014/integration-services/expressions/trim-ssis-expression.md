---
title: TRIM (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- TRIM function
- trailing blanks
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 59d7eb92d79aa77da3faded36036de4b14142c93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896527"
---
# <a name="trim-ssis-expression"></a>TRIM (expresión de SSIS)
  Devuelve una expresión de caracteres después de quitar los espacios iniciales y finales.  
  
> [!NOTE]  
>  TRIM no quita los caracteres de espacio en blanco, como los caracteres de tabulación o de salto de línea. Unicode proporciona puntos de código para muchos tipos distintos de espacios, pero su función solo reconoce el punto de código Unicode 0x0020. Cuando se convierten cadenas del juego de caracteres de doble byte (DBCS) a Unicode, éstas pueden incluir caracteres de espacio distintos de 0x0020 y la función no puede eliminarlos. Para eliminar cualquier tipo de espacio, puede utilizar el método Trim de Microsoft Visual Basic .NET en un script ejecutado desde el componente Script.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TRIM(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que puede quitar espacios.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 TRIM devuelve un resultado NULL si el valor del argumento es NULL.  
  
 TRIM solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que TRIM realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo quita los espacios iniciales y finales de un literal de cadena. El resultado devuelto es "New York".  
  
```  
TRIM("   New York   ")  
```  
  
 Este ejemplo quita los espacios iniciales y finales del resultado de concatenar las columnas **FirstName** y **LastName** . La cadena vacía entre **FirstName** y **LastName** no se quita.  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## <a name="see-also"></a>Vea también  
 [LTRIM &#40;expresión de SSIS&#41;](trim-ssis-expression.md)   
 [RTRIM &#40;expresión de SSIS&#41;](rtrim-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
