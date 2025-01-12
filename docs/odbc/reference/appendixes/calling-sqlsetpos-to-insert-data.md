---
title: Llamar a SQLSetPos para insertar datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037708"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Llamar a SQLSetPos para insertar datos
Cuando un ODBC *2.x* la aplicación funciona con un ODBC *3.x* controlador llama a **SQLSetPos** con un *operación* argumento de SQL_ADD, el Administrador de controladores no se asigna esta llamada a **SQLBulkOperations**. Si un ODBC *3.x* controlador debería funcionar con una aplicación que llama a **SQLSetPos** con SQL_ADD, el controlador debe admitir esa operación.  
  
 Una diferencia importante en el comportamiento cuando **SQLSetPos** se llama con SQL_ADD se produce cuando se llama en estado S6. En ODBC *2.x*, el controlador devolvió S1010 cuando **SQLSetPos** se llamó con SQL_ADD en estado S6 (después de que se ha colocado el cursor con **SQLFetch**). En ODBC *3.x*, **SQLBulkOperations** con un *operación* de SQL_ADD puede llamarse en estado S6. Una segunda diferencia importante en el comportamiento es que **SQLBulkOperations** con un *operación* de SQL_ADD puede mientras se llama en estado S5, **SQLSetPos** con un  **Operación** de SQL_ADD no. Para las transiciones de instrucción que pueden aparecer para el mismo llamar en ODBC *3.x*, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
