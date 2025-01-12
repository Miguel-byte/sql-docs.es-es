---
title: Usar instrucciones con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ddd61d15e3c363766c7e49b8e9045b60a7be164
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025792"
---
# <a name="using-statements-with-the-jdbc-driver"></a>Empleo de instrucciones con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se puede usar para trabajar con datos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de distintos modos. El controlador JDBC se puede usar para ejecutar instrucciones de SQL contra la base de datos o para llamar a procedimientos almacenados en la base de datos, empleando parámetros de entrada y de salida. El controlador JDBC también admite el uso de secuencias de escape de SQL, claves generadas automáticamente y actualizaciones realizadas dentro de una operación por lotes.  
  
El controlador JDBC proporciona tres clases para la recuperación de datos desde una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), para ejecutar instrucciones de SQL sin parámetros.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (heredada de SQLServerStatement), para ejecutar instrucciones de SQL compiladas que pueden contener parámetros IN.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), (heredada de SQLServerPreparedStatement), para ejecutar procedimientos almacenados que pueden contener parámetros IN, OUT o de ambos tipos.  
  
 En los temas de esta sección se trata cómo usar cada una de estas tres clases de instrucciones para trabajar con datos de una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  

| Tema                                                                                                    | Descripción                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Empleo de instrucciones con SQL](../../connect/jdbc/using-statements-with-sql.md)                             | Describe cómo usar instrucciones SQL con el controlador JDBC para trabajar con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    |
| [Empleo de instrucciones con procedimientos almacenados](../../connect/jdbc/using-statements-with-stored-procedures.md) | Describe cómo usar procedimientos almacenados con el controlador JDBC para trabajar con datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Empleo de varios conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)                           | Describe cómo usar el controlador JDBC para recuperar datos de varios conjuntos de resultados.                                                                       |
| [Empleo de secuencias de escape de SQL](../../connect/jdbc/using-sql-escape-sequences.md)                           | Describe cómo usar secuencias de escape de SQL, como literales y funciones de fecha y hora.                                                               |
| [Empleo de claves generadas automáticamente](../../connect/jdbc/using-auto-generated-keys.md)                             | Describe cómo usar claves generadas automáticamente.                                                                                                     |
| [Realización de operaciones por lotes](../../connect/jdbc/performing-batch-operations.md)                         | Describe cómo usar el controlador JDBC para llevar a cabo operaciones en lote.                                                                                      |
| [Control de instrucciones complejas](../../connect/jdbc/handling-complex-statements.md)                         | Describe cómo usar el controlador JDBC para ejecutar instrucciones complejas que realizan diversas tareas y pueden devolver tipos diferentes de datos.               |
  
## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
