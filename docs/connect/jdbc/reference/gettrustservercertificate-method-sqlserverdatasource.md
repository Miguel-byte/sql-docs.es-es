---
title: Método getTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81d07743dfefe0b0305b1a094a9ae4632d4effd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978582"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>Método getTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **Boolean** que indica si la propiedad trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si trustServerCertificate está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad trustServerCertificate se establece en **true**, se confía automáticamente en el certificado de Capa de sockets seguros (SSL) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el nivel de comunicación se cifra mediante SSL. Es decir, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no validará el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor predeterminado es **false**.  
  
 Si la propiedad trustServerCertificate se establece en **false**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará el certificado SSL del servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
