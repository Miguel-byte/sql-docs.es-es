---
title: SQLSetScrollOptions (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3746d9cea2ce5ffb7d03424d7cda4fa1889aabc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905381"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Parcial  
  
 Conformidad de la API de ODBC: Nivel 2  
  
 Establece las opciones que controlan el comportamiento de los cursores asociado con un identificador de instrucción, *hstmt*.  
  
 El controlador ODBC de Visual FoxPro admite solo SQL_CONCUR_READ_ONLY; no se admite la *fConcurrency* SQL_CONCUR_ROWVER de valor. El controlador convierte SQL_KEYSET_SIZE SQL_CURSOR_DYNAMIC y SQL_CURSOR_KEYSET_DRIVEN a SQL_SCROLL_STATIC con advertencia ODBC_01S02.  
  
 Para obtener más información, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) en el *referencia del programador de ODBC*.
