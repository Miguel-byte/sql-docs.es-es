---
title: "\"Agregar dirección IP\" en el cuadro de diálogo \"Nuevo agente de escucha del grupo de disponibilidad\""
description: 'Se describen las opciones del cuadro de diálogo "Agregar dirección IP" de la página "Especificar réplicas" en el "Asistente para grupo de disponibilidad" de SQL Server Management Studio. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 48b61a0f85d695f143f04f86387761170293a3b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935021"
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>Agregar dirección IP (cuadro de diálogo - SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema de Ayuda F1 se describen las opciones del cuadro de diálogo **Agregar dirección IP** . Se accede a este cuadro de diálogo desde el cuadro de diálogo **Nuevo agente de escucha del grupo de disponibilidad** y la pestaña **Escucha** de la página **Especificar réplicas** de [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] o [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de empezar a agregar subredes un agente de escucha del grupo de disponibilidad, asegúrese de que conoce la dirección IP para cada subred y, para una dirección IPv4, la máscara de subred.  
  
##  <a name="PageOptions"></a> Agregar las opciones de la dirección IP  
 **Subred**  
 Utilice la lista desplegable para seleccionar una dirección de la subred que va a agregar al agente de escucha del grupo de disponibilidad. De forma predeterminada, una subred posee una dirección IPv4 como una dirección IPv6. La primera vez que use el cuadro de diálogo **Agregar dirección IP** , la lista desplegable **Subred** mostrará las dos direcciones de subred para cada subred que hospeda una réplica para el grupo de disponibilidad. Para agregar una subred dada al agente de escucha, seleccione una de sus direcciones de subred.  
  
 Después de completar el cuadro de diálogo **Agregar dirección IP** y hacer clic en **Aceptar** para agregar una dirección de subred seleccionada al agente de escucha, la lista desplegable **Subred** filtrará la dirección de subred. Todas las direcciones de subred no seleccionadas permanecerán en la lista desplegable. Asegúrese de agregar una y solo una dirección de subred por subred al agente de escucha; de lo contrario, la creación del agente de escucha producirá un error.  
  
 **Direcciones**  
 Utilice este campo para escribir una dirección IP estática para la dirección de subred seleccionada. Póngase en contacto con su administrador de red para esta dirección IP. Asegúrese de escribir una dirección válida para la dirección de subred seleccionada; de lo contrario, la creación del agente de escucha producirá un error.  
  
 **Dirección IPv4**  
 Si ha seleccionado una dirección IPv4 de una subred, escriba aquí una dirección estática IPv4 válida.  
  
 **Máscara de subred**  
 Para una dirección IPv4, este campo de solo lectura muestra la máscara de subred de la subred seleccionada.  
  
 **Dirección IPv6**  
 Si ha seleccionado una dirección IPv6 de una subred, escriba aquí una dirección estática IPv6 válida.  
  
 **Aceptar**  
 Haga clic para agregar la subred cuya dirección ha seleccionado, junto con la dirección IP estática que ha especificado. Una fila con estos valores se agregará a la cuadrícula de subred del cuadro de diálogo **Nuevo agente de escucha del grupo de disponibilidad** o **Especificar réplicas** .  
  
> [!IMPORTANT]  
>  El cuadro de diálogo de **Agregar dirección IP** no comprueba la dirección IP. Tampoco impide agregar la segunda dirección de subred para una subred ya agregada al agente de escucha del grupo de disponibilidad.  
  
 **Cancelar**  
 Haga clic para cancelar las selecciones y volver al cuadro de diálogo **Nuevo agente de escucha de grupo de disponibilidad** o en la pestaña **Escucha** sin agregar una dirección IP estática para una subred.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Conectividad de cliente de AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
  
