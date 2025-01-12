---
title: Los cambios en el comportamiento de las marcas de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 447e6d4d35fa77f71f1a7a1b90a5a782e0ccebcc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096619"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Cambios en el comportamiento de marcas de seguimiento
  Las marcas de seguimiento globales establecidos por una sesión surten efecto en otras sesiones de forma inmediata. Algunas marcas de seguimiento de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no existen en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Le recomendamos deshabilitar todas las marcas de seguimiento antes de actualizar. Las marcas de seguimiento que modifican los modos de disponibilidad o la recuperación de base de datos pueden impedir que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] actualice correctamente la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede habilitar las marcas de seguimiento después de comprobar que sean necesarias y que siguen siendo válidas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Si necesita volver a habilitar las marcas de seguimiento, debería realizar pruebas adicionales en su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite marcas de seguimiento globales y de nivel de sesión. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible especificar las marcas de seguimiento como locales o globales utilizando un argumento adicional (-1) en el comando DBCC TRACEON. Si no se especifica este argumento, el valor predeterminado será local.  
  
 Además, en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], una marca de seguimiento establecida en la sesión A no tiene efecto automáticamente en una sesión b ya existente En su lugar, esta marca de seguimiento surte efecto sólo después de la primera vez que se establece la marca de seguimiento en la sesión B. Este comportamiento es no determinista en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] y es determinista en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, donde se establecen marcas de seguimiento globales establecidas en la sesión A inmediatamente en otras sesiones simultáneas.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
