---
title: M (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1990361b643aee24f34e6b119f61595a450ceab4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127717"
---
# <a name="m-geography-data-type"></a>M (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Valor **M** (medida) de la instancia de **geography**. La semántica del valor de medida la define el usuario, pero normalmente describe la distancia en un linestring. Por ejemplo, el valor de medida se podría usar para realizar un seguimiento de los mojones a lo largo de una carretera.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.M  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 Si la instancia de **geography** no es de tipo **Point**, se asignará el valor null a esta propiedad, así como a cualquier instancia de **Point** para la que no se establezca dicha propiedad.  
  
 Esta propiedad es de solo lectura.  
  
 Los valores M no se usan en los cálculos realizados por la biblioteca y, por lo tanto, no se incluirán en ninguno de dichos cálculos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` con valores Z (elevación) y M (medida), y se usa `M` para capturar el valor `M` de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
