---
title: GetChildren (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84f1a2f7a80e17571f1b8ad3e63db640fb58dc19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932503"
---
# <a name="getchildren-method-ado"></a>GetChildren (método) (ADO)
Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) cuyas filas representan los elementos secundarios de una colección [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **Recordset** para el que cada fila representa un elemento secundario del elemento actual del objeto **registro** objeto. Por ejemplo, los elementos secundarios de un **registro** que representa un directorio serían los archivos y subdirectorios contenidos en el directorio primario.  
  
## <a name="remarks"></a>Comentarios  
 El proveedor determina qué columnas hay en el valor devuelto **Recordset**. Por ejemplo, un proveedor de código fuente de documentos siempre devuelve un recurso **Recordset**.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
