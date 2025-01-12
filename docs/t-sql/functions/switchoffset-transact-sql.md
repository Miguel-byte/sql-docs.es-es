---
title: SWITCHOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ce69487c1550314dc7cfe3641333728fd07155e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117557"
---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un valor **datetimeoffset** que ha cambiado el ajuste de zona horaria almacenado por un nuevo ajuste de zona horaria especificado.  
  
 Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>Argumentos  
 *DATETIMEOFFSET*  
 Es una expresión que se puede resolver como un valor **datetimeoffset(n)** .  
  
 *time_zone*  
 Es una cadena de caracteres en formato [+|-]TZH:TZM o un entero con signo (de minutos) que representa el ajuste de zona horaria y se supone que reconoce y está ajustado para el horario de verano.  
  
## <a name="return-type"></a>Tipo devuelto  
 **datetimeoffset** con la precisión fraccionaria del argumento *DATETIMEOFFSET*.  
  
## <a name="remarks"></a>Notas  
 Use SWITCHOFFSET para seleccionar un valor **datetimeoffset** en el ajuste de zona horaria que sea diferente del que se almacenó originalmente. SWITCHOFFSET no actualiza el valor *time_zone* almacenado.  
  
 SWITCHOFFSET se puede usar para actualizar una columna **datetimeoffset**.  
  
 Si se usa SWITCHOFFSET con la función GETDATE(), es posible que la consulta se ejecute lentamente. Esto se debe a que el optimizador de consultas no puede obtener estimaciones de cardinalidad precisas para el valor datetime. Para resolver este problema, use la sugerencia de consulta OPTION (RECOMPILE) para obligar al optimizador de consultas a que vuelva a compilar un plan de consulta la próxima vez que se ejecute la misma consulta. De este modo, el optimizador tendrá estimaciones de cardinalidad precisas y generará un plan de consulta más eficaz. Para más información sobre la sugerencia de consulta RECOMPILE, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `SWITCHOFFSET` para mostrar un ajuste de zona horaria diferente del valor almacenado en la base de datos.  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>Consulte también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


