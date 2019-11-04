---
title: Importar y exportar datos con el Asistente para importación y exportación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e8838c92e2af7ca79ad1aa69972e46be0a1f64c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296275"
---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importar y exportar datos con el Asistente para importación y exportación de SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



 El Asistente para la  importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece una manera sencilla y rápida de copiar datos desde un origen a un destino. En esta introducción se describen los orígenes de datos que el asistente puede usar como orígenes y destinos, así como los permisos que necesita para ejecutar al asistente.

## <a name="get-the-wizard"></a>Obtener el asistente
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="what-happens-when-i-run-the-wizard"></a>¿Qué ocurre cuando ejecuto el asistente?
-    **Consulte la lista de pasos.** Para obtener una descripción de los pasos del asistente, consulte [Pasos del asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). También hay una página independiente de documentación para cada página del asistente.  
    \- o \-
-   **Vea un ejemplo.** Para obtener una visión rápida de las distintas pantallas que se muestran en una sesión típica, eche un vistazo a este sencillo y completo ejemplo en una sola página: [Comenzar con este sencillo ejemplo del Asistente para importación y exportación](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).  

##  <a name="wizardSources"></a> ¿Qué orígenes y destinos puedo usar?  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar datos de y en los orígenes de datos que se enumeran en la tabla siguiente. Para conectarse a algunos de estos orígenes de datos, quizá necesite descargar e instalar archivos adicionales.
 
| Origen de datos | ¿Es necesario descargar archivos adicionales? |
|-------------|-----------------------------------------|
|**Bases de datos empresariales**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 y otros.|SQL Server o SQL Server Data Tools (SSDT) instalan los archivos que necesita para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, SSDT no instala todos los archivos que necesita para conectarse a otras bases de datos empresariales, como Oracle o IBM DB2.<br/><br/>Para conectarse a una base de datos empresarial, normalmente deberá tener dos cosas:<br/><br/>1. **Software cliente**. Si ya tiene el software cliente instalado en el sistema de base de datos empresarial, por lo general ya dispone de lo necesario para establecer una conexión. Si no tiene instalado el software cliente, consulte al administrador de base de datos cómo instalar una copia con licencia.<br/><br/>2. **Controladores o proveedores**. Microsoft instala controladores y proveedores para conectarse a Oracle. Para conectarse a IBM DB2, obtenga el proveedor Microsoft OLE DB para DB2 v5.0 para Microsoft SQL Server de [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).<br/><br/>Para obtener más información, vea [Conectarse a un origen de datos de SQL Server](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md) o [Conectarse a un origen de datos de Oracle](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md).|
|**Archivos de texto** (archivos planos)|No se necesitan archivos adicionales.<br/><br/>Para obtener más información, consulte [Connect to a Flat File Data Source](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md) (Conectarse al origen de datos de un archivo plano).|
|**Archivos de Microsoft Excel y Microsoft Access**|Microsoft Office no instala todos los archivos que necesita para conectarse a archivos de Excel y Access como orígenes de datos. Obtenga la descarga siguiente: [Componente redistribuible del motor de base de datos de Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).<br/><br/>Para obtener más información, vea [Conexión a un origen de datos de Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) o [Conectarse a un origen de datos de Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Orígenes de datos de Azure**<br/>Actualmente, solo Almacenamiento de blobs de Azure.|SQL Server Data Tools no instala los archivos que necesita para conectarse a Azure Blob Storage como origen de datos. Obtenga la descarga siguiente: [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)(Feature Pack de Microsoft SQL Server 2016 Integration Services para Azure).<br/><br/>Para obtener más información, vea [Creación y administración de blobs en Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Bases de datos de código abierto**<br/>PostgreSQL, MySql y otros.|Para conectarse a estos orígenes de datos, tiene que descargar archivos adicionales.<br/><br/>- Para **PostgreSQL**, consulte [Connect to a PostgreSQL Data Source](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md) (Conectarse a un origen de datos de PostgreSQL).<br/>- Para **PostgreSQL**, consulte [Connect to a MySQL Data Source](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md) (Conectarse a un origen de datos de MySQL).|
|**Cualquier otro origen de datos para el que esté disponible un controlador o un proveedor**|Normalmente tiene que descargar archivos adicionales para conectarse a los siguientes tipos de orígenes de datos.<br/><br/>- Cualquier origen para el que esté disponible un **controlador ODBC** . Para obtener más información, consulte [Conectarse a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).<br/>- Cualquier origen para el que esté disponible un **proveedor de datos .NET Framework** .<br/>- Cualquier origen para el que esté disponible un **proveedor OLE DB** .<br/><br/>Los componentes de terceros que proporcionan funcionalidades de origen y destino para otros orígenes de datos se comercializan a veces como complementos de SQL Server Integration Services (SSIS).|

## <a name="how-do-i-connect-to-my-data"></a>¿Cómo me conecto a mis datos?
Para obtener información sobre cómo conectarse a un destino de uso frecuente, consulte una de las páginas siguientes:
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a archivos planos (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectarse con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Para obtener más información sobre cómo conectarse a un origen de datos que no aparezca en esta lista, consulte [The Connection Strings Reference (Referencia de cadenas de conexión)](https://www.connectionstrings.com/). Este sitio de terceros contiene cadenas de conexión de ejemplo y más información acerca de los proveedores de datos y la conexión que estos necesitan.

## <a name="what-permissions-do-i-need"></a>¿Qué permisos necesito?  
 Para ejecutar correctamente el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe disponer como mínimo de los siguientes permisos. Si ya trabaja con el origen y el destino de datos, probablemente cuente con los permisos necesarios.
  
|Necesita permisos para estas acciones|Si se conecta a SQL Server, necesita los permisos específicos siguientes: |  
|-------------------------|----------------------------------------------------|  
|Conectarse a las bases de datos o recursos compartidos de archivos de origen y de destino.|Derechos de inicio de sesión del servidor y de la base de datos.|  
|Exportar o leer datos desde la base de datos o el archivo de origen.|Permisos SELECT en las tablas y vistas de origen.|  
|Importar o escribir datos en la base de datos o el archivo de destino.|Permisos INSERT en las tablas de destino.|  
|Crear la base de datos o el archivo de destino, si procede.|Permisos CREATE DATABASE o CREATE TABLE.|  
|Guardar el paquete SSIS creado por el asistente, si procede.|Si quiere guardar el paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permisos suficientes para guardar el paquete en la base de datos **msdb** .|  
  
## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   
  
##  <a name="wizardSSIS"></a> El asistente usa SQL Server Integration Services (SSIS)  
 El asistente usa SQL Server Integration Services (SSIS) para copiar datos. SSIS es una herramienta para la extracción, transformación y carga (ETL) de datos. Las páginas del asistente usan parte del idioma de SSIS.
  
 En SSIS, la unidad básica es el **paquete**. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.    
  
Al final del asistente, si tiene instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o una versión superior, puede guardar el paquete de SSIS. Después podrá volver a usar el paquete o ampliarlo usando el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para agregar tareas, transformaciones y lógica controlada por eventos. El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece la manera más simple para crear un paquete básico de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que copia datos de un origen en un destino.

Para obtener más información sobre SSIS, vea [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="whats-next"></a>¿Qué sigue?  
 Inicie el asistente. Para obtener más información, vea [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)(Iniciar el Asistente para importación y exportación de SQL Server).  

## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)


