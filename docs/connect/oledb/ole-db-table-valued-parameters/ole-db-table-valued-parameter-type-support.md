---
title: Compatibilidad con tipos de parámetros con valores de tabla de OLE DB | Microsoft Docs
description: Compatibilidad con tipos de parámetros con valores de tabla de OLE DB
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: abff9abb82ad0ff54d9b1126541b98babbd6bd76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015296"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Compatibilidad con tipos de parámetros con valores de tablas de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este artículo, se describe la compatibilidad de tipos OLE DB para parámetros con valores de tabla.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de filas de parámetro con valores de tabla  
 Puede crear un objeto de conjunto de filas especializado para parámetros con valores de tabla. Cree el objeto de conjunto de filas del parámetro con valores de tabla mediante ITableDefinitionWithConstraints:: CreateTableWithConstraints o IOpenRowset:: OpenRowset. Para hacerlo, establezca el miembro *eKind* del parámetro *pTableID* en DBKIND_GUID_NAME y suministre CLSID_ROWSET_INMEMORY como miembro de *guid*. El nombre de tipo de servidor para el parámetro con valores de tabla debe especificarse en el miembro *pwszName* de *PTableID* al usar IOpenRowset:: OPENROWSET. El objeto de conjunto de filas del parámetro con valores de tabla se comporta como un controlador de OLE DB normal para SQL Server objeto.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 DBTYPE_TABLE es un nuevo tipo que representa un tipo de tabla. Este tipo especifica los parámetros con valores de tabla de varias interfaces OLE DB donde se requiere un DBTYPE.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE tiene el mismo formato que DBTYPE_IUNKNOWN. Es un puntero a un objeto del búfer de datos. Para obtener una especificación completa en los enlaces, el consumidor rellena el búfer DBOBJECT, con *iid* establecido en una de las interfaces del objeto de conjunto de filas (IID_IRowset). Si no se especifica DBOBJECT en ninguno de los enlaces, se da por supuesto el uso de IID_IRowset.  
  
 No se admiten conversiones a DBTYPE_TABLE ni desde este para cualquier otro tipo. IConvertType::CanConvert devolverá S_FALSE si no se permite la conversión para cualquier solicitud de conversión que no sea de DBTYPE_TABLE a DBTYPE_TABLE. Para ello, se da por supuesto el uso de DBCONVERTFLAGS_PARAMETER en el objeto Command.  
  
## <a name="methods"></a>Métodos  
 Para obtener información sobre los métodos de OLE DB que admiten parámetros con valores de tabla, vea [OLE DB métodos &#40;&#41;de compatibilidad de tipos de parámetro con valores de tabla](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propiedades  
 Para obtener información sobre OLE DB propiedades que admiten parámetros con valores de tabla, vea [OLE DB propiedades&#41;de compatibilidad &#40;con tipos de parámetro con valores de tabla](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
