---
title: Método supportsANSI92EntryLevelSQL (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92EntryLevelSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3fffc08-7254-4af7-bbae-8ff591fbd5ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e7f1781fe6b42cdd8057978ed22456fe60382b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969840"
---
# <a name="supportsansi92entrylevelsql-method-sqlserverdatabasemetadata"></a>Método supportsANSI92EntryLevelSQL (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite la gramática de SQL de nivel de entrada ANSI92.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsANSI92EntryLevelSQL()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsANSI92EntryLevelSQL se especifica mediante el método supportsANSI92EntryLevelSQL en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
