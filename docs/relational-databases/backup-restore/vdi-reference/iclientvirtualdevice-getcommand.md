---
title: IClientVirtualDevice::GetCommand
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IClientVirtualDevice::GetCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a861377924b4bb3cc1c1d2a4b83eba660fbf99e0
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847596"
---
# <a name="iclientvirtualdevicegetcommand-vdi"></a>IClientVirtualDevice::GetCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **GetCommand** se usa para obtener el siguiente comando en cola en un dispositivo. Cuando se solicita, esta función espera el siguiente comando.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IClientVirtualDevice::GetCommand (
   DWORD               dwTimeOut,
   VDC_Command**      const ppCmd
);
```

## <a name="parameters"></a>Parámetros

*ppCmd* Cuando un comando se devuelve correctamente, el parámetro devuelve la dirección de un comando que se va a ejecutar. La memoria devuelta es de solo lectura. Cuando se completa el comando, este puntero se pasa a la rutina CompleteCommand. Para más información sobre cada comando, vea Comandos.

*dwTimeOut* El tiempo de espera, en milisegundos. Use INFINTE para esperar indefinidamente. Use 0 para sondear un comando. Se devuelve VD_E_TIMEOUT si no hay ningún comando disponible actualmente. Si se agota el tiempo de espera, el cliente decide la siguiente acción.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | Se ha capturado un comando. |
| VD_E_CLOSE | El servidor ha cerrado el dispositivo. |
| VD_E_TIMEOUT | No había ningún comando disponible y se agotó el tiempo de espera. |
| VD_E_ABORT | El cliente o el servidor han usado el elemento SignalAbort para forzar un apagado. |

## <a name="remarks"></a>Notas

Cuando se devuelve VD_E_CLOSE, SQL Server ha cerrado el dispositivo. Esto forma parte del apagado normal. Una vez cerrados todos los dispositivos, el cliente invoca IClientVirtualDeviceSet2::Close para cerrar el conjunto de dispositivos virtuales.

Cuando esta rutina debe bloquearse para esperar un comando, el subproceso se deja en una condición de alerta.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).