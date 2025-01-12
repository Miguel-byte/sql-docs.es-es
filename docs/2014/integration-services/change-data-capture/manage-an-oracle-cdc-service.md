---
title: Administrar Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 5972cee3-b1a9-4c56-aed6-bdddf84af283
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9f9969630f8fe9f665a04575af8670ddb1af1b3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835638"
---
# <a name="manage-an-oracle-cdc-service"></a>Manage an Oracle CDC Service
  Puede usar la Consola de configuración del servicio CDC para administrar un servicio CDC específico.  
  
 **Para seleccionar el servicio CDC con el que desea trabajar**  
  
1.  En el panel izquierdo de la Consola de configuración del servicio CDC, expanda **Servicios CDC locales**.  
  
2.  Seleccione el servicio CDC con el que desea trabajar.  
  
     También puede hacer clic con el botón secundario en el servicio CDC con el que desea trabajar y seleccionar la acción deseada. Consulte [Lo que puede hacer con un servicio CDC](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService).  
  
 **OR**  
  
1.  Seleccione **Servicios CDC locales** en el panel izquierdo de la Consola de configuración del servicio CDC.  
  
2.  En la sección central de la Consola de configuración del servicio CDC, seleccione el servicio con el que desea trabajar.  
  
     También puede hacer clic con el botón secundario en el servicio CDC con el que desea trabajar y seleccionar la acción deseada. Consulte [Lo que puede hacer con un servicio CDC](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService).  
  
##  <a name="BKMK_WhatcandowithCDCService"></a> Lo que puede hacer con un servicio CDC  
 Puede realizar las acciones siguientes al trabajar con un servicio CDC.  
  
### <a name="delete-the-service"></a>Eliminar el servicio  
 En el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC, haga clic en **Eliminar** para eliminar el servicio.  
  
 También puede hacer clic con el botón derecho en el servicio CDC que quiera eliminar y seleccionar **Eliminar**.  
  
 **Nota**: Si cuando se elimina el servicio, este está en ejecución, se detiene antes de eliminarse.  
  
 Para eliminar la definición del servicio de Windows CDC de Oracle, el programa necesita acceso de actualización a la base de datos MSXDBCDC en la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al hacer clic en Aceptar para eliminar el servicio, el programa intenta eliminar el registro del servicio CDC de Oracle en la base de datos MSXDBCDC. Si el programa no puede eliminar el registro del servicio CDC de Oracle porque no tiene los permisos adecuados, pedirá al usuario que especifique un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con permisos de actualización para la base de datos MSXDBCDC.  
  
 Para obtener información acerca de los datos que debe especificar en el cuadro de diálogo Conectar con SQL Server, vea [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md).  
  
### <a name="edit-the-cdc-service-properties"></a>Editar las propiedades del servicio CDC  
 En el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC, haga clic en **Propiedades**.  
  
 También puede hacer clic con el botón derecho en el servicio CDC cuyas propiedades quiera editar y seleccionar **Propiedades**.  
  
## <a name="see-also"></a>Ver también  
 [Cómo administrar un servicio CDC local](how-to-manage-a-local-cdc-service.md)  
