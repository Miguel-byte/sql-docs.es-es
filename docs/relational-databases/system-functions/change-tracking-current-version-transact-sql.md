---
title: CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CURRENT_VERSION_TSQL
- CHANGE_TRACKING_CURRENT_VERSION
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_CURRENT_VERSION
- CHANGE_TRACKING_CURRENT_VERSION
ms.assetid: 3027c4f7-6b4d-4089-a369-5926e8a8da1c
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1bf8d568031541df8f4dfa80a4148ad759dad54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043000"
---
# <a name="changetrackingcurrentversion-transact-sql"></a>CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una versión que está asociada a la última transacción confirmada. Esta versión se puede usar cuando se enumeren los cambios mediante [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CHANGE_TRACKING_CURRENT_VERSION ( )  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 **bigint**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve NULL si no está habilitado el seguimiento de cambios para la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se declara la variable local `@next_baseline` para almacenar la versión actual de los cambios a los que se ha realizado el seguimiento y, a continuación, se usa la función `CHANGE_TRACKING_CURRENT_VERSION()` para obtener el valor de la variable.  
  
```sql  
DECLARE @next_baseline bigint;  
SET @next_baseline = CHANGE_TRACKING_CURRENT_VERSION();  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de seguimiento de cambios &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
