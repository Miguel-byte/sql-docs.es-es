---
title: Métodos de programación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99dac71ba0be4f4c3f3ff669f838b0409b996f06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283455"
---
# <a name="scheduling-methods"></a>Métodos de programación
  Puede utilizar estos métodos para crear y administrar las programaciones compartidas para la ejecución y la entrega de informes, así como para almacenar en memoria caché los planes de actualización que utiliza el servidor de informes.  
  
|Método|Acción|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|Crea un plan de actualización de caché para un elemento.|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|Crea una nueva programación compartida.|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|Elimina un plan de actualización de caché.|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|Elimina una programación compartida según un identificador de programación concreto.|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|Devuelve las propiedades del plan de actualización de caché especificado.|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|Devuelve los valores de las propiedades de una programación compartida.|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|Devuelve una lista de los planes de actualización de memoria caché asociada a un elemento de catálogo.|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|Devuelve una lista de los elementos que están asociados a una programación compartida.|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|Devuelve una lista de todas las programaciones compartidas en el servidor de informes o el sitio de SharePoint.|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|Devuelve una lista de estados de programación admitidos.|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|Pausa la ejecución de una programación determinada.|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|Reanuda una programación compartida que se ha pausado.|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|Establece las propiedades de un plan de actualización de caché.|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|Establece el valor de las propiedades de una programación compartida.|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)   
 [Métodos del servicio web del servidor de informes](report-server-web-service-methods.md)   
 [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
