---
title: SET STATISTICS IO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3cf335242bd0f0e33939c0a72c19390d90252103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941845"
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestre información relacionada con la cantidad de actividad de disco generada por las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>Notas  
 Cuando STATISTICS IO tiene el estado ON, se muestra información estadística; con el estado OFF, no se muestra la información.   
  
 Cuando esta opción se establece en ON, las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes devolverán la información estadística hasta que la opción sea OFF.  
  
 La siguiente tabla muestra y describe los elementos de salida.  
  
|Elemento de salida|Significado|  
|-----------------|-------------|  
|**Table**|Nombre de la tabla.|  
|**Scan count**|Número de búsquedas o exámenes iniciados después de alcanzar el nivel hoja en cualquier dirección para recuperar todos los valores y generar el conjunto de datos final de la salida.<br /><br /> El número de exámenes es 0 si el índice usado es un índice único o un índice agrupado en una clave principal y está buscando un solo valor. Por ejemplo, `WHERE Primary_Key_Column = <value>`.<br /><br /> El número de exámenes es 1 cuando se busca un valor con un índice agrupado que no es único y que se define en una columna de clave de no principal. Este proceso se realiza para comprobar si hay valores duplicados para el valor de clave que está buscando. Por ejemplo, `WHERE Clustered_Index_Key_Column = <value>`.<br /><br /> El número de exámenes es N si N es el número de exploraciones y búsquedas diferentes empezó hacia la izquierda o la derecha del nivel hoja después de encontrar un valor de clave mediante la clave de índice.|  
|**logical reads**|Número de páginas leídas de la caché de datos.|  
|**physical reads**|Número de páginas leídas del disco.|  
|**read-ahead reads**|Número de páginas llevadas a la caché por la consulta.|  
|**lob logical reads**|Número de páginas leídas de la caché de datos. Incluye **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** o páginas de índice de almacén de columnas.|  
|**lob physical reads**|Número de páginas leídas del disco. Incluye **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** o páginas de índice de almacén de columnas.|  
|**lob read-ahead reads**|Número de páginas llevadas a la caché por la consulta. Incluye **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** o páginas de índice de almacén de columnas.|

 La opción SET STATISTICS IO se establece en tiempo de ejecución, no en tiempo de análisis.

> [!NOTE]  
> Cuando las instrucciones Transact-SQL recuperan columnas LOB, es posible que algunas operaciones de recuperación de LOB necesiten recorrer el árbol de LOB varias veces. Esto puede ocasionar que SET STATISTICS IO informe de un mayor número de lecturas lógicas del que cabría esperar.

## <a name="permissions"></a>Permisos  
 Para utilizar SET STATISTICS IO, los usuarios deben tener los permisos adecuados para ejecutar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. El permiso SHOWPLAN no es necesario.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza las lecturas lógicas y físicas mientras procesa las instrucciones.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
