---
title: Especificar predicados en un paso de expresión de ruta de acceso | Microsoft Docs
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
- axis step [XQuery]
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e8ba9bb523d4ce7aed76f61c569f5e8b1775972
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946428"
---
# <a name="path-expressions---specifying-predicates"></a>Expresiones de ruta de acceso: Especificación de predicados
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Como se describe en el tema [las expresiones de ruta de acceso de XQuery](../xquery/path-expressions-xquery.md), un paso de eje en una expresión de ruta de acceso incluye los siguientes componentes:  
  
-   [Un eje](../xquery/path-expressions-specifying-axis.md).  
  
-   Una prueba de nodo. Para obtener más información, consulte [especificando la prueba de nodo en un paso de expresión de ruta de acceso](../xquery/path-expressions-specifying-node-test.md).  
  
-   Cero o más predicados. Esto es opcional.  
  
 El predicado opcional representa la tercera parte del paso de eje en una expresión de ruta de acceso.  
  
## <a name="predicates"></a>Predicados  
 Un predicado se utiliza para filtrar una secuencia de nodos aplicando una prueba específica. La expresión de predicado se incluye entre corchetes y se enlaza con el último nodo de una expresión de ruta de acceso.  
  
 Por ejemplo, supongamos que un valor de parámetro SQL (x) de la **xml** se declara el tipo de datos, como se muestra en la siguiente:  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 En este caso, las siguientes expresiones son expresiones válidas que utilizan el valor de predicado [1] en cada uno de los tres niveles de nodos diferentes:  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 Tenga en cuenta que, en cada caso, el predicado se enlaza con el nodo de la expresión de ruta de acceso donde se aplica. Por ejemplo, la primera expresión de ruta de acceso selecciona el primer <`Name`> elemento dentro de cada nodo/People/Person y, con la instancia XML suministrada, devuelve lo siguiente:  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 Sin embargo, la segunda expresión de ruta de acceso selecciona todos los <`Name`> elementos que están bajo el nodo primera/People/Person. Por tanto, devuelve lo siguiente:  
  
```  
<Name>John</Name>  
```  
  
 Se pueden utilizar paréntesis para cambiar el orden de evaluación del predicado. Por ejemplo, en la siguiente expresión se utiliza un conjunto de paréntesis para separar la ruta de acceso de (/People/Person/Name) del predicado [1]:  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 En este ejemplo cambia el orden en que se aplica el predicado. Esto se debe a que primero se evalúa la ruta de acceso incluida entre paréntesis (/People/Person/Name) y después se aplica el operador de predicado [1] al conjunto que contiene todos los nodos que hayan coincidido con la ruta de acceso entre paréntesis. Sin los paréntesis, el orden de las operaciones sería diferente, ya que [1] se aplicaría como prueba de nodo `child::Name`, de manera similar al primer ejemplo de expresión de ruta de acceso.  
  
### <a name="quantifiers-and-predicates"></a>Cuantificadores y predicados  
 Dentro de las llaves del predicado se pueden utilizar cuantificadores, y se pueden agregar más de una vez. Partiendo del ejemplo anterior, a continuación se muestra el uso correcto de varios cuantificadores en una subexpresión de predicado compleja.  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 El resultado de una expresión de predicado se convierte en un valor booleano, que se conoce como el valor real del predicado. En el resultado solo se devuelven los nodos de la secuencia cuyo valor real del predicado es True. Los demás nodos se descartan.  
  
 Por ejemplo, la siguiente expresión de ruta de acceso incluye un predicado en su segundo paso:  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 La condición especificada por este predicado se aplica a todos los <`Location`> elementos secundarios del nodo de elemento. El resultado es que solo se devuelven las ubicaciones de centros de trabajo cuyo atributo LocationID tenga el valor 10.  
  
 La expresión de ruta de acceso anterior se ejecuta en la siguiente instrucción SELECT:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>Calcular valores reales de predicado  
 Para determinar el valor real del predicado se aplican las siguientes reglas, según las especificaciones de XQuery:  
  
1.  Si el valor de la expresión de predicado es una secuencia vacía, el valor real del predicado es False.  
  
     Por ejemplo:  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     La expresión de ruta de acceso en esta consulta devuelve solo aquellos <`Location`> los nodos de elemento que tienen especificado el atributo LotSize. Si el predicado devuelve una secuencia vacía para un determinado <`Location`>, que la ubicación de centro de trabajo no se devuelve en el resultado.  
  
2.  Solo pueden ser valores xs: Integer, xs: Boolean o nodo de predicado\*. Nodo\*, el predicado se evalúa como True si hay nodos y False para una secuencia vacía. Cualquier otro tipo numérico, como double y float, genera un error de tipos estáticos. El valor real del predicado de una expresión es True si y solo si el entero resultante es igual al valor de la posición de contexto. Además, solo los valores literales enteros y **last()** función reducen la cardinalidad de la expresión de filtrado paso a 1.  
  
     Por ejemplo, la consulta siguiente recupera el tercer nodo de elemento secundario de la <`Features`> elemento.  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     Observe lo siguiente en la consulta anterior:  
  
    -   El tercer paso de la expresión especifica una expresión de predicado cuyo valor es 3. Por tanto, el valor real del predicado de esta expresión es True solo para los nodos cuya posición de contexto sea 3.  
  
    -   El tercer paso especifica también un carácter comodín (*) que indica todos los nodos de la prueba de nodo. Sin embargo, el predicado filtra los nodos y devuelve solo el nodo que ocupa la tercera posición.  
  
    -   La consulta devuelve el tercer elemento secundario de nodo de elemento de la <`Features`> elementos secundarios de la <`ProductDescription`> elementos secundarios de la raíz del documento.  
  
3.  Si el valor de la expresión de predicado es un valor booleano de tipo simple, el valor real del predicado es igual al valor de la expresión de predicado.  
  
     Por ejemplo, la siguiente consulta se especifica en un **xml**variable de tipo que contiene una instancia XML, la instancia XML de encuesta de cliente. La consulta recupera los clientes que tienen elementos secundarios. En esta consulta, que sería \<HasChildren > 1\</HasChildren >.  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     Observe lo siguiente en la consulta anterior:  
  
    -   La expresión en el **para** bucle consta de dos pasos y el segundo paso especifica un predicado. El valor de este predicado es de tipo Boolean. Si este valor es True, el valor real del predicado también es True.  
  
    -   La consulta devuelve el <`Customer`> elementos secundarios del elemento cuyo valor de predicado es True, de la \<encuesta > elementos secundarios de la raíz del documento. Éste es el resultado:  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  Si el valor de la expresión de predicado es una secuencia que contiene al menos un nodo, el valor real del predicado es True.  
  
 Por ejemplo, la consulta siguiente recupera ProductModelID para los modelos de producto cuya descripción de catálogo XML incluya al menos una característica, un elemento secundario de la <`Features`> elemento del espacio de nombres asociado con el **wm**prefijo.  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La cláusula WHERE especifica la [método exist() (tipo de datos XML)](../t-sql/xml/exist-method-xml-data-type.md).  
  
-   La expresión de ruta de acceso dentro de la **exist()** método especifica un predicado en el segundo paso. Si la expresión de predicado devuelve una secuencia de al menos una característica, el valor de esta expresión de predicado es True. En este caso, porque el **exist()** método devuelve True, se devuelve ProductModelID.  
  
## <a name="static-typing-and-predicate-filters"></a>Tipos estáticos y filtros de predicado  
 Los predicados también pueden afectar al tipo de una expresión deducido de forma estática. Los valores literales enteros y **last()** función reducir la cardinalidad de la expresión de filtrado paso a lo sumo una.  
  
  
