---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b7e0a949e132f01ce82e46a6e8b4c1d761c1a52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100054"
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica el tamaño de los datos **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **text**, **ntext** e **image** devueltos por una instrucción SELECT.  
  
> [!IMPORTANT]
>  Los tipos de datos **ntext**, **text** e **image** se quitarán en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite su uso en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que los usan actualmente. Use **nvarchar(max)** , **varchar(max)** y **varbinary(max)** en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argumentos  
 *number*  
 Es la longitud de los datos **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **text**, **ntext** o **image**, en bytes. *number* es un entero con un valor máximo de 2 147 483 647 (2 GB).  Un valor -1 indica un tamaño ilimitado. Un valor 0 restablece el tamaño al valor predeterminado de 4 KB.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 y versiones posteriores) y el controlador ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifican automáticamente `-1` (ilimitado) al conectarse.  
  
 **Controladores anteriores a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (versión 9) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente TEXTSIZE en 2147483647 al conectarse.  
  
## <a name="remarks"></a>Notas  
 La configuración de SET TEXTSIZE afecta a la función @@TEXTSIZE.  
  
 La opción de SET TEXTSIZE se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Consulte también  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
