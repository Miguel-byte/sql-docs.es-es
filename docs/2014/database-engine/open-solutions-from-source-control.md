---
title: Abrir soluciones desde Control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- opening solutions
- solutions [SQL Server Management Studio], opening
ms.assetid: a96a1f0d-0183-4587-a3b0-4598309cbdd2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f8405c9fcb04559b6f25d2244bc36dde760a182
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62844773"
---
# <a name="open-solutions-from-source-control"></a>Abrir soluciones desde el control de código fuente
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se puede utilizar para abrir soluciones directamente desde el control de código fuente. Al hacer esto, el entorno de Studio crea una copia de la última versión de los archivos de la solución en la ubicación que se especifique.  
  
 Si no hay una copia local de la solución en el disco local, es necesario abrir el proyecto desde el control de código fuente antes de poder utilizar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para desproteger la solución o recuperar los archivos de la misma.  
  
> [!NOTE]  
>  Si ya hay una copia local de la solución que se está abriendo desde el control de código fuente, se le pedirá que sobrescriba esta copia local.  
  
### <a name="to-open-a-solution-from-source-control"></a>Para abrir una solución desde el control de código fuente  
  
1.  En el **archivo** menú, elija **Control de código fuente**y haga clic en **abrir desde el Control de código fuente**.  
  
2.  Si se le pide, inicie sesión en [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  En el **crear un proyecto local de SourceSafe** cuadro de diálogo, seleccione la carpeta que contiene la solución que desea abrir y haga clic en **Aceptar**.  
  
4.  Si ya existe una carpeta de trabajo para la solución en la unidad de disco local, el **crear un nuevo proyecto en la carpeta** cuadro cambia para identificar el directorio local. Si no hay una carpeta de trabajo para la solución, puede escribir la ruta o ir al directorio local en el que debe abrirse la solución.  
  
5.  En el **Abrir solución** cuadro de diálogo, seleccione el archivo de solución y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Abrir proyectos desde el control de código fuente](../../2014/database-engine/open-projects-from-source-control.md)  
  
  
