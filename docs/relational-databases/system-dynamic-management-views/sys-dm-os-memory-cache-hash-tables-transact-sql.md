---
title: Sys.dm_os_memory_cache_hash_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5a52fc7c614752cde43a1670f2fb299b35aa0ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265770"
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada caché activa en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_cache_hash_tables**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Dirección (clave principal) de la entrada de caché. No admite valores NULL.|  
|**name**|**nvarchar(256)**|Nombre de la caché. No admite valores NULL.|  
|**type**|**nvarchar(60)**|Tipo de caché. No admite valores NULL.|  
|**table_level**|**int**|Número de tabla de hash. Una caché concreta puede tener varias tablas hash que corresponden a diferentes funciones de hash. No admite valores NULL.|  
|**buckets_count**|**int**|Número de depósitos en la tabla de hash. No admite valores NULL.|  
|**buckets_in_use_count**|**int**|Número de depósitos que se utilizan actualmente. No admite valores NULL.|  
|**buckets_min_length**|**int**|Número mínimo de entradas de caché en un depósito. No admite valores NULL.|  
|**buckets_max_length**|**int**|Número máximo de entradas de caché en un depósito. No admite valores NULL.|  
|**buckets_avg_length**|**int**|Número promedio de entradas de caché en cada depósito. No admite valores NULL.|  
|**buckets_max_length_ever**|**int**|Número máximo de entradas de caché en un depósito de hash en esta tabla de hash desde que se inició el servidor. No admite valores NULL.|  
|**hits_count**|**bigint**|Proporción de aciertos de la caché. No admite valores NULL.|  
|**misses_count**|**bigint**|Número de errores de la caché. No admite valores NULL.|  
|**buckets_avg_scan_hit_length**|**int**|Número promedio de entradas examinadas en un depósito antes de haber encontrado la búsqueda de un elemento. No admite valores NULL.|  
|**buckets_avg_scan_miss_length**|**int**|Número promedio de entradas examinadas en un depósito antes de haber finalizado la búsqueda sin éxito. No admite valores NULL.|  
|**pdw_node_id**|**int**|El identificador para el nodo en esta distribución.<br /><br /> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permisos 

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   

## <a name="see-also"></a>Vea también  
 
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


