---
title: Base de datos (categoría de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0d725f95fc8e9de0865ad895abd860d5f03687b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662933"
---
# <a name="database-event-category"></a>Base de datos (categoría de eventos)
  La categoría de evento **Base de datos** contiene clases de eventos para supervisar [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Data File Auto Grow (clase de eventos)](data-file-auto-grow-event-class.md)|Indica que el archivo de datos creció automáticamente. Este evento no se desencadena si se aumentó explícitamente el archivo de datos mediante ALTER DATABASE.|  
|[Data File Auto Shrink (clase de eventos)](data-file-auto-shrink-event-class.md)|Indica que se ha reducido el archivo de datos.|  
|[Database Mirroring: Connection (clase de eventos)](database-mirroring-connection-event-class.md)|Evento generado para informar del estado de una conexión de transporte para la creación de reflejo de la base de datos.|  
|[Database Mirroring State Change (clase de eventos)](database-mirroring-state-change-event-class.md)|Indica cuando cambia el estado de una base de datos reflejada.|  
|[Clase de eventos Database Suspect Data Page](database-suspect-data-page-event-class.md)|Indica cuando una página se agrega a la tabla **suspect_pages** en la base de datos **msdb** .|  
|[Log File Auto Grow (clase de eventos)](log-file-auto-grow-event-class.md)|Indica que el archivo de registro creció automáticamente. Este evento no se desencadena si el archivo de registro se aumentó explícitamente mediante ALTER DATABASE.|  
|[Log File Auto Shrink (clase de eventos)](log-file-auto-shrink-event-class.md)|Indica que el archivo de registro creció automáticamente. Este evento no se desencadena si el archivo de registro se reduce explícitamente mediante la instrucción ALTER DATABASE.|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)  
  
  
