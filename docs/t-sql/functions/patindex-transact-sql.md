---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f718d61c351e11c0e5d159e683390cf311f49e48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914365"
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la posición inicial de la primera repetición de un patrón en la expresión especificada, o ceros si el patrón no se encuentra, en todos los tipos de datos de texto y caracteres.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *pattern*  
 Es una expresión de carácter que contiene la secuencia que se va a buscar. Se pueden usar caracteres comodín, pero el carácter % debe ir delante y detrás de *pattern* (a menos que busque el primer o el último carácter). *pattern* es una expresión de la categoría del tipo de datos de cadena de caracteres. *pattern* tiene un límite de 8000 caracteres.  
  
 *expression*  
 [expression](../../t-sql/language-elements/expressions-transact-sql.md) es una expresión, normalmente una columna en la que se busca el patrón especificado. *expression* es de la categoría del tipo de datos de cadena de caracteres.  
  
## <a name="return-types"></a>Tipos devueltos  
**bigint** si *expression* es de los tipos de datos **varchar(max)** o **nvarchar(max)** ; en caso contrario, **int**.  
  
## <a name="remarks"></a>Notas  
Si *pattern* o *expression* son NULL, PATINDEX devuelve NULL.  
 
La posición inicial de PATINDEX es 1.
 
PATINDEX realiza comparaciones basadas en la intercalación de la entrada. Para realizar una comparación de una intercalación especificada, puede utilizar COLLATE para aplicar una intercalación explícita a la entrada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
Cuando se usan intercalaciones SC, el valor devuelto contará cualquier par suplente UTF-16 en el parámetro *expression* como un solo carácter. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
0x0000 (**char(0)** ) es un carácter no definido en las intercalaciones de Windows y no se puede incluir en PATINDEX.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-patindex-example"></a>A. Ejemplo sencillo de PATINDEX  
 En este ejemplo se comprueba una cadena corta de caracteres (`interesting data`) para la ubicación inicial de los caracteres `ter`.  
  
```sql  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Utilizar un patrón con PATINDEX  
En el siguiente ejemplo se busca la posición en que comienza el patrón `ensure` en una fila específica de la columna `DocumentSummary` de la tabla `Document` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
Si no restringe las filas que se van a buscar mediante una cláusula `WHERE`, la consulta devuelve todas las filas de la tabla e informa de valores distintos de cero para las filas en las que se encontró el modelo, y cero para todas las filas en las que no se encontró el modelo.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Utilizar caracteres comodín con PATINDEX  
 En el siguiente ejemplo se utilizan los caracteres comodín % y _ para buscar la posición en la que comienza el modelo `'en'` en la cadena especificada, seguido de cualquier carácter y `'ure'` (el índice comienza en 1):  
  
```sql  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
`PATINDEX` funciona igual que `LIKE`, por lo que se puede usar cualquiera de los caracteres comodín. No es necesario incluir el patrón entre caracteres de porcentaje. `PATINDEX('a%', 'abc')` devuelve 1 y `PATINDEX('%a', 'cba')` devuelve 3.  
  
 A diferencia de `LIKE`, `PATINDEX` devuelve una posición, de forma similar a `CHARINDEX`.  
  
### <a name="d-using-collate-with-patindex"></a>D. Utilizar COLLATE con PATINDEX  
 En el siguiente ejemplo se utiliza la función `COLLATE` para especificar de forma explícita la intercalación de la expresión que se está buscando.  
  
```sql  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. Usar una variable para especificar el patrón  
En este ejemplo se usa una variable para pasar un valor al parámetro *pattern*. Aquí se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
------------  
22
```  
  
## <a name="see-also"></a>Consulte también  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)  [&#40;Carácter comodín - Caracteres coincidentes &#40;Transact-SQL&#41;]  
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)  [&#40;Carácter comodín - Caracteres no coincidentes &#40;Transact-SQL&#41;]  
 [_ &#40;Wildcard - Match One Character&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  [_ &#40;Carácter comodín - Coincidir con un carácter&#41; &#40;Transact-SQL&#41;]  
 [Percent character &#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md) [Carácter de porcentaje &#40;Carácter comodín - Caracteres coincidentes Transact-SQL&#41;]  
  
  


