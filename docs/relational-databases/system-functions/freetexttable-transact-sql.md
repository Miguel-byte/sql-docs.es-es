---
title: FREETEXTTABLE (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ab1797fabd8fb7d77eab85c97604b77e72f25c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042763"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Es una función utilizada en el [cláusula FROM](../../t-sql/queries/from-transact-sql.md) de un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción SELECT para realizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] búsqueda de texto completo en texto completo indiza las columnas que contienen tipos de datos basados en caracteres. Esta función devuelve una tabla de cero, uno o más filas para las columnas que contienen valores que coinciden con el significado y no solo literalmente, del texto especificado *cadena_freetext*. Se hace referencia a FREETEXTTABLE como si fuera un nombre de tabla normal.  
  
 FREETEXTTABLE es útil para los mismos tipos de coincidencias que el [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md),  
  
 Las consultas que usan FREETEXTTABLE devuelven un valor de clasificación por relevancia (RANK) y una clave de texto completo (KEY) para cada fila.  
  
> [!NOTE]  
>  Para obtener información sobre las formas de búsqueda de texto completo que se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Consulta con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table*  
 Es el nombre de la tabla que se ha marcado para consultas de texto completo. *tabla* o *vista*puede ser un uno, dos o nombre de objeto de base de datos de tres partes. Al consultar una vista, puede incluirse solo una tabla base indizada de texto completo.  
  
 *tabla* no se puede especificar un nombre de servidor y no se puede usar en consultas en servidores vinculados.  
  
 *column_name*  
 Es el nombre de una o varias columnas indizadas de texto completo de la tabla especificada en la cláusula FROM. Las columnas pueden ser de tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** o **varbinary(max)** .  
  
 *column_list*  
 Indica que se pueden especificar varias columnas, separadas por una coma. *column_list* debe ir entre paréntesis. A menos que se especifique *language_term*, el idioma de todas las columnas de *column_list* debe ser el mismo.  
  
 \*  
 Especifica que todas las columnas que se hayan registrado para la búsqueda de texto completo se tienen que usar para buscar la *cadena_freetext* determinada. A menos que *language_term* se especifica, el idioma de todas las columnas indizadas de texto completo en la tabla debe ser el mismo.  
  
 *cadena_freetext*  
 Es el texto que se va a buscar en *column_name*. Se puede escribir cualquier texto, incluidas palabras, frases y oraciones. Se generarán coincidencias si se encuentra algún término o las formas de algún término en el índice de texto completo.  
  
 A diferencia de en el CONTAINS buscar condición where y es una palabra clave, cuando se usa en *cadena_freetext* la palabra 'and' se considera una palabra irrelevante, o [palabra irrelevante](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)y se descartarán.  
  
 No se permite el uso de WEIGHT, FORMSOF, caracteres comodín, NEAR y otros elementos sintácticos. *cadena_freetext* se separa en palabras, de las que se extraen las desinencias y se pasan por el diccionario de sinónimos.  
  
 LANGUAGE *language_term*  
 Es el idioma cuyos recursos se utilizarán en la separación de palabras, la lematización, los diccionarios de sinónimos y la eliminación de palabras irrelevantes como parte de la consulta. Este parámetro es opcional y puede especificarse como un valor hexadecimal, un entero o una cadena correspondiente al identificador de configuración regional (LCID) de un idioma. Si se especifica *language_term*, el idioma que representa se aplicará a todos los elementos de la condición de búsqueda. Si no se especifica ningún valor, se utiliza el idioma de texto completo de la columna.  
  
 Si se almacenan juntos documentos de idiomas diferentes como objetos binarios grandes (BLOB) en una sola columna, el identificador de configuración regional (LCID) de un documento determinado determina qué idioma se usa para indizar su contenido. Al consultar este tipo de columna, especificar *LANGUAGE término_de_idioma* puede aumentar la probabilidad de encontrar una coincidencia correcta.  
  
 Cuando se especifica como una cadena, *language_term* corresponde al valor de columna **alias** de la vista de compatibilidad [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  La cadena debe estar delimitada con comillas sencillas, como en '*language_term*'. Cuando se especifica como un entero, *language_term* es el LCID real que identifica el idioma. Cuando se especifica como un valor hexadecimal, *language_term* es 0x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda.  
  
 Si el valor está en formato DBCS (juego de caracteres de doble byte), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirá a Unicode.  
  
 Si el idioma especificado no es válido o no hay recursos instalados que se correspondan con dicho idioma, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error. Para usar recursos de idioma neutro, especifique 0x0 como *language_term*.  
  
 *top_n_by_rank*  
 Especifica que solo el *n*coincidencias con una clasificación más altos, en orden descendente, se devuelven. Solo se aplica cuando un valor entero, *n*, se especifica. Si se combina *top_n_by_rank* con otros parámetros, es posible que la consulta devuelva menos filas de las que en realidad coinciden con todos los predicados. *top_n_by_rank* permite aumentar el rendimiento de las consultas recuperando solamente las coincidencias más relevantes.  
  
## <a name="remarks"></a>Comentarios  
 Los predicados y las funciones de texto completo operan en una única tabla, que se obtiene del predicado FROM. Para buscar en varias tablas, utilice una tabla combinada en la cláusula FROM a fin de buscar en un conjunto de resultados que sea el producto de dos o más tablas.  
  
 FREETEXTTABLE utiliza las mismas condiciones de búsqueda que el predicado FREETEXT.  
  
 Similar a CONTAINSTABLE, la tabla devuelta tiene las columnas denominadas **clave** y **rango**, que se hace referencia en la consulta para obtener las filas apropiadas y utilizar la fila de valores de clasificación.  
  
## <a name="permissions"></a>Permisos  
 Solo los usuarios que dispongan de los privilegios SELECT adecuados para la tabla especificada o las columnas de la tabla a las que se haga referencia pueden llamar a FREETEXTTABLE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
 El ejemplo siguiente se crea y rellena una tabla sencilla de dos columnas, listado 3 condados y los colores de sus marcas. La TI se crea y rellena un catálogo de texto completo y un índice en la tabla. El **FREETEXTTABLE** se muestra la sintaxis.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>b. Usar FREETEXT en INNER JOIN  
 El ejemplo siguiente devuelve la descripción y el rango de todos los productos cuya descripción coincide con el significado de `high level of performance`.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. Especificar las coincidencias con una clasificación más alta y el idioma  
 El ejemplo siguiente es idéntico y muestra el uso de la `LANGUAGE` *language_term* y *top_n_by_rank* parámetros.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  El LENGUAJE *language_term* parámetro no es necesario utilizar el *top_n_by_rank* parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la búsqueda de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Creación y administración de catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Crear consultas de búsqueda de texto completo &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [Rowset Functions &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [Opción de configuración del servidor Calcular rango previamente](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
