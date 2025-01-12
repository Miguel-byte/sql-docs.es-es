---
title: Uso de sintaxis en una expresión de ruta de acceso abreviada | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e75db08f283631cf9b5daf064790786a1abc10f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946413"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Expresiones de ruta de acceso: Usar una sintaxis abreviada
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Todos los ejemplos de [descripción de las expresiones de ruta de acceso de XQuery](../xquery/path-expressions-xquery.md) utilizan sintaxis no abreviada para expresiones de ruta de acceso. La sintaxis no abreviada para un paso de eje en una expresión de ruta de acceso incluye el nombre del eje y la prueba de nodo, separados por dos puntos dobles, y seguidos por cero o más calificadores de paso.  
  
 Por ejemplo:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery admite las siguientes abreviaturas para usarlas con expresiones de ruta de acceso:  
  
-   El **secundarios** eje es el eje predeterminado. Por lo tanto, el **secundarios::** eje puede omitirse en un paso en una expresión. Por ejemplo, `/child::ProductDescription/child::Summary` puede escribirse como `/ProductDescription/Summary`.  
  
-   Un **atributo** eje se puede abreviar como @. Por ejemplo, `/child::ProductDescription[attribute::ProductModelID=10]` puede escribirse como `/ProudctDescription[@ProductModelID=10]`.  
  
-   Un **/descendant-or-self::node()/** se puede abreviar como / /. Por ejemplo, `/descendant-or-self::node()/child::act:telephoneNumber` puede escribirse como `//act:telephoneNumber`.  
  
     La consulta anterior recupera todos los números de teléfono almacenados en la columna AdditionalContactInfo de la tabla Contact. El esquema para AdditionalContactInfo se define de forma que un \<telephoneNumber > elemento puede aparecer en cualquier lugar en el documento. Por tanto, para recuperar todos los números de teléfono, debe buscar cada nodo del documento. Esta búsqueda se inicia en la raíz del documento y continúa en todos los nodos descendientes.  
  
     La consulta siguiente recupera todos los números de teléfono para un contacto de cliente específico:  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     Si reemplaza la expresión de ruta de acceso por la sintaxis abreviada, `//act:telephoneNumber`, obtendrá los mismos resultados.  
  
-   El **self::node()** en un paso puede abreviarse con un solo punto (.). Sin embargo, el punto no es equivalente o intercambiable con el **self::node()** .  
  
     Por ejemplo, en la consulta siguiente, el uso de un punto representa un valor y no un nodo:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   El **parent::node()** en un paso puede abreviarse con un punto doble (..).  
  
  
