---
title: Intercalación y tipos de datos de integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 40c4abad803424ac9b274045f699785b85689644
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874847"
---
# <a name="collation-and-clr-integration-data-types"></a>Intercalación y tipos de datos de integración CLR
  En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], el objeto `CompareInfo` administra las intercalaciones. Las interfaces de programación de aplicaciones (API) de cadenas de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizan la propiedad `CompareInfo` asociada al objeto `CultureInfo` del subproceso actual para comparar las cadenas. El valor predeterminado de la `CultureInfo` objeto se basa en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuración regional de Windows para el equipo en el que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando. Esto determina la semántica de comparación predeterminada para comparar valores de `CultureInfo` si no se ha especificado ningún `System.String` concreto. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cambia de forma explícita la propiedad `CompareInfo` para la intercalación de base de datos o de servidor. Si es necesario, los usuarios deben establecer la propiedad `CompareInfo` pertinente en sus rutinas.  
  
## <a name="parameter-collation"></a>Intercalación de parámetros  
 Cuando se crea una rutina de Common Language Runtime (CLR) y enlazado a la rutina hay un parámetro de un método CLR del tipo `SQLString`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una instancia del parámetro con la intercalación predeterminada de la base de datos que contiene la rutina que hace la llamada. Si un parámetro no es `SqlType` (por ejemplo, `String` en lugar de `SQLString`), la información de intercalación de la base de datos no se asocia al parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
