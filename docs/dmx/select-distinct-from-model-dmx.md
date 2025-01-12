---
title: Seleccione DISTINCT &lt;from &gt; Model (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 67ed5236aad0549fa6850114280ee15d8cebcaeb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892529"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT &lt;from &gt; Model (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve todas los estados posibles para la columna seleccionada del modelo. Los valores devueltos varían dependiendo de si la columna especificada contiene valores discretos, valores numéricos de datos discretos o valores numéricos continuos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelve.  
  
 *lista de expresiones*  
 Lista delimitada por comas de expresiones o identificadores de columna (derivados del modelo) relacionados.  
  
 *model*  
 Identificador de modelo.  
  
 *lista de condiciones*  
 Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción **SELECT DISTINCT from** solo funciona con una sola columna o con un conjunto de columnas relacionadas. Esta cláusula no funciona con un conjunto de columnas no relacionadas.  
  
 La instrucción **SELECT DISTINCT from** permite hacer referencia directamente a una columna dentro de una tabla anidada. Por ejemplo:  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 Los resultados de la instrucción **SELECT DISTINCT \<from Model >** varían según el tipo de columna. En la siguiente tabla se describen los tipos de columna admitidos y la salida de la instrucción.  
  
|Tipo de columna|Salida|  
|-----------------|------------|  
|Discrete|Valores únicos de la columna.|  
|Discretized|Punto medio de cada depósito de datos discretos de la columna.|  
|Continuous|Punto medio de los valores de la columna.|  
  
## <a name="discrete-column-example"></a>Ejemplo de columna discreta  
 El siguiente ejemplo de código se basa en `[TM Decision Tree]` el modelo que se crea en el [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta devuelve los valores únicos que existen en la columna discreta `Gender`.  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 Resultados del ejemplo:  
  
|Sexo|  
|------------|  
||  
|F|  
|M|  
  
 Para las columnas que contienen valores discretos, los resultados incluyen siempre el estado Ausente, mostrado como un valor nulo.  
  
## <a name="continuous-column-example"></a>Ejemplo de columna continua  
 El siguiente ejemplo de código devuelve el punto medio y la antigüedad máxima y mínima de todos los valores de la columna.  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 Resultados del ejemplo:  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 La consulta también devuelve una fila de valores nulos para representar los valores ausentes.  
  
## <a name="discretized-column-example"></a>Ejemplo de columnas de datos discretos  
 El ejemplo de código siguiente devuelve el punto medio y los valores máximo y mínimo de cada depósito creado por el algoritmo para la columna [`Yearly Income]`. Para reproducir los resultados de este ejemplo, debe crear una nueva estructura de minería de datos que sea igual que `[Targeted Mailing]`. En el asistente, cambie el tipo de contenido de `Yearly Income` la columna **continuo** a **discreto**.  
  
> [!NOTE]  
>  También puede cambiar el modelo de minería datos creado en el Tutorial básico de minería de datos para discretizar la columna de estructura de minería de datos [`Yearly Income]`. Para obtener información sobre cómo hacerlo, vea [cambiar la discretización de una columna en un modelo de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model). Sin embargo, al cambiar la discretización de la columna, se volverá a procesar la estructura de minería de datos, lo que cambiará los resultados de otros modelos generados usando esa estructura.  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 Resultados del ejemplo:  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 Puede ver que los valores de la columna [Yearly Income] se han discretizado en cinco depósitos, más una fila adicional de valores nulos, para representar los valores ausentes.  
  
 El número de posiciones decimales de los resultados depende del cliente usado para la consulta. Aquí se han redondeado a dos posiciones decimales, tanto por simplicidad como para reflejar los valores mostrados en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Por ejemplo, si examina el modelo usando el Visor de árbol de decisión y hace clic en un nodo que contiene clientes agrupados por ingresos, se muestran las propiedades de nodo siguientes en la información sobre herramientas:  
  
 Age > = 69 e ingresos anuales < 39221,41  
  
> [!NOTE]  
>  El valor mínimo del depósito mínimo y el valor máximo del depósito máximo son los valores observados más altos y más bajos. Los valores que queden fuera de este intervalo observado se supone que pertenecen a los depósitos mínimo y máximo.  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
