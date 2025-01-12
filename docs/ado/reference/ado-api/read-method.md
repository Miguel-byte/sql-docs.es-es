---
title: Método Read | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 992631b8fb3864b6d7404f86d2f65de222f0b1c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917415"
---
# <a name="read-method"></a>Método Read
Lee un número especificado de bytes de un archivo binario [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumBytes*  
 Opcional. Un **largo** valor que especifica el número de bytes que se leen desde el archivo o la [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor **adReadAll**, que es el valor predeterminado.  
  
## <a name="return-value"></a>Valor devuelto  
 El **lectura** método lee un número especificado de bytes o toda la secuencia desde un **Stream** objeto y devuelve los datos resultantes como un **Variant**.  
  
## <a name="remarks"></a>Comentarios  
 Si *NumBytes* es mayor que el número de bytes restante en el **Stream**, se devuelven solo los bytes restantes. No se rellenan los datos de lectura para que coincida con la longitud especificada por *NumBytes*. Si no hay ningún byte para leer, se devuelve una variante con un valor null. **Lectura** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  *NumBytes* siempre mide los bytes. Para el texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**), utilice [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
