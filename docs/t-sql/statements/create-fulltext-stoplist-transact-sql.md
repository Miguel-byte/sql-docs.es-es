---
title: CREATE FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5316bb4daa281c0abedd133803965a0b0af63bdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912759"
---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una nueva lista de palabras irrelevantes de texto completo en la base de datos actual.  
  
 Las palabras irrelevantes se administran en bases de datos por medio de objetos denominados *listas de palabras irrelevantes*. Una lista de palabras irrelevantes es una lista de palabras que, cuando se asocia a un índice de texto completo, se aplica a las consultas de texto completo en ese índice. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST y DROP FULLTEXT STOPLIST solo se admiten para un nivel de compatibilidad de 100. En niveles de compatibilidad de 80 y 90, estas instrucciones no se admiten. Sin embargo, en todos los niveles de compatibilidad la lista de palabras irrelevantes del sistema se asocia automáticamente a los nuevos índices de texto completo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 Es el nombre de la lista de palabras irrelevantes. *stoplist_name* puede tener un máximo de 128 caracteres. *stoplist_name* debe ser único entre todas las listas de palabras irrelevantes de la base de datos actual y cumplir las reglas de los identificadores.  
  
 *stoplist_name* se usará cuando se cree el índice de texto completo.  
  
 *database_name*  
 Es el nombre de la base de datos donde se encuentra la lista de palabras irrelevantes especificada por *source_stoplist_name*. Si no se especifica, *database_name* usa de manera predeterminada la base de datos actual.  
  
 *source_stoplist_name*  
 Especifica que la nueva lista de palabras irrelevantes se crea copiando otra lista existente. Si *source_stoplist_name* no existe, o el usuario de la base de datos no tiene los permisos correctos, CREATE FULLTEXT STOPLIST produce un error. Si alguno de los idiomas especificados en las palabras irrelevantes de la lista de palabras irrelevantes de origen no está registrado en la base de datos actual, CREATE FULLTEXT STOPLIST crea correctamente la lista, pero se devuelven advertencias y no se agregan las palabras irrelevantes correspondientes.  
  
 SYSTEM STOPLIST  
 Especifica que la nueva lista de palabras irrelevantes se crea a partir de la lista predeterminada que hay en la [base de datos Resource](../../relational-databases/databases/resource-database.md).  
  
 AUTHORIZATION *owner_name*  
 Especifica el nombre de una entidad de seguridad de base de datos como propietaria de la lista de palabras irrelevantes. *owner_name* debe ser el nombre de una entidad de seguridad de la que el usuario actual sea miembro, o bien el usuario actual debe tener el permiso IMPERSONATE en *owner_name*. Si no se especifica, la propiedad se otorga al usuario actual.  
  
## <a name="remarks"></a>Notas  
 El creador de la lista de palabras irrelevantes es su propietario.  
  
## <a name="permissions"></a>Permisos  
 Para crear una lista STOPLIST se requieren permisos CREATE FULLTEXT CATALOG. El propietario de la lista de palabras irrelevantes puede conceder explícitamente el permiso CONTROL para una lista de palabras irrelevantes para permitir a los usuarios agregar y quitar palabras, y quitar la lista de palabras irrelevantes.  
  
> [!NOTE]  
>  El uso de una lista de palabras irrelevantes con un índice de texto completo requiere el permiso REFERENCE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. Crear una lista de palabras irrelevantes de texto completo  
 En el ejemplo siguiente se crea una nueva lista de palabras irrelevantes de texto completo denominada `myStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. Copiar una lista de palabras irrelevantes de texto completo a partir de una lista de palabras irrelevantes de texto completo existente  
 En el ejemplo siguiente se crea una lista de palabras irrelevantes de texto completo denominada `myStoplist2` copiando la lista de palabras irrelevantes de AdventureWorks denominada `Customers.otherStoplist`.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. Copiar una lista de palabras irrelevantes de texto completo a partir de la lista de palabras irrelevantes de texto completo del sistema  
 En el ejemplo siguiente se crea una lista de palabras irrelevantes de texto completo denominada `myStoplist3` copiando la lista de palabras irrelevantes del sistema.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
