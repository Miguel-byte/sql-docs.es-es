---
title: Position (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
ms.openlocfilehash: de9f30c3c63030aa956366c222b7cbda94e2becb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038981"
---
# <a name="context-functions---position-xquery"></a>Funciones de contexto: position (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta función devuelve un valor entero que indica la posición del elemento de contexto dentro de la secuencia de elementos que se está procesando.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **fn:Position()** sólo puede utilizarse en el contexto de un predicado dependiente del contexto. Concretamente, solo se puede utilizar entre corchetes ([ ]). Las comparaciones con esta función no reducen la cardinalidad durante una inferencia de tipo estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en el [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. Usar la función position() de XQuery para recuperar las dos primeras características de producto  
 La consulta siguiente recupera las dos primeras características, los dos primeros elementos secundarios de la <`Features`> elemento de la descripción de catálogo del modelo de producto. Si hay más características, agrega un <`there-is-more/`> elemento para el resultado.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **espacio de nombres** palabra clave en el [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define un prefijo de espacio de nombres que se usa en el cuerpo de la consulta.  
  
-   El cuerpo de la consulta genera XML que tiene un \<producto > elemento con **ProductModelID** y **ProductModelName** atributos y tiene características de producto que se devuelven como elementos secundarios.  
  
-   El **position()** función se utiliza en el predicado para determinar la posición de la \<características > elemento secundario en el contexto. Si es la primera o segunda característica, se devuelve.  
  
-   La instrucción IF incorpora un \<allí-is-more / > elemento para el resultado si hay más de dos características en el catálogo de productos.  
  
-   Dado que no todos los modelos de producto tienen sus descripciones de catálogo almacenadas en la tabla, la cláusula WHERE descarta las filas para las que CatalogDescriptions es NULL.  
  
 Éste es un resultado parcial:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
