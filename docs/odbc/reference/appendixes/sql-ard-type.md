---
title: SQL_ARD_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802040851259a8537fabcd3cc0da1afdf9b8dbe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057055"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
El identificador del tipo SQL_ARD_TYPE se utiliza para indicar que los datos en un búfer será del tipo especificado en el campo SQL_DESC_CONCISE_TYPE de la descartar. SQL_ARD_TYPE se escribe en el *TargetType* argumento de una llamada a **SQLGetData** en lugar de un tipo de datos específica y permite escribir una aplicación para cambiar los datos del búfer cambiando el descriptor campo. Este valor bloquea el tipo de datos de la  *\*TargetValuePtr* búfer para el campo descriptor. (No se especificaron SQL_ARD_TYPE en una llamada a **SQLBindCol** o **SQLBindParameter** porque el tipo de búfer dependiente ya está asociado a los campos de SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y se puede cambiar en cualquier momento cambiando cualquiera de esos campos.)  
  
 El identificador del tipo SQL_ARD_TYPE puede usarse para especificar valores no predeterminados para la precisión de segundos de tipos de datos interval y líderes y escriba los valores de precisión y escala para los datos SQL_C_NUMERIC. Para obtener más información, consulte [reemplazar predeterminado inicial y la precisión de segundos para tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) y [reemplazar predeterminado precisión y escala para los tipos de datos numéricos](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), más adelante en este apéndice.
