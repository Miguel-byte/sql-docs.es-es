---
title: Creación del conjunto de filas de parámetro con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8994747896c7a04f2527ff451fb566d5ee6f914
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133349"
---
# <a name="table-valued-parameter-rowset-creation"></a>Creación de conjuntos de filas de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Aunque los consumidores pueden proporcionar cualquier objeto de conjunto de filas para los parámetros con valores de tabla, los objetos de conjunto de filas típicos se implementan para los almacenes de datos back-end y, por consiguiente, proporcionan un rendimiento limitado. Por esta razón, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite a los consumidores crear un objeto de conjunto de filas especializado encima de los datos en memoria. Este objeto de conjunto de filas especial en memoria es un nuevo objeto COM llama a un conjunto de filas de parámetro con valores de tabla. Proporciona una funcionalidad similar a la de los conjuntos de parámetros.  
  
 El consumidor crea explícitamente objetos de conjunto de filas de parámetros con valores de tabla para los parámetros de entrada a través de varias interfaces de nivel de sesión. Hay una instancia de un objeto de conjunto de filas de parámetro con valores de tabla para cada parámetro con valores de tabla. El consumidor puede crear los objetos de conjunto de filas de parámetros con valores de tabla proporcionando información de metadatos que ya se conoce (escenario estático) o detectando esa información a través de interfaces de proveedor (escenario dinámico). En las secciones siguientes se describen los dos escenarios.  
  
## <a name="static-scenario"></a>Escenario estático  
 Cuando se conoce la información de tipo, el consumidor utiliza ITableDefinitionWithConstraints::CreateTableWithConstraints para crear una instancia de un objeto de conjunto de filas de parámetro con valores de tabla que corresponde a un parámetro con valores de tabla.  
  
 El *guid* campo (*pTableID* parámetro) contiene el GUID especial (CLSID_ROWSET_TVP). El miembro *pwszName* contiene el nombre del tipo de parámetro con valores de tabla del que el consumidor quiere crear una instancia. El campo *eKind* se establecerá en DBKIND_GUID_NAME. Este nombre es necesario en una instrucción SQL ad hoc, pero es opcional en las llamadas a procedimientos.  
  
 Para la agregación, el consumidor pasa el *pUnkOuter* parámetro con IUnknown de control.  
  
 Las propiedades del objeto de conjunto de filas de parámetro con valores de tabla son de solo lectura, por lo que no se espera que el consumidor para establecer las propiedades en *rgPropertySets*.  
  
 Para el miembro *rgPropertySets* de cada estructura DBCOLUMNDESC, el consumidor puede especificar propiedades adicionales para cada columna. Estas propiedades pertenecen a la propiedad DBPROPSET_SQLSERVERCOLUMN establecida. Permiten especificar la configuración calculada y predeterminada de cada columna. Admiten también propiedades de columna existentes, como la nulabilidad y la identidad.  
  
 Para recuperar la información correspondiente de un objeto de conjunto de filas de parámetros con valores de tabla, el consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar información sobre el valor null, unique, calculadas y actualizar el estado de cada columna, el consumidor use IColumnsRowset:: GetColumnsRowset o IColumnsInfo:: GetColumnInfo. Estos métodos proporcionan información detallada sobre cada columna de conjunto de filas de parámetros con valores de tabla.  
  
 El consumidor especifica el tipo de cada columna del parámetro con valores de tabla. Esto es similar al modo en que se especifican las columnas cuando se crea una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El consumidor Obtiene un objeto de conjunto de filas de parámetro con valores de tabla desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB a través de la *ppRowset* parámetro de salida.  
  
## <a name="dynamic-scenario"></a>Escenario dinámico  
 Cuando el consumidor no tiene información de tipo, debe usar IOpenRowset:: OpenRowset para crear instancias de objetos de conjunto de filas de parámetro con valores de tabla. Todo lo que el consumidor tiene que proporcionar al proveedor es el nombre de tipo.  
  
 En este escenario, el proveedor obtiene la información de tipo de un objeto de conjunto de filas de parámetros con valores de tabla del servidor en nombre del consumidor.  
  
 El *pTableID* y *pUnkOuter* se deben establecer parámetros como se muestra en el escenario estático. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, a continuación, obtiene la información de tipo (información de columna y restricciones) del servidor y devolver un objeto de conjunto de filas de parámetro con valores de tabla a través de la *ppRowset* parámetro. Esta operación requiere la comunicación con el servidor y, por consiguiente, su rendimiento no es tan bueno como el del escenario estático. El escenario dinámico solamente funciona con llamadas a procedimientos parametrizadas.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
