---
title: Clase de eventos Broker:Forwarded Message Sent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 51784663fdfec66f851bed479184ae21170a3681
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664021"
---
# <a name="brokerforwarded-message-sent-event-class"></a>Broker:Forwarded Message Sent, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento Broker:Forwarded Message Sent cuando Service Broker reenvía un mensaje.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Forwarded Message Sent  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BigintData1|`bigint`|Número de secuencia de mensajes.|52|Sin|  
|ClientProcessID|`int`|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o identificador de la base de datos predeterminada si no se ha emitido la instrucción USE *database*para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos Server Name en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DBUserName|`nvarchar`|Identificador de la instancia de agente del servicio del que procede el mensaje.|40|No|  
|EventClass|`int`|Tipo de clase de eventos capturado. Siempre es 139 para Broker:Forwarded Message Sent.|27|No|  
|EventSequence|`int`|Número de secuencia de este evento.|51|Sin|  
|FileName|`nvarchar`|Nombre del servicio al que se destina el mensaje.|36|Sin|  
|GUID|`uniqueidentifier`|Id. de conversación del diálogo. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|Sin|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IndexID|`int`|Número de saltos que quedan para el mensaje reenviado.|24|Sin|  
|IntegerData|`int`|Número de fragmento del mensaje reenviado.|25|No|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|No|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|ObjectId|`int`|Valor de período de vida del mensaje reenviado cuando se reenvió.|22|Sin|  
|ObjectName|`nvarchar`|Identificador del mensaje reenviado.|34|Sin|  
|OwnerName|`nvarchar`|Identificador de agente al que se dirige el mensaje.|37|Sin|  
|RoleName|`nvarchar`|Rol del identificador de conversación. Una de las siguientes opciones:<br /><br /> Initiator. Este agente inició la conversación.<br /><br /> Target. Este agente es el destino de la conversación.|38|Sin|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|SPID|`int`|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|Correcto|`int`|Tiempo transcurrido durante el proceso de reenvío.|23|Sin|  
|TargetLoginName|`nvarchar`|Dirección de red a la que esta instancia envió el mensaje. Tenga en cuenta que puede ser distinta del destino final del mensaje.|42|Sin|  
|TargetUserName|`nvarchar`|Nombre del servicio que ha iniciado el mensaje.|39|Sin|  
|TransactionID|`bigint`|Identificador de la transacción asignado por el sistema.|4|Sin|  
  
  
