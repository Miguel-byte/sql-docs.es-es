---
title: Sugerencias de tabla en indizan la vista de definiciones se omiten en el modo de compatibilidad 80 y no se permiten en el modo 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69a6bae06b1cb5d7a727ff2582f10bccf1e21ca8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091805"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>Las sugerencias de tabla en definiciones de vistas indizadas se omiten cuando el modo de compatibilidad es 80, mientras que en los modos 90 y superiores, no se permite su uso
  Las sugerencias de tabla en las definiciones de las vistas indizadas no se permiten en el modo de compatibilidad 90 o superior. Para obtener más información, vea los temas siguientes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla: "Diseñar vistas indizadas", "creación de vistas indizadas," y "Sugerencia de consulta ([!INCLUDE[tsql](../../includes/tsql-md.md)])."  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Las sugerencias de tabla se deben quitar de las definiciones de las vistas indizadas. Independientemente del modo de compatibilidad que se utilice, es recomendable que pruebe la aplicación. Al hacerlo, puede asegurarse de que funciona como es de esperar a la hora de crear, actualizar u obtener acceso a las vistas indizadas, incluyendo el caso en el que las vistas indizadas estén en concordancia con ciertas consultas.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
