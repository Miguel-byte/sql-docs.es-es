---
title: Especificar información de origen (Asistente para particiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aca14c9462d847d91ae2b51dfdf179650ee06732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068169"
---
# <a name="specify-source-information-partition-wizard"></a>Especificar información de origen (Asistente para particiones)
  Use la página **Especificar información de origen** para seleccionar el grupo de medida en el que desea crear la partición, así como la vista del origen de datos y las tablas de filtros de la partición.  
  
> [!CAUTION]  
>  Si especifica una tabla en **Tablas disponibles** usada por otra partición, deberá proporcionar una consulta en la página **Restringir filas** para evitar duplicar datos en el cubo.  
  
## <a name="options"></a>Opciones  
 **Grupo de medida**  
 Seleccione un grupo de medida para la partición.  
  
 **Look in**  
 Seleccione el origen de datos o la vista del origen de datos que contiene las tablas de origen para la partición. La vista del origen de datos utilizada por el grupo de medida aparece seleccionada de forma predeterminada.  
  
 **Tablas de filtros**  
 Escriba la cadena que quiere usar para restringir las tablas mostradas en **Tablas disponibles**con el nombre de la tabla.  
  
 **Buscar tablas**  
 Seleccione esta opción para actualizar la lista de tablas de **Tablas disponibles**y restringir la lista si se ha especificado una cadena en **Tablas de filtros**.  
  
 **Tablas disponibles**  
 Seleccione las tablas que desea utilizar como tablas de origen para las particiones. El **Asistente para particiones** crea una partición para cada una de las tablas seleccionadas en **Tablas disponibles**.  
  
 Si no ha especificado ningún filtro en **Tablas de filtros**, esta opción mostrará la lista de todas las tablas en el origen de datos o en la vista del origen de datos especificados en **Buscar en** que presenten una estructura similar a la tabla de hechos utilizada por el grupo de medida especificado en **Grupo de medida**.  
  
 Si ha especificado un filtro en **Tablas de filtros**, podrá restringir aún más la lista mediante la comparación del filtro con los nombres de tabla que cumplen los criterios anteriores. Solo se mostrarán las tablas que contengan la cadena especificada en **Tablas de filtros** .  
  
> [!NOTE]  
>  Si selecciona más de una tabla, no podrá mostrarse la página **Restringir filas** y no podrán restringirse las filas para las particiones creadas a partir de las tablas seleccionadas. Para restringir filas en las particiones, ejecute el Asistente para particiones para cada tabla en la que desea crear una partición.  
  
## <a name="see-also"></a>Vea también  
 [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
