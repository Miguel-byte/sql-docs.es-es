---
title: Intercalación de servidor del motor de base de datos incompatible (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 235811baf7339416750a5e3795caae55b0ba70aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094752"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Intercalación del servidor de motor de base de datos incompatible (Asesor de actualizaciones)
  Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para utilizar una intercalación de servidor incompatible.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para utilizar una intercalación de servidor incompatible.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint usa la arquitectura de servicios compartidos de SharePoint. SharePoint no admite [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para las intercalaciones de servidor o que distinguen entre mayúsculas y minúsculas o las intercalaciones de servidor binarias. Entre las intercalaciones incompatibles se incluyen las que son binarias o distinguen entre mayúsculas y minúsculas de forma predeterminada, y las intercalaciones base que son compatibles de forma predeterminada, pero se han configurado con alguno de los designadores de intercalación siguientes:  
  
-   **Binario**  
  
-   **Distingue mayúsculas de minúsculas**  
  
-   **Binary-codepoint**  
  
 Debido a que la intercalación de servidor actual de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] es incompatible, la actualización se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 La propiedad de intercalación del servidor de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no se puede cambiar. No podrá completar una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Deberá migrar la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un servidor nuevo que use una intercalación del servidor compatible. Para obtener más información, vea:  
  
-   [Actualizar y migrar Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Seleccionar una intercalación de SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
