---
title: Tarea Limpieza de mantenimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8b3c3aa4f63018e91370c4e01dada40c35a5f2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830805"
---
# <a name="maintenance-cleanup-task"></a>tarea, Limpieza de mantenimiento
  La tarea Limpieza de mantenimiento quita archivos relacionados con planes de mantenimiento, entre los que se incluyen archivos de copia de seguridad de la base de datos e informes creados a partir de planes de mantenimiento. Para obtener más información, vea [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md) y [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 El uso de la tarea Limpieza de mantenimiento permite que un paquete pueda quitar los archivos de copia de seguridad o los informes del plan de mantenimiento del servidor especificado. La tarea Limpieza de mantenimiento incluye una opción para quitar un archivo específico o un grupo de archivos de una carpeta. También puede especificar la extensión de los archivos que desea eliminar.  
  
 Cuando se configura la tarea Limpieza de mantenimiento para quitar archivos de copia de seguridad, la extensión del nombre de archivo predeterminada es BAK. Para archivos de informe, la extensión predeterminada es TXT. Puede actualizar las extensiones para que se adapten a sus necesidades; la única limitación es que las extensiones deben tener una longitud inferior a 256 caracteres.  
  
 Normalmente, conviene quitar archivos los antiguos que ya no son necesarios; la tarea Limpieza de mantenimiento se puede configurar para eliminar archivos con una antigüedad específica. Por ejemplo, se puede configurar la tarea para eliminar archivos que tienen más de cuatro semanas. También puede especificar la antigüedad de los archivos que desea eliminar en días, semanas, meses o años. Si no especifica la antigüedad mínima de los archivos que desea eliminar, se eliminan todos los archivos del tipo especificado.  
  
 A diferencia de versiones anteriores de la tarea Limpieza de mantenimiento, la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la tarea no elimina automáticamente los archivos incluidos en los subdirectorios del directorio especificado. Esta restricción reduce el área expuesta a cualquier ataque que pudiera utilizar la funcionalidad de la tarea Limpieza de mantenimiento para eliminar archivos de forma malintencionada. Para eliminar las subcarpetas del primer nivel, debe seleccionarlo explícitamente. Para ello, active la opción **Incluir subcarpetas de primer nivel** en el cuadro de diálogo **Tarea Limpieza de mantenimiento** .  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>Configuración de la tarea Limpieza de mantenimiento  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Limpieza de mantenimiento &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo establecer estas propiedades en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
