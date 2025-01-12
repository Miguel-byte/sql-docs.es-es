---
title: INSERT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 210ab8c5750fdcb38bcbca324d77eecd926042d1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892722"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Procesa el objeto de minería de datos especificado. Para obtener más información sobre cómo procesar modelos y estructuras de minería de datos, vea [requisitos de procesamiento y consideraciones sobre &#40;la&#41;minería de datos](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining).  
  
 Si se especifica una estructura de minería de datos, la instrucción procesa la estructura de minería de datos y todos sus modelos de minería de datos asociados. Si se especifica un modelo de minería de datos, la instrucción procesa solamente el modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *estructuras*  
 Identificador de estructura.  
  
 *columnas del modelo asignado*  
 Lista delimitada por comas de identificadores de columna e identificadores anidados.  
  
 *consulta de datos de origen*  
 Consulta de origen en el formato definido por el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Si no especifica el **modelo** o la **estructura**de minería de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] datos, busca el tipo de objeto basándose en el nombre y procesa el objeto correcto. Si el servidor contiene una estructura y un modelo de minería de datos con el mismo nombre, se devuelve un error.  
  
 Con la segunda forma de sintaxis, inserte en *\<el objeto >* . COLUMN_VALUES, puede insertar datos directamente en las columnas del modelo sin entrenar el modelo. Este método proporciona datos de columna al modelo de forma concisa y ordenada que resultan útiles a la hora de trabajar con conjuntos de datos que contienen jerarquías o columnas ordenadas.  
  
 Si utiliza **Insert Into** con un modelo de minería de datos o una estructura de minería de datos \<y deja fuera de las columnas del modelo asignado > y \<de los argumentos de la consulta de datos de origen >, la instrucción se comporta como **ProcessDefault**, mediante enlaces que ya existe. La instrucción devuelve un error cuando no existen enlaces. Para obtener más información sobre **ProcessDefault**, vea [Opciones de procesamiento &#40;y&#41;configuración Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services). En el siguiente ejemplo se muestra la sintaxis:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Si especifica el **modelo de minería** de datos y proporciona columnas asignadas y una consulta de datos de origen, se procesan el modelo y la estructura asociada.  
  
 La siguiente tabla ofrece una descripción del resultado de distintas formas de la instrucción, en función del estado de los objetos.  
  
|Instrucción|Estado de los objetos|Resultado|  
|---------------|----------------------|------------|  
|Insertar en modelo de *\<modelo de minería de datos >*|La estructura de minería de datos está procesada.|Se procesa el modelo de minería de datos.|  
||La estructura de minería de datos no está procesada.|Se procesan el modelo y la estructura de minería de datos.|  
||La estructura de minería de datos contiene modelos de minería de datos adicionales.|Se produce un error en el proceso. Deberá volver a procesar la estructura y los modelos de minería de datos asociados.|  
|Insertar en estructura de la estructura *\<de minería de datos >*|La estructura de minería de datos está procesada o sin procesar.|Se procesan la estructura de minería de datos y los modelos de minería de datos asociados.|  
|Insertar en *\<modelo* de modelo de minería de datos > que contiene una consulta de origen<br /><br /> o Administrador de configuración de<br /><br /> Insertar en *\<estructura* de la estructura de minería de datos > que contiene una consulta de origen|La estructura o el modelo ya tienen contenido.|Se produce un error en el proceso. Debe borrar los objetos antes de realizar esta operación mediante la [eliminación &#40;de DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Columnas de modelo asignadas  
 Mediante el uso \<de las columnas del modelo asignado > elemento, puede asignar las columnas del origen de datos a las columnas del modelo de minería de datos. Las \<columnas del modelo asignado > elemento tienen el formato siguiente:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Al usar **SKIP**, puede excluir ciertas columnas que deben existir en la consulta de origen, pero que no existen en el modelo de minería de datos. SKIP es útil cuando no se tiene el control sobre las columnas que se incluyen en el conjunto de filas de entrada. Si está escribiendo su propia instrucción OPENQUERY, lo mejor es omitir la columna en la lista de columnas SELECT en lugar de usar SKIP.  
  
 SKIP también es útil cuando se necesita una columna del conjunto de filas de entrada para realizar una combinación, pero la estructura de minería de datos no utiliza la columna. Un ejemplo típico de esto es una estructura y un modelo de minería de datos que contienen una tabla anidada. El conjunto de filas de entrada para esta estructura tendrá una columna de clave externa que se utiliza para crear un conjunto de filas jerárquico mediante la cláusula SHAPE, pero la columna de clave externa casi nunca se utiliza en el modelo.  
  
 La sintaxis de SKIP requiere que se inserte SKIP en la posición de la columna individual en el conjunto de filas de entrada que no tiene ninguna columna de estructura de minería de datos correspondiente. Por ejemplo, en el ejemplo de tabla anidada siguiente, OrderNumber debe estar seleccionado en la cláusula APPEND para que se pueda utilizar en la cláusula RELATE con el fin de especificar la combinación; sin embargo, no desea insertar los datos de OrderNumber en la tabla anidada de la estructura de minería de datos. Por consiguiente, el ejemplo utiliza la palabra clave SKIP en lugar de OrderNumber en el argumento de INSERT INTO.  
  
## <a name="source-data-query"></a>Consulta de datos de origen  
 El \<elemento > de la consulta de datos de origen puede incluir los siguientes tipos de orígenes de datos:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Cualquier consulta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que devuelva un conjunto de filas  
  
 Para obtener más información sobre los tipos de orígenes de datos, vea [ &#60;consulta&#62;de datos de origen](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Ejemplo básico  
 En el ejemplo siguiente se usa **OPENQUERY** para entrenar un modelo Bayes Naive basado en los datos de correo de [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] destino de la base de datos.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Ejemplo de tabla anidada  
 En el ejemplo siguiente se utiliza una **forma** para entrenar un modelo de minería de datos de asociación que contiene una tabla anidada. Tenga en cuenta que la primera línea contiene **SKIP** en lugar de OrderNumber, que es necesaria en la instrucción **SHAPE_APPEND** pero no se utiliza en el modelo de minería de datos.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-definition.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
