---
title: sys.dm_hadr_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e817b17de8a8af93a13628334337686abbe66b5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900687"
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada intento de reparación de página automática en cualquier base de datos de disponibilidad en una réplica de disponibilidad hospedada para cualquier grupo de disponibilidad por la instancia de servidor. Esta vista contiene las filas para los últimos intentos de reparación de página automática en una base de datos principal o secundaria determinada, con un máximo de 100 filas por base de datos. En cuanto una base de datos alcanza el máximo, la fila del siguiente intento de reparación de página automática reemplazará una de las entradas existentes.
  
  En la tabla siguiente se define el significado de las distintas columnas:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador la base de datos a la que corresponde esta fila.|  
|**file_id**|**int**|Identificador del archivo en el que se encuentra la página.|  
|**page_id**|**bigint**|Identificador de la página en el archivo.|  
|**error_type**|**int**|Tipo del error. Los valores pueden ser:<br /><br /> **-** 1 = todos los errores de hardware 823<br /><br /> 1 = 824 errores que no sea una suma de comprobación incorrecta o una página rasgada (por ejemplo, un identificador de página incorrecto)<br /><br /> 2 = Suma de comprobación incorrecta<br /><br /> 3 = Página rasgada|  
|**page_status**|**int**|El estado del intento de reparación de la página:<br /><br /> 2 = En cola para la solicitud del socio.<br /><br /> 3 = Solicitud enviada al socio.<br /><br /> 4 = página se ha reparado correctamente.<br /><br /> 5 = no se pudo reparar la página durante el último intento / reparación de página automática intentará reparar la página de nuevo.|  
|**modification_time**|**datetime**|Hora del último cambio en el estado de la página.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Reparación de página automática &#40;grupos de disponibilidad: creación de reflejo de la base de datos&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

