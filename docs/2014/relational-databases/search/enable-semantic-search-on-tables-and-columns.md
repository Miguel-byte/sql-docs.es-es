---
title: Habilitar la búsqueda semántica en tablas y columnas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], enabling
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2cd0ea9764007784fb6f999c3115e0a2997d8e2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011378"
---
# <a name="enable-semantic-search-on-tables-and-columns"></a>Habilitar la búsqueda semántica en tablas y columnas
  Describe cómo habilitar o deshabilitar la indización semántica estadística de las columnas seleccionadas que contienen documentos o texto.  
  
 La búsqueda semántica estadística usa los datos que indiza la búsqueda de texto completo y crea índices adicionales. Como resultado de esta dependencia en la búsqueda de texto completo, se crea un nuevo índice semántico al definir un nuevo índice de texto completo o al modificar un índice de texto completo existente. Puede crear un nuevo índice semántico mediante instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] o mediante el Asistente para indización de texto completo y otros cuadros de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], como se describe en este tema.  
  
##  <a name="BasicEnabling"></a> Crear un índice semántico  
  
###  <a name="reqenable"></a> Requisitos y restricciones para crear un índice semántico  
  
-   Puede crear un índice en cualquiera de los objetos de base de datos admitidos para la indización de texto completo, incluidas las tablas y las vistas indizadas.  
  
-   Para poder habilitar la indización semántica de columnas específicas, deben existir los siguientes requisitos previos:  
  
    -   Establece el catálogo de texto completo predeterminado para la base de datos.  
  
    -   La tabla debe tener un índice de texto completo.  
  
    -   Las columnas seleccionadas deben participar en el índice de texto completo.  
  
     Puede crear y habilitar todas estos requisitos a la vez.  
  
-   Puede crear un índice en columnas que contenga cualquiera de los tipos de datos admitidos para la indización de texto completo. Para obtener más información, vea [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md).  
  
-   Puede especificar cualquier tipo de documento admitido para la indización de texto completo para las columnas `varbinary(max)`. Para obtener más información, consulte: [Procedimientos: Determinar qué tipos de documento se pueden indexar](#doctypes) en este tema.  
  
-   La indexación semántica crea dos tipos de índices para las columnas que seleccione: un índice de frases clave y un índice de similitud de documentos. No puede seleccionar solo uno de los tipos de índice o el otro cuando habilite la indización semántica. Sin embargo, puede consultar estos dos índices por separado. Para obtener más información, vea [Buscar frases clave en documentos con la búsqueda semántica](find-key-phrases-in-documents-with-semantic-search.md) y [Buscar documentos similares y relacionados con la búsqueda semántica](find-similar-and-related-documents-with-semantic-search.md).  
  
-   Si no especifica explícitamente ningún LCID para un índice semántico, solo se usan las estadísticas del idioma principal y de su idioma asociado para la indización semántica.  
  
-   Si especifica un idioma para una columna para la que no está disponible el idioma, se produce un error de creación del índice y se devuelve un mensaje de error.  
  
###  <a name="HowToEnableCreate"></a> Procedimientos para: Crear un índice semántico cuando no hay ningún índice de texto completo  
 Cuando cree un nuevo índice de texto completo con la instrucción **CREATE FULLTEXT INDEX** , puede habilitar la indexación semántica en el nivel de columna especificando la palabra clave **STATISTICAL_SEMANTICS** como parte de la definición de columna. Asimismo, puede habilitar la indización semántica cuando use el Asistente para indización de texto completo con el fin de crear un nuevo índice de texto completo.  
  
 **Crear un nuevo índice semántico con Transact-SQL**  
 Llame a la instrucción **CREATE FULLTEXT INDEX** y especifique **STATISTICAL_SEMANTICS** para cada columna en la que quiera crear un índice semántico. Para obtener más información sobre todas las opciones de esta instrucción, vea [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 **Ejemplo 1: Creación de un índice único, un índice de texto completo y un índice semántico**  
  
 En el ejemplo siguiente, se crea un catálogo de texto completo predeterminado, **ft**. Después, se crea un índice único en la columna **JobCandidateID** de la tabla **HumanResources.JobCandidate** de la base de datos de ejemplo AdventureWorks2012. Este índice único se requiere como columna de clave de un índice de texto completo. Después, en el ejemplo se crea un índice de texto completo y un índice semántico en la columna **Resume** .  
  
```sql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **Ejemplo 2: Creación de un índice de texto completo y semántico en varias columnas con rellenado de índice retrasado**  
  
 En el ejemplo siguiente se crea un catálogo de texto completo, **documents_catalog**, en la base de datos de ejemplo AdventureWorks2012. A continuación, se crea un índice de texto completo que usa este nuevo catálogo. El índice de texto completo se crea en las columnas **Title**, **DocumentSummary**y **Document** de la tabla **Production.Document** , mientras que el índice semántico se crea únicamente en la columna **Document** . Este índice de texto completo usa el catálogo de texto completo recién creado y un índice de clave única existente, **PK_Document_DocumentID**. Tal como se recomienda, esta clave de índice se crea en una columna de enteros, **DocumentID**. En el ejemplo se especifica el LCID de inglés, 1033, que es el idioma de los datos de las columnas.  
  
 En este ejemplo también se especifica que el seguimiento de cambios está desactivado sin rellenado. Posteriormente, durante las horas de menor actividad, en el ejemplo se usa una instrucción **ALTER FULLTEXT INDEX** para iniciar un rellenado completo en el nuevo índice y habilitar el seguimiento automático de cambios.  
  
```sql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 Posteriormente, durante horas de menor actividad, el índice se rellena:  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
 **Crear un nuevo índice semántico con SQL Server Management Studio**  
 Ejecute el Asistente para indexación de texto completo y habilite **Semántica estadística** en la página **Seleccionar columnas de la tabla** para cada columna en la que quiera crear un índice semántico. Para obtener más información, incluida la información sobre cómo iniciar el Asistente para indexación de texto completo, vea [Usar el Asistente para indexación de texto completo](use-the-full-text-indexing-wizard.md).  
  
###  <a name="HowToEnableAlter"></a> Procedimientos para: Crear un índice semántico cuando hay un índice de texto completo existente  
 Puede agregar la indexación semántica cuando modifique un índice de texto completo existente con la instrucción **ALTER FULLTEXT INDEX** . También puede agregar la semántica con varios cuadros de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Agregar un índice semántico con Transact-SQL**  
 Llame a la instrucción **ALTER FULLTEXT INDEX** con las opciones descritas más adelante para cada columna en la que quiera agregar un índice semántico. Para obtener más información sobre todas las opciones de esta instrucción, vea [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql).  
  
 Tanto el índice de texto completo como el índice semántico se vuelven a rellenar después de llamar a **ALTER**, a menos que se especifique lo contrario.  
  
-   Para agregar una indexación de texto completo solo a una columna, use la sintaxis **ADD** .  
  
-   Para agregar tanto una indexación de texto completo como una indexación semántica a una columna, use la sintaxis **ADD** con la opción **STATISTICAL_SEMANTICS** .  
  
-   Para agregar una indexación semántica a una columna que ya esté habilitada para la indexación de texto completo, use la opción **ADD STATISTICAL_SEMANTICS** . Solo puede agregar una indización semántica a una columna en una única instrucción **ALTER** .  
  
 **Ejemplo: Incorporación de una indización semántica a una columna que ya tenga indexación de texto completo**  
  
 En el ejemplo siguiente se modifica un índice de texto completo existente en la tabla **Production.Document** de la base de datos de ejemplo AdventureWorks2012. En el ejemplo se agrega un índice semántico en la columna **Document** de la tabla **Production.Document** , que ya tiene un índice de texto completo. En el ejemplo se especifica que el índice no se volverá a rellenar automáticamente.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
 **Agregar un índice semántico con SQL Server Management Studio**  
 Puede cambiar las columnas habilitadas para la indexación semántica y de texto completo en la página **Columnas de índice de texto completo** del cuadro de diálogo **Propiedades del índice de texto completo** . Para obtener más información, vea [Administrar índices de texto completo](../../database-engine/manage-full-text-indexes.md).  
  
###  <a name="addreq"></a> Requisitos y restricciones para modificar un índice existente  
  
-   No puede modificar ningún índice existente mientras el rellenado del mismo esté en curso. Para obtener más información sobre cómo supervisar el progreso del rellenado de índices, vea [Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md).  
  
-   No puede agregar indización a una columna ni modificar o quitar la indización de la misma columna en una sola llamada a la instrucción **ALTER FULLTEXT INDEX** .  
  
##  <a name="dropping"></a> Quitar un índice semántico  
  
###  <a name="drophow"></a> Procedimientos para: Quitar un índice semántico  
 Puede quitar la indexación semántica cuando modifique un índice de texto completo existente con la instrucción **ALTER FULLTEXT INDEX** . También puede quitar la indización semántica con varios cuadros de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Quitar un índice semántico con Transact-SQL**  
 -   Para quitar la indexación semántica solo de una columna o de algunas columnas, se debe llamar a la instrucción **ALTER FULLTEXT INDEX** con la opción **ALTER COLUMN***nombre_columna***DROP STATISTICAL_SEMANTICS**. Puede quitar la indización de varias columnas en una sola instrucción **ALTER** .  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP STATISTICAL_SEMANTICS  
    GO  
    ```  
  
-   Para quitar la indexación de texto completo y semántica de una columna, se debe llamar a la instrucción **ALTER FULLTEXT INDEX** con la opción **ALTER COLUMN***nombre_columna***DROP**.  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP  
    GO  
    ```  
  
 **Quitar un índice semántico con SQL Server Management Studio**  
 Puede cambiar las columnas habilitadas para la indexación semántica y de texto completo en la página **Columnas de índice de texto completo** del cuadro de diálogo **Propiedades del índice de texto completo** . Para obtener más información, vea [Administrar índices de texto completo](../../database-engine/manage-full-text-indexes.md).  
  
###  <a name="dropreq"></a> Requisitos y restricciones para quitar un índice semántico  
  
-   No puede quitar la indización de texto completo de ninguna columna mientras se conserve la indización semántica. La indización semántica depende de la indización de texto completo para los resultados de similitud de documentos.  
  
-   No puede especificar la opción **NO POPULATION** cuando quite la indización semántica de la última columna de una tabla para la que se habilitó la indización semántica. Se requiere un ciclo de rellenado para quitar los resultados que se indizaron previamente.  
  
## <a name="checking-whether-semantic-search-is-enabled-on-database-objects"></a>Comprobar si la búsqueda semántica está habilitada en objetos de base de datos  
  
###  <a name="HowToCheckEnabled"></a> Procedimientos para: Comprobar si la búsqueda semántica está habilitada en objetos de base de datos  
 **¿Búsqueda semántica está habilitada para una base de datos?**  
 Consulte la propiedad **IsFullTextEnabled** de la función de metadatos [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql).  
  
 Un valor devuelto de 1 indica que la búsqueda de texto completo y la búsqueda semántica están habilitadas para la base de datos; un valor devuelto de 0 indica lo contrario.  
  
```sql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
 **¿Búsqueda semántica está habilitada para una tabla?**  
 Consulte la propiedad **TableFullTextSemanticExtraction** de la función de metadatos [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql).  
  
 Un valor devuelto de 1 indica que la búsqueda semántica está habilitada para la tabla; un valor devuelto de 0 indica lo contrario.  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 **¿Búsqueda semántica está habilitada para una columna?**  
 Para determinar si la búsqueda semántica está habilitada para una columna específica:  
  
-   Consulte la propiedad **StatisticalSemantics** de la función de metadatos [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql).  
  
     Un valor devuelto de 1 indica que la búsqueda semántica está habilitada para la columna; un valor devuelto de 0 indica lo contrario.  
  
    ```sql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   Consulte la vista de catálogo [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql) para el índice de texto completo.  
  
     Un valor de 1 en la columna **statistical_semantics** indica que la columna especificada está habilitada para la indexación semántica además de la indexación de texto completo.  
  
    ```sql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   En el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en una columna y seleccione **Propiedades**. En la página **General** del cuadro de diálogo **Propiedades de columna** , compruebe el valor de la propiedad **Semántica estadística** .  
  
     Un valor True indica que la columna especificada está habilitada para la indización semántica además de la indización de texto completo.  
  
## <a name="determining-what-can-be-indexed-for-semantic-search"></a>Determinar qué se puede indizar para la búsqueda semántica  
  
###  <a name="HowToCheckLanguages"></a> Procedimientos para: Compruebe qué lenguajes se admiten para la búsqueda semántica  
  
> [!IMPORTANT]  
>  Hay menos idiomas que sean compatibles con la indización semántica que con la indización de texto completo. Como resultado, puede haber columnas que pueda indizar para la búsqueda de texto completo, pero que no para la búsqueda semántica.  
  
 Consulte la vista de catálogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql).  
  
```sql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 Los siguientes idiomas se admiten para la indización semántica. En esta lista se representa la salida de la vista de catálogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql), ordenada por LCID.  
  
|Lenguaje|LCID|  
|--------------|----------|  
|German|1031|  
|Inglés (Estados Unidos)|3082|  
|Francés|1036|  
|Italiano|1040|  
|Portugués (Brasil)|1046|  
|Ruso|1049|  
|Sueco|1053|  
|Inglés (Reino Unido)|2057|  
|Portugués (Portugal)|2070|  
|Español|3082|  
  
###  <a name="doctypes"></a> Procedimientos para: Determinar qué tipos de documentos se pueden indizar  
 Consulte la vista de catálogo [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
 Si el tipo de documento que desea indizar no está en la lista de tipos compatibles, puede tener que buscar, descargar, e instalar filtros adicionales. Para obtener más información, consulte [ver o cambiar los filtros registrados y separadores de palabras](view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="BestPracticeFilegroup"></a> Procedimiento recomendado: Considere la posibilidad de crear un grupo de archivos independiente para el texto completo e índices semánticos  
 Plantéese crear un grupo de archivos independiente para los índices de texto completo y semántico si la asignación de espacio en disco es un problema. Los índices semánticos se crean en el mismo grupo de archivos que el índice de texto completo. Un índice semántico totalmente rellenado puede contener una gran cantidad de datos.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="IssueNoResults"></a> Problema: Buscar en una columna específica no devuelve ningún resultado  
 **¿Se especificó un LCID que no sea Unicode para un idioma Unicode?**  
 Se puede habilitar la indización semántica en un tipo de columna que no sea Unicode con un LCID para un idioma que solo tenga palabras Unicode, como LCID 1049 para ruso. En este caso, nunca se obtendrán resultados de los índices semánticos de esta columna.  
  
  
