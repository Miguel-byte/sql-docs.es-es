---
title: sys.dm_db_mirroring_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: stevestein
ms.author: sstein
ms.openlocfilehash: e08aa031af0bd8c9d5c5ad012d11c534281f92f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017909"
---
# <a name="database-mirroring---sysdmdbmirroringautopagerepair"></a>Creación de reflejo: la base de datos sys.dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada intento de reparación de página automática en cualquier base de datos reflejada en la instancia del servidor. Esta vista contiene las filas para los últimos intentos de reparación de página automática en una base de datos reflejada determinada, con un máximo de 100 filas por base de datos. En cuanto una base de datos alcanza el máximo, la fila del siguiente intento de reparación de página automática reemplazará una de las entradas existentes. En la tabla siguiente se define el significado de las distintas columnas.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador la base de datos a la que corresponde esta fila.|  
|**file_id**|**int**|Identificador del archivo en el que se encuentra la página.|  
|**page_id**|**bigint**|Identificador de la página en el archivo.|  
|**error_type**|**int**|Tipo del error. Los valores pueden ser:<br /><br /> **-** 1 = todos los errores de hardware 823<br /><br /> 1 = 824 errores que no sea una suma de comprobación incorrecta o una página rasgada (por ejemplo, un identificador de página incorrecto)<br /><br /> 2 = Suma de comprobación incorrecta<br /><br /> 3 = Página rasgada|  
|**page_status**|**int**|El estado del intento de reparación de la página:<br /><br /> 2 = En cola para la solicitud del socio.<br /><br /> 3 = Solicitud enviada al socio.<br /><br /> 4 = En cola para la reparación de página automática (respuesta recibida del socio).<br /><br /> 5 = La reparación de página automática tuvo éxito y la página debería ser utilizable.<br /><br /> 6 = Irreparable. Esto indica que se produjo un error durante el intento de reparación de la página, por ejemplo, porque la página también está dañada en el socio, el socio está desconectado o existe un problema de red. Este estado no es definitivo; si se vuelve a producir un daño en la página, se solicitará de nuevo la página del socio.|  
|**modification_time**|**datetime**|Hora del último cambio en el estado de la página.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Reparación de página automática &#40;grupos de disponibilidad: creación de reflejo de la base de datos&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


