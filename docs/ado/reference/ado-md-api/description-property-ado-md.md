---
title: Descripción (propiedad, ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5636b5f4e49ff9a5bbe46937a8d7b972e61b4502
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938573"
---
# <a name="description-property-ado-md"></a>Description (propiedad) (ADO MD)
Devuelve un texto de explicación del objeto actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Para [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos, **descripción** se aplica únicamente a medida y fórmulas. **Descripción** devuelve una cadena vacía ("") para todos los demás tipos de miembros. Para obtener más información sobre los distintos tipos de miembros, vea el [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propiedad.  
  
 Esta propiedad solo se admite en **miembro** objetos que pertenecen a un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Se produce un error cuando se hace referencia a esta propiedad desde **miembro** objetos que pertenecen a un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
