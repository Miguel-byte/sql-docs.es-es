---
title: Sys.availability_group_listeners (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listeners_TSQL
- sys.availability_group_listeners
- sys.availability_group_listeners_TSQL
- availability_group_listeners
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_group_listeners catalog view
- Availability Groups [SQL Server], listeners
ms.assetid: b5e7d1fb-3ffb-4767-8135-604c575016b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b363e410f35eb7880933520dd1dbf47f258b651e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041062"
---
# <a name="sysavailabilitygrouplisteners-transact-sql"></a>sys.availability_group_listeners (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Para cada grupo de disponibilidad AlwaysOn, devuelve cero filas indicando que no hay ningún nombre de red asociado al grupo de disponibilidad, o devuelve una fila para cada configuración de escucha de grupo de disponibilidad en el clúster de clústeres de conmutación por error de Windows Server (WSFC). Esta vista muestra la configuración en tiempo real recopilada del clúster.  
  
> [!NOTE]  
>  Esta vista de catálogo no describe los detalles de una configuración IP, que se definió en el clúster de WSFC.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Id. de grupo de disponibilidad (**group_id**) desde [sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md).|  
|**listener_id**|**nvarchar(36)**|GUID del identificador de recursos del clúster.|  
|**dns_name**|**nvarchar(63)**|Nombre de red configurado (nombre de host) del agente de escucha del grupo de disponibilidad.|  
|**port**|**int**|Número de puerto TCP configurado para el agente de escucha del grupo de disponibilidad.<br /><br /> NULL = El agente de escucha se ha configurado fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y su número de puerto no se ha agregado al grupo de disponibilidad. Para agregar el puerto, Listener de la opción de modificar el agente de escucha de la [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**is_conformant**|**bit**|Si esta configuración IP es conforme; puede ser:<br /><br /> 1 = El agente de escucha es conforme. Existen sola relaciones "OR" entre sus direcciones de protocolo de Internet (IP). *Función* abarca cada una configuración IP que se creó el [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción. Además, si una configuración IP fue creada fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por ejemplo mediante el Administrador de clústeres de conmutación por error de WSFC, pero se puede modificar mediante la instrucción tsql ALTER AVAILABILITY GROUP, la configuración IP se califica como conforme.<br /><br /> 0 = El agente de escucha es no conforme. Normalmente, esto indica que una dirección IP que no pudo configurarse utilizando los comandos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se definió, sin embargo, directamente en el clúster de WSFC.|  
|**ip_configuration_string_from_cluster**|**nvarchar(max)**|Cadenas de configuración IP de clúster, si existen, para este agente de escucha. NULL = El agente de escucha no tiene direcciones IP virtuales. Por ejemplo:<br /><br /> Dirección IPv4: `65.55.39.10`.<br /><br /> Dirección IPv6: `2001::4898:23:1002:20f:1fff:feff:b3a3`|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
