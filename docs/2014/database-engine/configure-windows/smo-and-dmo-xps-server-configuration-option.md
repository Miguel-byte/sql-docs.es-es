---
title: SMO y DMO XPs (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d55bd667909721a68d51bcd1db7128b809118843
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755277"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs (opción de configuración del servidor)
  Utilice la opción SMO y DMO XPs para habilitar en este servidor los procedimientos almacenados de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).  
  
 Tenga en cuenta que, a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], DMO se ha quitado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En la siguiente tabla se describen los valores posibles:  
  
|Valor|Significado|  
|-----------|-------------|  
|0|SMO XPs no está disponible.|  
|1|SMO XPs está disponible. Ésta es la opción predeterminada.|  
  
 La configuración surte efecto de forma inmediata.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se habilitan los procedimientos almacenados extendidos de SMO.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
