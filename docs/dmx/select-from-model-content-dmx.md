---
title: Seleccione del &lt;modelo&gt;. CONTENIDO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 61cbacee45147b7b6203e9cb2164c02cdc2c7453
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892828"
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>Seleccione del &lt;modelo&gt;. CONTENIDO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el conjunto de filas de esquema del modelo de minería de datos para el modelo de minería de datos especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *lista de expresiones*  
 Lista delimitada por comas de columnas derivadas del conjunto de filas de esquema CONTENT.  
  
 *model*  
 Identificador de modelo.  
  
 *expresión de condición*  
 Opcional. Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 > **Seleccionar del**  _\<modelo_ **.** La instrucción de contenido devuelve contenido específico de cada algoritmo. Por ejemplo, podría desear usar las descripciones de todas las reglas de un modelo de reglas de asociación en una aplicación personalizada. Puede usar una **> seleccionar del \<modelo.** Instrucción de contenido para devolver valores en la columna NODE_RULE del modelo.  
  
 En la tabla siguiente se enumeran las columnas que están incluidas en el contenido del modelo de minería de datos.  
  
> [!NOTE]  
>  Los algoritmos podrían interpretar las columnas de forma distinta para poder representar el contenido correctamente. Para obtener una descripción del contenido del modelo de minería de datos para cada algoritmo y sugerencias sobre cómo interpretar y consultar el contenido del modelo de minería de datos para cada tipo de modelo, vea [contenido &#40;del modelo de minería de datos Analysis Services-minería&#41;de datos](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
|Columna de conjunto de filas CONTENT|Descripción|  
|---------------------------|-----------------|  
|MODEL_CATALOG|Nombre del catálogo. Su valor es NULL si el proveedor no admite catálogos.|  
|MODEL_SCHEMA|Nombre del esquema no completo. Su valor es NULL si el proveedor no admite esquemas.|  
|MODEL_NAME|Nombre del modelo. Esta columna no puede contener valores NULL.|  
|ATTRIBUTE_NAME|Nombre del atributo que corresponde al nodo.|  
|NODE_NAME|El nombre del nodo.|  
|NODE_UNIQUE_NAME|Nombre único del nodo dentro del modelo.|  
|NODE_TYPE|Entero que representa el tipo del nodo. .|  
|NODE_GUID|GUID del nodo. Su valor es NULL si no hay ningún GUID.|  
|NODE_CAPTION|Etiqueta o título asociado con el nodo. Se utiliza principalmente para la presentación. Si no existe ningún título, se devuelve NODE_NAME.|  
|CHILDREN_CARDINALITY|Número de elementos secundarios que tiene el nodo.|  
|PARENT_UNIQUE_NAME|Nombre único del nodo primario del nodo.|  
|NODE_DESCRIPTION|Descripción del nodo.|  
|NODE_RULE|Fragmento XML que representa la regla incrustada en el nodo. El formato de la cadena XML está basado en el estándar PMML.|  
|MARGINAL_RULE|Fragmento XML que describe la ruta de acceso del elemento primario al nodo.|  
|NODE_PROBABILITY|Probabilidad de la ruta de acceso que finaliza en el nodo.|  
|MARGINAL_PROBABILITY|Probabilidad de alcanzar el nodo desde el nodo primario.|  
|NODE_DISTRIBUTION|Tabla que contiene estadísticas que describen la distribución de los valores del nodo.|  
|NODE_SUPPORT|Número de casos de compatibilidad de este nodo.|  
  
## <a name="examples"></a>Ejemplos  
 El código siguiente devuelve el identificador del nodo primario para el modelo de árboles de decisión que se agregó a la estructura de minería de datos de Targeted Mailing.  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 Resultados esperados:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 La consulta de siguiente usa la función **IsDescendant** para devolver los elementos secundarios inmediatos del nodo que se devolvió en la consulta anterior.  
  
> [!NOTE]  
>  Dado que el valor de NODE_NAME es una cadena, no puede usar una instrucción Sub-SELECT para devolver NODE_ID como argumento a la función **IsDescendant** .  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 Resultados esperados:  
  
 Dado que el modelo es de árboles de decisión, los descendientes del nodo primario del modelo incluyen un único nodo de estadísticas marginal, un nodo que representa el atributo de predicción y varios nodos que contienen los atributos de entrada y los valores. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining).  
  
## <a name="using-the-flattened-keyword"></a>Usar la palabra clave FLATTENED  
 El contenido del modelo de minería de datos suele contener información interesante sobre el modelo en columnas de tablas anidadas. La palabra clave FLATTENED le permite recuperar los datos de una columna de tabla anidada sin utilizar un proveedor que admita conjuntos de filas jerárquicos.  
  
 La consulta siguiente devuelve un único nodo, el nodo de estadísticas marginal (NODE_TYPE = 26) de un modelo de Bayes naive. Sin embargo, este nodo contiene una tabla anidada, en la columna NODE_DISTRIBUTION. Como resultado, se quita información de estructura jerárquica de la columna de tabla anidada y se devuelve una fila para cada fila de la tabla anidada. El valor de MODEL_NAME de la columna escalar se repite para cada fila de la tabla anidada.  
  
 Además, observe que si especifica únicamente el nombre de la columna de tabla anidada, se devuelve una columna nueva para cada columna de la tabla anidada. De forma predeterminada, el nombre de la tabla anidada se pone como prefijo del nombre de cada columna de tabla anidada.  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Resultados del ejemplo:  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 En el ejemplo siguiente se demuestra cómo devolver solamente algunas columnas de la tabla anidada utilizando una instrucción sub-select. Puede simplificar la presentación creando un alias del nombre de la tabla anidada, como se muestra a continuación.  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 Resultados del ejemplo:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
