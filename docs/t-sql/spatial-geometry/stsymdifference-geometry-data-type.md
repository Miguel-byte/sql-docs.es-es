---
title: STSymDifference (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ea26c364621910d6dd5148a5753bd6709d3e0f07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066286"
---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un objeto que representa todos los puntos que están en una instancia de **geometry** o en otra instancia de **geometry**, pero no los puntos que pertenecen a ambas instancias.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 Es la otra instancia de **geometry** además de la instancia en la que se invoca `STSymDistance()`.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
 Este método siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geometry**. El resultado puede contener segmentos de arco circulares solo si las instancias de entrada contienen segmentos de arco circulares.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. Calcular la diferencia simétrica entre dos instancias de Polygon  
 En el ejemplo siguiente se utiliza `STSymDifference()` para calcular la diferencia simétrica entre dos instancias de `Polygon`.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. Calcular la diferencia simétrica entre una instancia de CurvePolygon y una instancia de Polygon  
 En el siguiente ejemplo se devuelve un objeto `GeometryCollection` que representa la diferencia simétrica entre un objeto `CurvePolygon` y un objeto `Polygon`.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. Usar STSymDifference () en una instancia de CurvePolygon con una instancia de Polygon inscrita  
 En el siguiente ejemplo se devuelve una instancia de `CurvePolygon` con un anillo `Polygon` interior que representa la diferencia simétrica entre las dos instancias comparadas.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
