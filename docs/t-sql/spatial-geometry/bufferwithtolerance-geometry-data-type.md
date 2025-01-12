---
title: BufferWithTolerance (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9d8b500415aa5e6812524fff6403735a11cf765a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017537"
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un objeto geométrico que representa la unión de todos los valores de puntos cuya distancia desde una instancia de **geometry** es menor o igual que un valor especificado, lo que posibilita una tolerancia especificada.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 Es una expresión **float** que especifica la distancia desde la instancia de **geometry** en torno a la que se va a calcular el búfer.  
  
 *tolerance*  
 Es una expresión **float** que especifica la tolerancia de la distancia del búfer.  
  
 *Tolerance* hace referencia a la variación máxima en la distancia de búfer ideal para la aproximación lineal devuelta.  
  
 Por ejemplo, la distancia de búfer ideal de un punto es un círculo, pero un círculo debe conseguirse de forma aproximada mediante un polígono. Cuanto más pequeña sea la tolerancia, más puntos tendrá el polígono, lo que aumenta la complejidad del resultado, pero disminuye el error.  
  
 *relative*  
 Es un valor **bit** que especifica si el valor *tolerance* es relativo o absoluto. Si es TRUE o 1, la tolerancia es relativa y se calcula como el producto del parámetro *tolerance* por el diámetro del cuadro de límite de la instancia. Si es FALSE o 0, la tolerancia es absoluta y el valor *tolerance* es la variación máxima absoluta en la distancia del búfer ideal para la aproximación lineal devuelta.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Excepciones  
 El parámetro *tolerance* debe ser mayor que cero. Si *tolerance* <= 0, se produce una excepción `System.ArgumentOutOfRangeException`.  
  
> [!NOTE]  
>  Puesto que *tolerance* es un tipo **float**, se puede generar una excepción `System.Runtime.InteropServices.COMException` si el valor dado para la tolerancia es muy pequeño, debido a problemas de redondeo con los tipos de punto flotante.  
  
## <a name="remarks"></a>Notas  
 Cuando *distance* > 0, se devuelve una instancia de **Polygon** o **MultiPolygon**.  
  
> [!NOTE]  
>  Dado que la distancia es **float**, un valor sumamente pequeño puede igualarse a cero en los cálculos. Cuando ocurre esto, se devuelve una copia de la instancia de **geometry** que llama. Vea [float y real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Cuando *distance* = 0, se devuelve una copia de la instancia de **geometry** que llama.  
  
 Cuando *distance* < 0:  
  
-   Se devuelve una instancia de **GeometryCollection** vacía si las dimensiones de la instancia son 0 o 1.  
  
-   Se devuelve un búfer negativo si las dimensiones de la instancia son dos o más.  
  
    > [!NOTE]  
    >  Un búfer negativo también puede crear una instancia de **GeometryCollection** vacía.  
  
 Un búfer negativo quita todos los puntos que se encuentran dentro de la distancia especificada del límite de la instancia de **geometry**.  
  
 El error entre el búfer teórico y el calculado es max(tolerance, extents \* 1.E-7), donde tolerance es el valor del parámetro *tolerance*. Para más información sobre las extensiones, vea la [referencia del método del tipo de datos geometry](https://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` y se usa `BufferWithTolerance()` para obtener un búfer aproximado a su alrededor.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [STBuffer &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

