---
title: Sys.sql_dependencies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8742ebefab7a4b826eac0088a2d57f022a27715b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073184"
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada dependencia de una entidad a la que se hace referencia conforme a su referencia en la expresión o instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que definen otro objeto que hace la referencia.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) en su lugar.  

  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifica la clase de la entidad a la que se hace referencia:<br /><br /> 0 = objeto o columna (solo referencias no enlazada a esquema)<br /><br /> 0 = Objeto o columna (referencias enlazadas a esquemas)<br /><br /> 2 = Tipos (referencias enlazadas a esquemas)<br /><br /> 3 = Colecciones de esquemas XML (referencias enlazadas a esquemas)<br /><br /> 4 = Función de partición (referencias enlazadas a esquemas)|  
|**class_desc**|**nvarchar(60)**|Descripción de la clase de la entidad a la que se hace referencia:<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|Id. del objeto que hace la referencia.|  
|**column_id**|**int**|Si el Id. que hace la referencia es una columna, se obtiene el Id. de la columna que hace la referencia; en caso contrario, el valor es 0.|  
|**referenced_major_id**|**int**|Id. de la entidad a la que se hace referencia, interpretado por el valor de clase de acuerdo con:<br /><br /> 0, 1 = Id. de objeto del objeto o la columna.<br /><br /> 2 = Id. del tipo.<br /><br /> 3 = Id. de la colección de esquemas XML.|  
|**referenced_minor_id**|**int**|Id. secundario de la entidad a la que se hace referencia, interpretado por el valor de clase de acuerdo con lo siguiente.<br /><br /> Si la clase =:<br /><br /> 0, **referenced_minor_id** es un Id. de columna; o si no es una columna, es 0.<br /><br /> 1, **referenced_minor_id** es un Id. de columna; o si no es una columna, es 0.<br /><br /> En caso contrario, **referenced_minor_id** = 0.|  
|**is_selected**|**bit**|Objeto o columna seleccionados.|  
|**is_updated**|**bit**|Objeto o columna actualizados.|  
|**is_select_all**|**bit**|El objeto se utiliza en la cláusula SELECT* (solo nivel de objeto).|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
