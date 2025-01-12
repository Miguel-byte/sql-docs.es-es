---
title: Lote de procesamiento (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- batches [Analysis Services]
ms.assetid: ba4dcf72-0667-41d0-816b-ab8ff9a7d9cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c54c374bc5dd6b7bea30a95cb84f5e9365f0e75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076938"
---
# <a name="batch-processing-analysis-services"></a>Procesamiento por lotes (Analysis Services)
  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede usar el comando Batch para enviar varios comandos de procesamiento al servidor en una única solicitud. El procesamiento por lotes ofrece una forma de controlar qué objetos se deben procesar y en qué orden. Además, un lote se puede ejecutar como una serie de trabajos independientes o como una transacción en la que un error en un proceso causa la reversión del lote completo.  
  
 El procesamiento por lotes maximiza la disponibilidad de datos consolidando y reduciendo el tiempo empleado en confirmar los cambios. Cuando se procesa totalmente una dimensión, cualquier partición que usa dicha dimensión se marca como sin procesar. Como resultado, los cubos que contienen las particiones sin procesar no están disponibles para búsquedas. Puede solucionar esto con un trabajo de procesamiento por lotes mediante el procesamiento de las dimensiones junto con las particiones afectadas. La ejecución del trabajo de procesamiento por lotes como una transacción asegura que todos los objetos incluidos en la transacción permanezcan disponibles para consultas hasta que se complete todo el procesamiento. Mientras la transacción confirma los cambios, se aplican bloqueos en los objetos afectados, por lo que estos no están disponibles temporalmente, pero en general la cantidad de tiempo empleado para confirmar los cambios es inferior a la que se emplearía procesando los objetos individualmente.  
  
 Los procedimientos de este tema muestran los pasos para procesar completamente dimensiones y particiones. El procesamiento por lotes también puede incluir otras opciones de procesamiento, como el procesamiento incremental. Para que estos procedimientos funcionen correctamente, debe usar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente que contenga al menos dos dimensiones y una partición.  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Procesamiento por lotes en SQL Server Data Tools](#bkmk_ssdt)  
  
 [Procesamiento por lotes con XMLA en Management Studio](#bkmk_xmla)  
  
##  <a name="bkmk_ssdt"></a> Procesamiento por lotes en SQL Server Data Tools  
 Para poder procesar objetos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], se debe implementar el proyecto que contiene los objetos. Para más información, vea [Implementar proyectos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md).  
  
1.  Abra [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
2.  Abra un proyecto que se haya implementado.  
  
3.  En el Explorador de soluciones, debajo del proyecto implementado, expanda la carpeta **Dimensiones** .  
  
4.  Manteniendo presionada la tecla Ctrl, haga clic en todas las dimensiones que aparecen en la carpeta **Dimensiones** .  
  
5.  Haga clic con el botón derecho en las dimensiones seleccionadas y luego haga clic en **Procesar**.  
  
6.  Manteniendo presionada la tecla Ctrl, haga clic en todas las dimensiones que aparecen en la **lista de objetos**.  
  
7.  Haga clic con el botón derecho en las dimensiones seleccionadas y seleccione **Proceso completo**.  
  
8.  Para personalizar el trabajo de proceso por lotes, haga clic en **Cambiar configuración**.  
  
9. En **Opciones de procesamiento**, marque la siguiente configuración:  
  
    -   La opción**Orden de procesamiento** establecida en **Secuenciales**y la opción **Modo de transacción** establecida en **Una transacción**.  
  
    -   La opción**Opción de tabla de reescritura** establecida en **Utilizar existente**.  
  
    -   En **Objetos afectados**, active la casilla **Procesar objetos afectados** .  
  
10. Haga clic en la pestaña **Errores de clave de dimensión** . Compruebe que la opción **Utilizar la configuración de error predeterminada** esté activada.  
  
11. Haga clic en **Aceptar** para cerrar la pantalla **Cambiar configuración** .  
  
12. Haga clic en **Ejecutar** en la pantalla **Procesar objetos** para iniciar el trabajo de procesamiento.  
  
13. Cuando en el cuadro **Estado** se muestre **Proceso finalizado correctamente**, haga clic en **Cerrar**.  
  
14. Haga clic en **Cerrar** en la pantalla **Procesar objetos** .  
  
##  <a name="bkmk_xmla"></a> Procesamiento por lotes con XMLA en Management Studio  
 Puede crear un script XMLA que realice el procesamiento por lotes. Comience por generar un script XMLA en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para cada objeto y, a continuación combínelos en una única consulta XMLA que puede ejecutar interactivamente o en una tarea programada.  
  
 Para obtener enstrucciones paso a paso, vea **Ejemplo 2** en [Schedule SSAS Admenistrative Tasks with SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md).  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)  
  
  
