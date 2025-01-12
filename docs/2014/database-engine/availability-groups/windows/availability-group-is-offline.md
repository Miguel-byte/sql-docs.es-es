---
title: Grupo de disponibilidad sin conexión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35d8f9cdda7c3b85c77d290f9c793640705438e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815441"
---
# <a name="availability-group-is-offline"></a>Grupo de disponibilidad sin conexión
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado en línea del grupo de disponibilidad|  
|**Problema**|El grupo de disponibilidad está sin conexión.|  
|**Categoría**|**Crítico**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva comprueba el estado en línea o sin conexión del grupo de disponibilidad. La directiva está en mal estado y se genera una alerta cuando el recurso de clúster del grupo de disponibilidad está sin conexión o no tiene una réplica principal.  
  
 El estado de la directiva es correcto cuando el recurso de clúster del grupo de disponibilidad está en línea y el grupo de disponibilidad tiene una réplica principal.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Grupo de disponibilidad sin conexión](https://go.microsoft.com/fwlink/p/?LinkId=220850) en TechNet Wiki.  
  
## <a name="possible-causes"></a>Posibles causas  
 Este problema se puede deber a un error en la instancia del servidor que hospeda la réplica principal o a que el recurso de grupo de disponibilidad del clúster de conmutación por error de Windows Server (WSFC) se ha quedado sin conexión. A continuación se indican las posibles causas de que el grupo de disponibilidad esté sin conexión:  
  
-   El grupo de disponibilidad no está configurado con el modo de conmutación automática por error. La réplica principal deja de estar disponible y el rol de todas las réplicas del grupo de disponibilidad es RESUELVE AFTER.  
  
    -   El servicio de instancia de la réplica principal está inactivo o no responde.  
  
    -   El grupo de disponibilidad tiene un problema de conectividad con el clúster.  
  
-   El grupo de disponibilidad está configurado con el modo de conmutación automática por error y no se completa correctamente.  
  
    -   Durante la conmutación automática por error, se produce un error en la comprobación de preparación principal en la réplica de destino, y no hay ninguna réplica disponible para convertirse en la nueva réplica principal.  
  
-   El recurso de grupo de disponibilidad del clúster se queda sin conexión.  
  
    -   Cualquier recurso de clúster dependiente encuentra un problema crítico y se queda sin conexión. El recurso de grupo de disponibilidad también está sin conexión hasta que el recurso dependiente vuelve a estar en línea.  
  
    -   Un problema crítico en el clúster desactiva el recurso de grupo de disponibilidad.  
  
-   Hay una conmutación por error automática, manual o forzada en curso para el grupo de disponibilidad.  
  
## <a name="possible-solutions"></a>Soluciones posibles  
 Las siguientes son posibles soluciones para este problema:  
  
-   Si la instancia de SQL Server de la réplica principal está inactiva, reinicie el servidor y compruebe que el grupo de disponibilidad se recupera en un estado correcto.  
  
-   Si parece que se ha producido un error en la conmutación automática por error, compruebe que las bases de datos de la réplica están sincronizadas con la réplica principal conocida y, a continuación, conmute por error a la réplica principal. Si las bases de datos no están sincronizadas, seleccione una réplica con una pérdida de datos mínima y, a continuación, recupere el modo de conmutación por error.  
  
-   Si el recurso del clúster está sin conexión mientras que las instancias de SQL Server parecen estar en buen estado, use el Administrador de clústeres de conmutación por error para comprobar el estado del clúster u otros problemas de clúster en el servidor. También puede usar el Administrador de clústeres de conmutación por error para intentar poner en línea el recurso de grupo de disponibilidad.  
  
-   Si hay una conmutación por error en curso, espere a que se complete.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
