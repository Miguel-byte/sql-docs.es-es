---
title: Biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b81a7871434691a5940a04c7c60aaad9254b645
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201167"
---
# <a name="odbc-cursor-library"></a>Biblioteca de cursores ODBC
  Algunos controladores ODBC solo admiten los valores de cursor predeterminado; estos controladores tampoco admiten las operaciones de cursor posicionadas, como **SQLSetPos**. La biblioteca de cursores ODBC es un componente de Microsoft Data Access Components (MDAC) que se utiliza para implementar cursores de bloque o estáticos en un controlador que normalmente no los admite. La biblioteca de cursores también implementa instrucciones UPDATE y DELETE posicionadas y **SQLSetPos** para los cursores que crea.  
  
 La biblioteca de cursores ODBC se implementa como un nivel entre el Administrador de controladores ODBC y un controlador ODBC. Si se carga la biblioteca de cursores ODBC, el Administrador de controladores ODBC enruta todos los comandos relacionados con cursor a la biblioteca de cursores en lugar del controlador. Para implementar un cursor, la biblioteca de cursores implementa un cursor que captura el conjunto completo de resultados del controlador subyacente y lo almacena en la caché del cliente. Al utilizar la biblioteca de cursores ODBC, la aplicación se limita a la funcionalidad del cursor de la biblioteca de cursores; la aplicación no dispone de compatibilidad con funcionalidad adicional del cursor incluida en el controlador subyacente.  
  
 No hay gran necesidad de utilizar la biblioteca de cursores ODBC con el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ya que el propio controlador admite más funcionalidad de cursor que la biblioteca de cursores ODBC. La única razón para usar la biblioteca de cursores ODBC con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client es porque el controlador implementa su compatibilidad con cursores a través de los cursores de servidor y los cursores de servidor no admiten todas las instrucciones SQL. Considere la posibilidad de utilizar la biblioteca de cursores ODBC siempre que necesite disponer de un cursor estático con procedimientos almacenados, lotes o instrucciones SQL que contengan COMPUTE, COMPUTE BY, FOR BROWSE o INTO. Sin embargo, debe prestar atención si utiliza la biblioteca de cursores, ya que almacena en la memoria caché del cliente el conjunto de resultados completo, lo que puede consumir grandes cantidades de memoria y reducir el rendimiento.  
  
 Una aplicación invoca la biblioteca de cursores conexión por conexión mediante [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) para establecer el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse a un origen de datos. SQL_ATTR_ODBC_CURSORS se establece en uno de tres valores:  
  
 SQL_CUR_USE_ODBC  
 Cuando esta opción se establece con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, la biblioteca de cursores ODBC invalida la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de cursores nativa del controlador ODBC de Native Client. En la conexión solo se pueden utilizar los tipos de cursor que admite la biblioteca de cursores; no se pueden utilizar cursores de servidor.  
  
 SQL_CUR_USE_DRIVER  
 Cuando se establece esta opción, todas del cursor de soporte técnico nativo para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client puede utilizarse para la conexión. No se puede inicializar la biblioteca de cursores ODBC. Todos los cursores se implementan como cursores de servidor.  
  
 SQL_CUR_USE_IF_NEEDED  
 Cuando se establece esta opción, el efecto es el mismo que al utilizar SQL_CUR_USE_DRIVER cuando se usa con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. En tiempo de conexión, el Administrador de controladores ODBC se comprueba para ver si el controlador ODBC que se está conectando a es compatible con la opción SQL_FETCH_PRIOR de [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md). Si el controlador no admite la opción, el Administrador de controladores ODBC carga la biblioteca de cursores ODBC. Si el controlador admite la opción, el Administrador de controladores ODBC no carga la biblioteca de cursores ODBC y la aplicación utiliza la compatibilidad nativa del controlador. Dado que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite SQL_FETCH_PRIOR, el Administrador de controladores ODBC no carga la biblioteca de cursores ODBC.  
  
 La biblioteca de cursores permite a las aplicaciones utilizar varias instrucciones activas en una conexión, así como cursores desplazables y actualizables. La biblioteca de cursores debe estar cargada para admitir esta funcionalidad. Use [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) para especificar cómo se debe usar la biblioteca de cursores y [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para especificar el tamaño de tipo, simultaneidad y conjunto de filas del cursor.  
  
## <a name="see-also"></a>Vea también  
 [Cómo se implementan los cursores](how-cursors-are-implemented.md)  
  
  
