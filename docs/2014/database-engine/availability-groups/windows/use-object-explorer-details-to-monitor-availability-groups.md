---
title: Utilice los detalles del explorador de objetos para supervisar los grupos de disponibilidad (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.OEdetails.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: 84affc47-40e0-43d9-855e-468967068c35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5545b36aba250a04744b66abad5434f8573c053e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788328"
---
# <a name="use-the-object-explorer-details-to-monitor-availability-groups-sql-server-management-studio"></a>Usar los detalles del Explorador de objetos para supervisar los grupos de disponibilidad (SQL Server Management Studio)
  En este tema se describe cómo se usa el panel **Detalles del Explorador de objetos** de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para supervisar y administrar grupos de disponibilidad AlwaysOn, réplicas de disponibilidad y bases de datos de disponibilidad existentes.  
  
> [!NOTE]  
>  Para obtener información sobre cómo usar el panel Detalles del Explorador de objetos, vea [Panel de detalles del Explorador de objetos](../../../ssms/object/object-explorer-details-pane.md).  
  
-   **Antes de empezar:**  [Requisitos previos](#Prerequisites)  
  
-   **Para supervisar un grupo de disponibilidad, utilizando:**  [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Detalles del Explorador de objetos:**  
  
     [Detalles de grupos de disponibilidad](#AvGroupsDetails)  
  
     [Detalles de la réplica de disponibilidad](#AvReplicaDetails)  
  
     [Detalles de la base de datos de disponibilidad](#AvDbDetails)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe estar conectado a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instancia del servidor) que hospeda la réplica principal o una réplica secundaria.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para supervisar grupos de disponibilidad, réplicas de disponibilidad y bases de datos de disponibilidad**  
  
1.  En el menú Ver, haga clic en **Detalles del Explorador de objetos**o presione la tecla **F7** .  
  
2.  En el Explorador de objetos, conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que desea supervisar un grupo de disponibilidad y haga clic en el nombre del servidor para expandir el árbol.  
  
3.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
4.  El panel **Detalles del Explorador de objetos** muestra todos los grupos de disponibilidad para los que la instancia del servidor conectado hospeda una réplica. Para cada grupo de disponibilidad, la columna de **Instancia de servidor (principal)** muestra el nombre de la instancia de servidor que hospeda actualmente la réplica principal.  Para mostrar más información sobre un grupo de disponibilidad determinado, selecciónelo en el Explorador de objetos.  
  
5.  El panel **Detalles del Explorador de objetos** muestra a continuación los nodos **Réplicas de disponibilidad** y **Bases de datos de disponibilidad** para este grupo de disponibilidad:  
  
    -   Al expandir el nodo **Grupo de disponibilidad** en el Explorador de objetos y seleccionar el nodo **Réplicas de disponibilidad** , el panel **Detalles del Explorador de objetos** muestra información sobre cada una de las réplicas de disponibilidad del grupo. Para obtener más información, vea [Detalles de la réplica de disponibilidad](#AvReplicaDetails)más adelante en este tema.  
  
         Para realizar operaciones en varias réplicas de disponibilidad, selecciónelas y haga clic con el botón secundario en ellas para abrir un menú contextual que enumera los comandos disponibles.  
  
    -   Al expandir el nodo **Grupo de disponibilidad** en el Explorador de objetos y seleccionar el nodo **Bases de datos de disponibilidad** , el panel **Detalles del Explorador de objetos** muestra información sobre cada una de las bases de datos de disponibilidad del grupo. Para obtener más información, vea [Detalles de la base de datos de disponibilidad](#AvDbDetails)más adelante en este tema.  
  
         Para realizar operaciones en varias bases de datos de disponibilidad, selecciónelas y haga clic con el botón secundario en ellas para abrir un menú contextual que enumera los comandos disponibles.  
  
##  <a name="AvGroupsDetails"></a> Detalles de grupos de disponibilidad  
 La pantalla de detalles de **Grupos de disponibilidad** muestra las siguientes columnas:  
  
 **Name**  
 Enumera las carpetas de agentes de escucha de **Réplicas de disponibilidad**, **Bases de datos de disponibilidad**y **Grupo de disponibilidad** del grupo de disponibilidad seleccionado.  
  
##  <a name="AvReplicaDetails"></a> Detalles de la réplica de disponibilidad  
 La pantalla de detalles de **Réplica de disponibilidad** muestra las siguientes columnas:  
  
 **Instancia del servidor**  
 Muestra el nombre de la instancia de servidor que hospeda la réplica de disponibilidad, junto con un icono que indica el estado actual de la conexión de la instancia de servidor a la instancia de servidor local.  
  
 **Rol**  
 Indica el rol actual de la réplica de disponibilidad, **Principal** o **Secundaria**. Para más información sobre los roles de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
 **Modo de conexión en rol secundario**  
 Indica si las bases de datos de una réplica de disponibilidad determinada que está realizando el rol secundario (es decir, actuando como réplica secundaria) pueden aceptar conexiones de los clientes.  
  
 Los valores posibles son los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**No permitir conexiones**|No se permiten conexiones directas a las bases de datos de disponibilidad cuando esta réplica de disponibilidad está actuando como réplica secundaria. Las bases de datos secundarias no están disponibles para acceso de lectura.|  
|**Permitir solo conexiones de lectura**|Solo se permiten conexiones de solo lectura directas cuando esta réplica actúa como réplica secundaria. Todas las bases de datos de la réplica están disponibles para acceso de lectura.|  
|**Permitir todas las conexiones**|Se permiten todas las conexiones a estas bases de datos para acceso de solo lectura cuando esta réplica actúa como réplica secundaria.|  
  
 **Estado de conexión**  
 Indica si la réplica secundaria está conectada actualmente a la réplica principal. Los valores posibles son los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Desconectado**|En el caso de una réplica de disponibilidad remota, indica que está desconectada de la réplica de disponibilidad local. La respuesta de la réplica local al estado Desconectado depende de su rol, del siguiente modo:<br /><br /> En la réplica principal, si una réplica secundaria está desconectada, las bases de datos secundarias se marcan como **No sincronizadas** en la réplica principal y la réplica principal espera a que la réplica secundaria vuelva a conectarse.<br /><br /> En la réplica secundaria, cuando detecta que está desconectada, intenta volver a conectarse a la réplica principal.|  
|**Conectado**|Una réplica de disponibilidad remota que está conectada actualmente a la réplica local.|  
|**NULL**|Si la réplica local es una réplica secundaria, este valor es NULL para las demás réplicas secundarias.|  
  
 **Estado de sincronización**  
 Indica si una réplica secundaria está sincronizada actualmente con la réplica principal. Los valores posibles son los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**No sincronizadas**|La base de datos no está sincronizada o no se ha unido todavía al grupo de disponibilidad.|  
|**Sincronizado**|La base de datos está sincronizada con la base de datos principal en la réplica principal actual, si existe, o en la última réplica principal.<br /><br /> Nota: En el modo de rendimiento, la base de datos nunca está en estado Synchronized.|  
|**NULL**|Estado desconocido. Este valor aparece cuando la instancia del servidor local no puede comunicarse con el clúster de conmutación por error de WSFC (es decir, el nodo local no forma parte del quórum de WSFC).|  
  
> [!NOTE]  
>  Para obtener más información sobre los contadores de rendimiento para réplicas de disponibilidad, vea [SQL Server, réplica de disponibilidad](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbDetails"></a> Detalles de la base de datos de disponibilidad  
 La pantalla de detalles de **Base de datos de disponibilidad** muestra las siguientes propiedades de las bases de datos de disponibilidad de un grupo de disponibilidad determinado:  
  
 **Name**  
 El nombre de la base de datos de disponibilidad.  
  
 **Estado de sincronización**  
 Indica si la base de datos de disponibilidad está sincronizada actualmente con la réplica principal.  
  
 Los estados posibles de sincronización son los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Sincronizando|La base de datos secundaria ha recibido las entradas del registro de transacciones de la base de datos principal no escritas todavía en el disco (protegido).<br /><br /> Nota: En el modo de confirmación asincrónica, el estado de sincronización siempre es **Synchronizing**.|  
  
 **Suspendida**  
 Indica si la base de datos de disponibilidad está actualmente en línea. Los valores posibles son los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Suspendida**|Este estado indica que la base de datos está suspendida localmente y necesita ser reanudada manualmente.<br /><br /> En la réplica principal, el valor no es confiable para una base de datos secundaria. Para determinar de forma confiable si una base de datos secundaria está suspendida, consúltela en la réplica secundaria que hospeda la base de datos.|  
|**Sin unir**|Indica que la base de datos secundaria no se ha unido al grupo de disponibilidad o se ha quitado del grupo.|  
|**En línea**|Indica que la base de datos no está suspendida en la réplica de disponibilidad local y que la base de datos está conectada.|  
|**Sin conectar**|Indica que la réplica secundaria no se puede conectar actualmente a la réplica principal.|  
  
> [!NOTE]  
>  Para obtener información sobre los contadores de rendimiento para las bases de datos de disponibilidad, vea [SQL Server, réplica de base de datos](../../../relational-databases/performance-monitor/sql-server-database-replica.md).  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Utilice el panel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)   
 [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
  
