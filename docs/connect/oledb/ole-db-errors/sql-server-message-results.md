---
title: Resultados del mensaje de SQL Server | Microsoft Docs
description: resultados de los mensajes de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994918"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguientes no generan conjuntos de filas del controlador OLE DB para SQL Server ni un recuento de filas afectadas al ejecutarse:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Si la ejecución es correcta, el controlador de OLE DB para SQL Server Devuelve S_OK y los mensajes están disponibles para el controlador de OLE DB para SQL Server consumidor.  
  
 El controlador de OLE DB para SQL Server Devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la [!INCLUDE[tsql](../../../includes/tsql-md.md)] ejecución de muchas instrucciones o la ejecución del consumidor de un controlador de OLE DB para SQL Server función miembro.  
  
 El consumidor del controlador OLE DB para SQL Server que permite la especificación dinámica de texto de consulta debe comprobar las interfaces de error después de cada ejecución de una función de miembro independientemente del valor del código de retorno, la presencia o ausencia de una referencia de interfaz **IRowset** o **IMultipleResults** devuelta o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
