---
title: Supervisión de la replicación con el Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b5d1a63937a11da4703ec4ef0338dee89a5c33f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667310"
---
# <a name="monitoring-replication-with-system-monitor"></a>Supervisar la replicación con el Monitor de sistema
  El Monitor de sistema de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows le permite utilizar gráficos, diagramas e informes para medir la eficacia del equipo, identificar y solucionar posibles problemas (como el uso desequilibrado de recursos, hardware insuficiente o diseño deficiente de programas), y planear necesidades de hardware adicionales. Para obtener más información, vea [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 El Monitor de sistema utiliza objetos y contadores de rendimiento que proporcionan información sobre el rendimiento de diversos procesos. Puede medir el rendimiento de la replicación a través de contadores asociados con los agentes de replicación:  
  
|Agente|Objeto de rendimiento|Contador|Descripción|  
|-----------|------------------------|-------------|-----------------|  
|Todos los agentes|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agentes de replicación|En ejecución|Número de agentes de replicación en ejecución actualmente.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantánea de replicación|Instantánea: Cmds entregados/s|Número de comandos por segundo entregados al distribuidor.|  
|Agente de instantáneas|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Instantánea de replicación|Instantánea: Transacciones entregadas/s|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Registro del log de replicación|Lector del registro: Cmds entregados/s|Número de comandos por segundo entregados al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Registro del log de replicación|Lector del registro: Transacciones entregadas/s|Número de transacciones por segundo entregadas al distribuidor.|  
|Agente de registro del LOG|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Registro del log de replicación|Lector del registro: Latencia de entrega|Tiempo, en milisegundos, que transcurre desde que se aplican las transacciones en el publicador hasta que se entregan al distribuidor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribución de duplicación|Dist: Cmds entregados/s|Número de comandos por segundo entregados al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribución de duplicación|Dist: Transacciones entregadas/s|Número de transacciones por segundo entregadas al suscriptor.|  
|Agente de distribución|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribución de duplicación|Dist: Latencia de entrega|Tiempo, en milisegundos, transcurrido desde que las transacciones se entregan al distribuidor hasta que se aplican en el suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Conflictos/seg.|Número de conflictos por segundo que ocurren durante el proceso de combinación.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Cambios descargados/seg.|Número de filas replicadas por segundo del publicador al suscriptor.|  
|Agente de mezcla|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Mezcla de replicación|Cambios cargados/seg.|Número de filas replicadas por segundo del suscriptor al publicador.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar &#40;replicación&#41;](../monitoring-replication.md)  
  
  
