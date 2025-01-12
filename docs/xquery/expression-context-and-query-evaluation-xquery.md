---
title: Contexto de expresiones y evaluación de consultas (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: d665b16c6b635da8b267ac0549ab8d918af8c06b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038920"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>Contexto de expresiones y evaluación de consultas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  El contexto de una expresión es la información que se utiliza para analizarla y evaluarla. A continuación, se muestran las dos fases de evaluación de XQuery:  
  
-   **Contexto estático** -esta es la fase de compilación de consulta. En función de la información disponible, a veces pueden producirse errores durante este análisis estático de la consulta.  
  
-   **Contexto dinámico** -esta es la fase de ejecución de consulta. Aunque una consulta no presente errores estáticos, como errores que se hayan producido durante la compilación de la consulta, la consulta puede devolver errores durante su ejecución.  
  
## <a name="static-context"></a>Contexto estático  
 La inicialización del contexto estático se refiere al proceso que consiste en reunir toda la información de cara al análisis estático de la expresión. Como parte de la inicialización del contexto estático, se llevan a cabo los siguientes pasos:  
  
-   El **espacio en blanco límite** directiva está establecida en la franja. Por lo tanto, no se conserva el espacio en blanco de límite con el **cualquier elemento** y **atributo** constructores en la consulta. Por ejemplo:  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     La siguiente consulta devuelve el siguiente resultado, porque el espacio límite se elimina durante el análisis de la expresión XQuery:  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   El enlace del espacio de nombres y el prefijo se inicializan para los siguientes espacios de nombres:  
  
    -   Un conjunto de espacios de nombres predefinidos.  
  
    -   Cualquier espacio de nombres definido mediante WITH XMLNAMESPACES. Para obtener más información, consulte [agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)).  
  
    -   Cualquier espacio de nombres definido en el prólogo de la consulta. Tenga en cuenta que las declaraciones de espacios de nombres del prólogo pueden reemplazar la declaración de espacio de nombres de WITH XMLNAMESPACES. Por ejemplo, en la siguiente consulta, WITH XMLNAMESPACES declara un prefijo (pd) que se enlaza al espacio de nombres (`https://someURI`). Sin embargo, en la cláusula WHERE, el prólogo de la consulta reemplaza el enlace.  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     Todos estos enlaces de espacio de nombres se resuelven durante la inicialización del contexto estático.  
  
-   Si la consulta con tipo **xml** columna o variable, los componentes de la colección de esquemas XML asociada con la columna o variable se importan en el contexto estático. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
-   Se pone a disposición de cada uno de los tipos atómicos de los esquemas importados una función de conversión en el contexto estático. Esto se muestra en el ejemplo siguiente. En este ejemplo, se especifica una consulta contra un tipo **xml** variable. La colección de esquemas XML asociada a esta variable define un tipo atómico, myType. Correspondiente a este tipo, una función de conversión, **myType()** , está disponible durante el análisis estático. La expresión de consulta (`ns:myType(0)`) devuelve un valor de tipo myType.  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     En el ejemplo siguiente, la función de conversión para la **int** tipo integrado de XML se especifica en la expresión.  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 Una vez inicializado el contexto estático, se analiza la expresión de consulta (se compila). El análisis estático conlleva los siguientes pasos:  
  
1.  Análisis de la consulta.  
  
2.  Resolución de los nombres de tipos y funciones que se hayan especificado en la expresión.  
  
3.  Escritura estática de la consulta. Este paso garantiza la seguridad de tipos de la consulta. Por ejemplo, la consulta siguiente devuelve un error estático, porque el **+** operador requiere argumentos de tipo primitivo numérico:  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     En el ejemplo siguiente, la **value()** operador requiere un valor singleton. Como se especifica en el esquema XML, puede haber varios \<Elem > elementos. El análisis estático de la expresión determina que no tiene seguridad de tipos y se devuelve un error estático. Para resolver este error, hay que volver a escribir la expresión y especificar explícitamente un valor singleton (`data(/x:Elem)[1]`).  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     Para obtener más información, consulte [XQuery y tipos estáticos](../xquery/xquery-and-static-typing.md).  
  
### <a name="implementation-restrictions"></a>Restricciones de implementación  
 A continuación se muestran las limitaciones relativas al contexto estático:  
  
-   No se admite el modo de compatibilidad de XPath.  
  
-   Para una construcción XML, solo se admite el modo de construcción de eliminación. Esta es la configuración predeterminada. Por lo tanto, es el tipo del nodo de elemento construidos de **xdt: sin tipo** son de tipo y los atributos de **xdt: untypedAtomic** tipo.  
  
-   Solo se admite el modo de ordenación ordenado.  
  
-   Solo se admite la directiva de eliminación de espacio XML.  
  
-   No se admite la funcionalidad URI básica.  
  
-   **fn:doc()** no se admite.  
  
-   **fn:Collection()** no se admite.  
  
-   No se proporciona un indicador estático de XQuery.  
  
-   La intercalación asociada con el **xml** se usa el tipo de datos. Esta intercalación siempre se establece en la intercalación de punto de código Unicode.  
  
## <a name="dynamic-context"></a>Contexto dinámico  
 El contexto dinámico se refiere a la información que debe estar disponible en el momento de ejecución de la expresión. Además del contexto estático, también se inicializa la siguiente información como parte del contexto dinámico:  
  
-   El foco de la expresión, como el elemento de contexto, la posición de contexto y el tamaño de contexto, se inicializa del modo que se muestra a continuación. Tenga en cuenta que todos estos valores pueden reemplazarse por la [método nodes()](../t-sql/xml/nodes-method-xml-data-type.md).  
  
    -   El **xml** tipo de datos establece el elemento de contexto, el nodo que se va a procesar, en el nodo de documento.  
  
    -   La posición de contexto, la posición del elemento de contexto con respecto a los nodos que se van a procesar, se establece primero en 1.  
  
    -   El tamaño de contexto, el número de elementos de la secuencia que se va a procesar, se establece primero en 1, porque siempre hay un nodo de documento.  
  
### <a name="implementation-restrictions"></a>Restricciones de implementación  
 A continuación se muestran las limitaciones relativas al contexto dinámico:  
  
-   El **fecha y hora actuales** funciones de contexto, **fn:current-fecha**, **fn:current-tiempo**, y **fn:current-dateTime**, no son admite.  
  
-   El **zona horaria implícita** está fija en UTC+0 y no se puede cambiar.  
  
-   El **fn:doc()** no se admite la función. Todas las consultas se ejecutan en **xml** columnas o variables de tipo.  
  
-   El **fn:collection()** no se admite la función.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)   
 [Comparar XML con tipo y XML sin tipo](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
