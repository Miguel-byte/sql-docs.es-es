---
title: Herramientas para supervisar grupos de disponibilidad
description: 'Una referencia de las diversas herramientas disponibles para supervisar el rendimiento y el mantenimiento de los grupos de disponibilidad Always On. '
ms.custom: seodec18
ms.date: 06/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31cf3fcc59ad9dbe694b7a11f6b90981f37fc78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014670"
---
# <a name="tools-to-monitor-always-on-availability-groups"></a>"Herramientas para supervisar grupos de disponibilidad Always On"
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para supervisar las propiedades y el estado de un grupo de disponibilidad AlwaysOn, puede usar las siguientes herramientas.  
  
|Herramienta|Descripción breve|Vínculos|  
|----------|-----------------------|-----------|  
|Paquete de supervisión de System Center para SQL Server|El paquete de supervisión de SQL Server (SQLMP) es la solución recomendada para supervisar los grupos de disponibilidad y las bases de datos de disponibilidad y de replicación de disponibilidad para los administradores TIC. Entre las características de supervisión que son de particular importancia para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se incluyen las siguientes:<br /><br /> La detectabilidad automática de los grupos de disponibilidad, las réplicas de disponibilidad y la base de datos de disponibilidad entre cientos de equipos. Esto le permite realizar fácilmente el seguimiento del inventario de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Alertas y vales de System Center Operations Manager (SCOM). Estas características proporcionan un conocimiento detallado que permite una resolución más rápida de un problema.<br /><br /> Una extensión personalizada de la supervisión del estado de AlwaysOn mediante la administración basada en directivas (PBM).<br /><br /> El estado abarca desde las bases de datos de disponibilidad a las réplicas de disponibilidad.<br /><br /> Tareas personalizadas que administran [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] desde la consola de System Center Operations Manager.|Para descargar el módulo de supervisión (SQLServerMP.msi) y la *Guía del módulo de administración de SQL Server para System Center Operations Manager* (SQLServerMPGuide.doc), vea:<br /><br /> [Paquete de supervisión de System Center para SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] proporcionan una gran cantidad de información sobre los grupos de disponibilidad y las réplicas, bases de datos, escuchas y el entorno de clúster de WSFC.|[Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|El panel **Detalles del Explorador de objetos** muestra información básica acerca de los grupos de disponibilidad hospedados en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que está conectado.<br /><br /> **\*\* Sugerencia \*\*** Use este panel para seleccionar varios grupos, réplicas o bases de datos de disponibilidad y para realizar tareas administrativas rutinarias en los objetos seleccionados; por ejemplo, quitar de un grupo de disponibilidad varias réplicas o bases de datos de disponibilidad.|[Usar los detalles del Explorador de objetos para supervisar los grupos de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Los cuadros de diálogo**Propiedades** permiten ver las propiedades de los grupos de disponibilidad, las réplicas o los agentes de escucha y, en algunos casos, para cambiar la configuración.|-   [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)<br />-   [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)<br />-   [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)|  
|Monitor de sistema|El objeto de rendimiento **SQLServer:Availability Replica** contiene contadores de rendimiento que proporcionan información sobre las réplicas de disponibilidad.|[SQL Server, réplica de disponibilidad](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor de sistema|El objeto de rendimiento **SQLServer:Database Replica** contiene contadores de rendimiento que proporcionan información sobre las bases de datos secundarias en una réplica secundaria dada.<br /><br /> El objeto **SQLServer:Databases** de SQL Server contiene contadores de rendimiento que supervisan las actividades del registro de transacciones, entre otras cosas. Los siguientes contadores son especialmente importantes para supervisar la actividad de registro de transacciones en bases de datos de disponibilidad: **Tiempo de escritura de vaciados de registros (ms)** , **Vaciados de registro/s.** , **Errores de caché del grupo de registros/s.** , **Lecturas de disco del grupo de registros/s** y **Solicitudes del grupo de registros/s**.|[SQL Server, réplica de base de datos](../../../relational-databases/performance-monitor/sql-server-database-replica.md) y [SQL Server, objeto Databases](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Modelo de estado AlwaysOn, parte 1: arquitectura del modelo de estado](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/08/the-alwayson-health-model-part-1-health-model-architecture/)  
  
     [Modelo de estado de AlwaysOn, parte 2: extender el modelo de estado](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/)  
  
     [Supervisión del estado de Always On con PowerShell, parte 1: Información general básica de los cmdlets](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
     [Supervisión del estado de Always On con PowerShell, parte 2: Uso avanzado de cmdlets](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
     [Supervisión del estado de Always On con PowerShell, parte 3: Una sencilla aplicación de supervisión](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
     [Supervisión del estado de Always On con PowerShell, parte 4: Integración con el Agente SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
     [Blogs del equipo de Always On de SQL Server: el blog oficial del equipo de Always On de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.microsoft.com/psssql/)  
  
-   **Notas del producto:**  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Reparación de página automática &#40;grupos de disponibilidad: creación de reflejo de la base de datos&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
