---
title: YEAR (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e677a4a0c36f52ae62dfc06cd597ad5401fc8e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768701"
---
# <a name="year-ssis-expression"></a>YEAR (expresión de SSIS)
  Devuelve un entero que representa la parte del año de una fecha.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 Fecha con cualquier formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentarios  
 YEAR devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente en uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
 Utilizar la función YEAR es más sencillo pero equivalente a utilizar la función DATEPART("Year", date).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el número del año de un literal de fecha. Si la fecha tiene el formato mm/dd/aaaa, este ejemplo devuelve "2002".  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el año en la columna **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el año de la fecha actual.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>Vea también  
 [DATEADD &#40;expresión de SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](month-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
