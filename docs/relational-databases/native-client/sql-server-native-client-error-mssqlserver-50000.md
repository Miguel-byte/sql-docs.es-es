---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63431d2f8f20159d65a02833c2f24e08d180321a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031731"
---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>Error de SQL Server Native Client MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Versión del producto|11.0|  
|Identificador del evento|50000|  
|Origen del evento|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nombre simbólico||  
|Texto del mensaje|Error de red al intentar leer el archivo '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Se ha realizado un intento de instalación (o actualización) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en un equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ya está instalado y donde la instalación existente se realizó desde un archivo MSI al que se le cambió el nombre desde sqlncli.msi.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, desinstale la versión existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar este error, no instale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client desde un archivo MSI que no se denomine sqlncli.msi.  
  
## <a name="internal-only"></a>Solo para uso interno  
  
