---
title: sp_syscollector_set_cache_directory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
author: stevestein
ms.author: sstein
ms.openlocfilehash: affa8825053f1123c3fae5518f006e2172b9be39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010669"
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica el directorio en el que se almacenan los datos recopilados antes de cargarlos en el almacén de administración de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @cache_directory = ] 'cache_directory'` El directorio del sistema de archivos donde los datos recopilados se almacenan temporalmente. *cache_directory* es **nvarchar (255)** , su valor predeterminado es null. Si no se especifica ningún valor, se utiliza el directorio temporal predeterminado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe deshabilitar el recopilador de datos antes de cambiar la configuración del directorio de la memoria caché. Se produce un error en este procedimiento almacenado si se habilita el recopilador de datos. Para obtener más información, consulte [habilitar o deshabilitar la recopilación de datos](../../relational-databases/data-collection/enable-or-disable-data-collection.md), y [administrar la recopilación de datos](../../relational-databases/data-collection/manage-data-collection.md).  
  
 El directorio especificado no tiene que existir en el momento en que se ejecute sp_syscollector_set_cache_directory; sin embargo, los datos no pueden almacenarse en memoria caché y cargarse correctamente hasta que se cree el directorio. Recomendamos crear el directorio antes de ejecutar este procedimiento almacenado.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de base de datos dc_admin (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente se deshabilita el recopilador de datos, Establece el directorio de caché para el recopilador de datos `D:\tempdata`y, a continuación, habilita el recopilador de datos.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
