---
title: Editor de transformación búsqueda (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.columns.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: 690ffef5-fd59-4e95-a27d-4fcf0d6b1c0b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1a32dcbcee6704cb4fecef7b58cbff8354b910a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057895"
---
# <a name="lookup-transformation-editor-columns-page"></a>Editor de transformación Búsqueda (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de transformación Búsqueda** para especificar la combinación entre la tabla de origen y la tabla de referencia, y para seleccionar columnas de búsqueda de la tabla de referencia.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Las columnas de entrada son las columnas del flujo de datos de un origen conectado. Las columnas de entrada y la columna de búsqueda deben tener tipos de datos coincidentes.  
  
 Utilice una operación de arrastrar y colocar para asignar columnas de entrada disponibles a columnas de búsqueda.  
  
 También puede asignar columnas de entrada a columnas de búsqueda utilizando el teclado, resaltando una columna en la tabla **Columnas de entrada disponibles** , presionando la tecla de aplicación y haciendo clic en **Editar asignaciones**a continuación.  
  
 **Columnas de búsqueda disponibles**  
 Muestra la lista de columnas de búsqueda. Las columnas de búsqueda son columnas de la tabla de referencia en las que desea buscar valores que coinciden con las columnas de entrada.  
  
 Utilice una operación de arrastrar y colocar para asignar columnas de búsqueda disponibles a columnas de entrada.  
  
 Use las casillas para seleccionar las columnas de búsqueda de la tabla de referencia en las que se realizarán operaciones de búsqueda.  
  
 También puede asignar columnas de búsqueda a columnas de entrada utilizando el teclado, resaltando una columna en la tabla **Columnas de búsqueda disponibles** , presionando la tecla de aplicación y haciendo clic en **Editar asignaciones**a continuación.  
  
 **columna de búsqueda**  
 Muestra las columnas de búsqueda seleccionadas. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de búsqueda disponibles** .  
  
 **Operación de búsqueda**  
 Seleccione una operación de búsqueda de la lista para llevar a cabo en la columna de búsqueda.  
  
 **Alias de salida**  
 Escriba un alias para la salida de cada columna de búsqueda. El valor predeterminado es el nombre de la columna de búsqueda; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
## <a name="see-also"></a>Vea también  
 [Editor de transformación Búsqueda &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de transformación Búsqueda &#40;página Conexión&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de transformación Búsqueda &#40;página Avanzadas&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor de transformación Búsqueda &#40;página Salida de error&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Transformación Búsqueda aproximada](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
