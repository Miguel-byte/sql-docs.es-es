---
title: sys.registered_search_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 055e64c743c453fb6362d45587b395bf6f3d77bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067889"
---
# <a name="sysregisteredsearchproperties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila para cada propiedad de búsqueda que cualquier lista de propiedades de búsqueda contiene en la base de datos actual.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|Identificador de la lista de propiedades de búsqueda a que pertenece esta propiedad.|  
|**property_set_guid**|**uniqueidentifier**|Identificador único global (GUID) que identifica el conjunto de propiedades al que pertenece la propiedad de búsqueda.|  
|**property_int_id**|**int**|Entero que identifica esta propiedad de búsqueda en el conjunto de propiedades. **property_int_id** es único dentro del conjunto de propiedades.|  
|**property_name**|**nvarchar(64)**|Nombre que identifica de forma exclusiva esta propiedad de búsqueda en la lista de propiedades de búsqueda.<br /><br /> Nota: Para buscar en una propiedad, especifique el nombre de esta propiedad en el [CONTAINS](../../t-sql/queries/contains-transact-sql.md) predicado.|  
|**property_description**|**nvarchar(512)**|Descripción de la propiedad.|  
|**property_id**|**int**|Identificador de propiedad interno de la propiedad de búsqueda dentro de la lista de propiedades de búsqueda identificada por el **property_list_id** valor.<br /><br /> Cuando una propiedad determinada se agrega a una lista de propiedades de búsqueda dada, el servicio Motor de búsqueda de texto completo registra la propiedad y le asigna un identificador de propiedad interno que es específico de esa lista de propiedades. El identificador de propiedad interno, que es un entero, es único para una lista de propiedades de búsqueda determinada. Si una propiedad determinada se registra para varias listas de propiedades de búsqueda, se puede asignar un identificador de propiedad interno diferente para cada lista de propiedades de búsqueda.<br /><br /> Nota: El identificador de propiedad interno es distinto del identificador de entero de propiedad que se especifica al agregar la propiedad a la lista de propiedades de búsqueda. Para obtener más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).<br /><br /> Para ver todos los relacionados con la propiedad de contenido en el índice de texto completo: <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos para las propiedades de búsqueda se limita a las que están en las listas de propiedades de búsqueda de las que se es propietario o en las que se ha concedido algún permiso REFERENCE.  
  
> [!NOTE]  
>  El propietario de lista de propiedades de búsqueda puede conceder permisos REFERENCE o CONTROL en la lista. Los usuarios con permiso CONTROL también pueden conceder el permiso REFERENCE a otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se enumeran todos los metadatos para propiedades de búsqueda registradas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
