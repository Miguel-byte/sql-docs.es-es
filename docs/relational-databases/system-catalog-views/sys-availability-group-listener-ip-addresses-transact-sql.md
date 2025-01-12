---
title: Sys.availability_group_listener_ip_addresses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listener_ip_addresses
- sys.availability_group_listener_ip_addresses
- availability_group_listener_ip_addresses_TSQL
- sys.availability_group_listener_ip_addresses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.availability_group_listener_ip_addresses catalog view
ms.assetid: e515fa6b-1354-4110-9b70-ab2e6164c992
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9c66e12ec326ba5021de0829b0d7cc479f858c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997589"
---
# <a name="sysavailabilitygrouplisteneripaddresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada dirección IP asociada a cualquier escucha de grupo de disponibilidad AlwaysOn del clúster de clústeres de conmutación por error de Windows Server (WSFC).  
  
 Clave principal: **listener_id** + **dirección_IP** + **ip_sub_mask**  
  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar(36)**|GUID de recurso del clúster de conmutación por error de Windows Server (WSFC).|  
|**ip_address**|**nvarchar(48)**|Dirección IP virtual configurada del agente de escucha del grupo de disponibilidad. Devuelve una sola dirección IPv4 o IPv6.|  
|**ip_subnet_mask**|**nvarchar(15)**|Máscara de subred de IP configurada para la dirección IPv4, si existe, que se configura para el agente de escucha del grupo de disponibilidad.<br /><br /> NULL = subred IPv6|  
|**is_dhcp**|**bit**|Si la dirección IP está configurada por DHCP, puede ser:<br /><br /> 0 = La dirección IP no está configurada por DHCP.<br /><br /> 1 = La dirección IP está configurada por DHCP|  
|**network_subnet_ip**|**nvarchar(48)**|Dirección IP de subred de red que especifica la subred a la que pertenece la dirección IP.|  
|**network_subnet_prefix_length**|**int**|Longitud de prefijo de subred de red de la subred a la que pertenece la dirección IP.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Máscara de subred de red de la subred a la que pertenece la dirección IP. **network_subnet_ipv4_mask** para especificar las opciones < network_subnet_option > de DHCP en una cláusula WITH DHCP de la [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) o [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.<br /><br /> NULL = subred IPv6|  
|**state**|**tinyint**|Estado ONLINE/OFFLINE de recursos IP del clúster de WSFC; puede ser:<br /><br /> 1 = En línea. El recurso de IP está en línea.<br /><br /> 0 = Sin conexión. El recurso de IP está sin conexión.<br /><br /> 2 = Pendiente en línea. El recurso de IP está sin conexión pero se está poniendo en línea.<br /><br /> 3 = error. El recurso de IP se estaba poniendo en línea pero sufrió un error.|  
|**state_desc**|**nvarchar(60)**|Descripción de **estado**, uno de:<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
