---
title: '@@TOTAL_READ (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TOTAL_READ_TSQL'
- '@@TOTAL_READ'
dev_langs:
- TSQL
helpviewer_keywords:
- number of disk reads
- disks [SQL Server], number of disk reads
- '@@TOTAL_READ function'
- total read [SQL Server]
- read activity since last started
ms.assetid: b505fbe9-9569-4f3d-80b9-b64b5109ac98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4d743ba90c6dc8ea93daa97a56aa341e4ba987cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098940"
---
# <a name="x40x40totalread-transact-sql"></a>&#x40;&#x40;TOTAL_READ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de lecturas de disco (no de caché) realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
@@TOTAL_READ  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **integer**  
  
## <a name="remarks"></a>Notas  
 Para mostrar un informe con varias estadísticas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluida la actividad de lectura y escritura, ejecute **sp_monitor**.  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo muestra cómo devolver el número total de lecturas y escrituras en disco para la fecha y hora actuales.  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funciones estadísticas del sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_WRITE &#40;Transact-SQL&#41;](../../t-sql/functions/total-write-transact-sql.md)  
  
  
