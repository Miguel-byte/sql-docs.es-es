---
title: 'Lección 9: Compilar y ejecutar la aplicación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 321075631a48570a80e8294f992e8ddb17d50bd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108382"
---
# <a name="lesson-9-build-and-run-the-application"></a>Lección 9: Generación y ejecución de la aplicación
  Después de crear un filtro para los datos de la tabla de datos, el paso siguiente consiste en generar y ejecutar la aplicación del sitio Web.  
  
### <a name="to-build-and-run-the-application"></a>Para generar y ejecutar la aplicación  
  
1.  Pulse **CTRL+F5** para ejecutar la página Default.aspx sin depurar o pulse F5 para ejecutar la página con la depuración.  
  
     Como parte del proceso de compilación, se compila el informe y los errores detectados (por ejemplo, un error de sintaxis en una expresión usada en el informe) se agregan a la **Lista de tareas** que se encuentra en la parte inferior de la ventana de Visual Studio.  
  
     La página Web aparece en el explorador. El control ReportViewer muestra el informe. Puede utilizar la barra de herramientas para navegar por el informe, ampliarlo y exportarlo a Excel.  
  
2.  Mantenga el mouse sobre alguna de las filas bajo la columna **Nombre** . El cursor del mouse mostrará un símbolo de mano.  
  
3.  Haga clic en un valor de la columna **Nombre** . El informe secundario se muestra con los datos filtrados correspondientes.  
  
4.  Haga clic en el icono, **Volver al informe primario**, en la barra de herramientas de **ReportViewer** para navegar de nuevo al informe **Primario** .  
  
     ![explorar en SSRS a través del uso de ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "profundizar ssrs a través del uso de ReportViewer")  
  
5.  Cierre el explorador para salir.  
  
  
