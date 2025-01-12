---
title: Clase de eventos Showplan Text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan Text event class
ms.assetid: f36c73b2-a1d1-4513-9594-78818f3fcb0d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6108a35d3f1c51f4d3dedbcf673be1d837091b71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62692072"
---
# <a name="showplan-text-event-class"></a>Showplan Text, clase de eventos
  La clase de eventos Showplan Text se produce cuando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta una instrucción SQL. La información contenida es un subconjunto de la información disponible en las clases de eventos Showplan All, Showplan XML Statistics Profile o Showplan XML.  
  
 Cuando la clase de eventos Showplan Text se incluye en un seguimiento, la sobrecarga dificultará el rendimiento de forma significativa. Para minimizar este riesgo, limite el uso de esta clase de eventos a los seguimientos que supervisen problemas específicos durante periodos breves. Showplan Text no implicará tanta sobrecarga como otras clases de eventos del plan de presentación.  
  
 Cuando la clase de eventos Showplan Text se incluye en un seguimiento, debe seleccionarse la columna de datos BinaryData. Si no se incluye, la información de esta clase de eventos no se mostrará en el seguimiento.  
  
## <a name="showplan-text-event-class-data-columns"></a>Columnas de datos de la clase de eventos Showplan Text  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BinaryData|`image`|Costo estimado del texto de Showplan.|2|No|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|Clase de eventos|`int`|Tipo de evento = 96.|27|Sin|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|Integer Data|`integer`|Número estimado de filas devueltas.|25|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LineNumber|`int`|Muestra el número de la línea que contiene el error.|5|Sí|  
|Login SID|`bitmap`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sin|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|NestLevel|`int`|Valor entero que representa los datos devueltos por @@NESTLEVEL.|29|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|ObjectID|`int`|Identificador del objeto asignado por el sistema.|22|Sí|  
|ObjectName|`nvarchar`|Nombre del objeto al que se hace referencia.|34|Sí|  
|ObjectType|`int`|Valor que representa el tipo del objeto implicado en el evento. Este valor corresponde al de la columna Type de la tabla sys.objects. Para ver los valores, vea [Columna de evento de seguimiento ObjectType](objecttype-trace-event-column.md).|28|Sí|  
|IdSolicitud|`int`|Solicita la identificación que inició la consulta de texto completo.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que se utiliza para describir la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Referencia de operadores lógicos y físicos del plan de presentación](../showplan-logical-and-physical-operators-reference.md)   
 [Showplan All (clase de eventos)](showplan-all-event-class.md)   
 [Showplan XML Statistics Profile (clase de eventos)](showplan-xml-statistics-profile-event-class.md)   
 [Showplan XML (clase de eventos)](showplan-xml-event-class.md)  
  
  
