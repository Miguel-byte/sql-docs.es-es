---
title: srv_sendrow (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_sendrow
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_sendrow
ms.assetid: a08f608a-10e6-4bff-9b48-0d02e8026cdb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f39355222b491be27cc1b914401dcc459151e4bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62718062"
---
# <a name="srv_sendrow-extended-stored-procedure-api"></a>srv_sendrow (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Transmite una fila de datos al cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_sendrow ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la solicitud de idioma). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido utiliza para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Se llama a la función **srv_sendrow** una vez por cada fila enviada al cliente. Todas las filas se deben enviar al cliente antes de se envíe cualquier mensaje, valor de estado o estado de finalización con **srv_sendmsg**, **srv_status**o **srv_senddone**.  
  
 El envío de una fila en la que no se han definido todas sus columnas con **srv_describe** hace que la aplicación API Procedimiento almacenado extendido provoque un mensaje de error informativo y devuelva FAIL al cliente. En este caso, la fila no se envía.  
  
> [!NOTE]  
>  La API Procedimiento almacenado extendido no permite enviar las filas de cálculo al cliente. Además, si se envía al cliente una fila que contiene datos `ntext`, `text` o `image`, no se incluyen el puntero de texto ni la marca de tiempo del texto.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_describe &#40;API de procedimiento almacenado extendido&#41;](srv-describe-extended-stored-procedure-api.md)  
  
  
