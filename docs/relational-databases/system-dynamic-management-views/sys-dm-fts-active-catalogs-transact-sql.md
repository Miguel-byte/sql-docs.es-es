---
title: sys.dm_fts_active_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 31dd240f15d9d778cbab43f6b4b1bfda2e4e1857
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265966"
---
# <a name="sysdmftsactivecatalogs-transact-sql"></a>sys.dm_fts_active_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información de catálogos de texto completo que tienen alguna actividad de rellenado en progreso en el servidor.  
  
> [!NOTE]
>  Las columnas siguientes se quitará en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: is_paused, previous_status, previous_status_description, row_count_in_thousands, estado, status_description y worker_count. Evite el uso de estas columnas en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que las usan actualmente.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de la base de datos que contiene el catálogo de texto completo activo.|  
|**catalog_id**|**int**|Id. del catálogo de texto completo activo.|  
|**memory_address**|**varbinary(8)**|Dirección de búferes de memoria asignados para la actividad de llenado relacionada con este catálogo de texto completo.|  
|**name**|**nvarchar(128)**|Nombre del catálogo de texto completo activo.|  
|**is_paused**|**bit**|Indica si el llenado del catálogo de texto completo activo se ha pausado.|  
|**status**|**int**|Estado actual del catálogo de texto completo. Uno de los siguientes:<br /><br /> 0 = Inicializando<br /><br /> 1 = Preparado<br /><br /> 2 = En pausa<br /><br /> 3 = Error temporal<br /><br /> 4 = Necesario volver a montar<br /><br /> 5 = Apagado<br /><br /> 6 = En modo inactivo para copia de seguridad<br /><br /> 7 = La copia de seguridad se realiza a través del catálogo<br /><br /> 8 = El catálogo está dañado|  
|**status_description**|**nvarchar(120)**|Descripción del estado actual del catálogo de texto completo activo.|  
|**previous_status**|**int**|Estado anterior del catálogo de texto completo. Uno de los siguientes:<br /><br /> 0 = Inicializando<br /><br /> 1 = Preparado<br /><br /> 2 = En pausa<br /><br /> 3 = Error temporal<br /><br /> 4 = Necesario volver a montar<br /><br /> 5 = Apagado<br /><br /> 6 = En modo inactivo para copia de seguridad<br /><br /> 7 = La copia de seguridad se realiza a través del catálogo<br /><br /> 8 = El catálogo está dañado|  
|**previous_status_description**|**nvarchar(120)**|Descripción del estado anterior del catálogo de texto completo activo.|  
|**worker_count**|**int**|Número de subprocesos que trabajan actualmente en este catálogo de texto completo.|  
|**active_fts_index_count**|**int**|Número de índices de texto completo que se van a rellenar.|  
|**auto_population_count**|**int**|Número de tablas con un rellenado automático en curso para este catálogo de texto completo.|  
|**manual_population_count**|**int**|Número de tablas con rellenado manual en curso para este catálogo de texto completo.|  
|**full_incremental_population_count**|**int**|Número de tablas con un rellenado incremental o completo en curso para este catálogo de texto completo.|  
|**row_count_in_thousands**|**int**|Número de filas estimado (en miles) en todos los índices de texto completo en este catálogo de texto completo.|  
|**is_importing**|**bit**|Indica si se va a importar el catálogo de texto completo:<br /><br /> 1 = Se va a importar el catálogo.<br /><br /> 2 = No se va a importar el catálogo.|  
  
## <a name="remarks"></a>Comentarios  
 Era nueva en la columna is_importing [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
   
## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones significativas de esta vista de administración dinámica](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "combinaciones significativas de esta vista de administración dinámica")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|Uno a uno|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|Uno a uno|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve información acerca de los catálogos de texto completo activos en la base de datos actual.  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
