---
title: Ver y leer los archivos de registro de instalación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7bf7d199239be10760df49d586cdf5048fbc4a80
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "67906769"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>Ver y leer los archivos de registro de instalación de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El programa de instalación de SQL Server crea archivos de registro en una carpeta con fecha y marca de tiempo en **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** de forma predeterminada, donde *nnn* son los números que se corresponden a la versión de SQL que se va a instalar. El formato del nombre de la carpeta de registro con marca de tiempo es AAAAMMDD_hhmmss. Cuando el programa de instalación se ejecuta en modo desatendido, los registros se crean en %temp%\sqlsetup*.log. Todos los archivos de la carpeta de registro se almacenan en el archivo Log\*.cab en su carpeta de registro correspondiente.  

   | Archivo           | Ruta de acceso |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<NombreDelEquipo>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **Archivos de registro de MSI** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Nombre>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Para las instalaciones desatendidas** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > Los números de la ruta de acceso *nnn* corresponden a la versión de SQL que se va a instalar. En la imagen anterior se ha instalado SQL 2017, por lo que la carpeta es 140. En el caso de SQL 2016, la carpeta sería 130 y, en el caso de SQL 2014, la carpeta sería 120.
  
 El programa de instalación de SQL server lleva a cabo tres fases básicas: 
  
1.  Comprobación de reglas globales: valida los requisitos básicos del sistema
2.  Actualización de componentes: comprueba si hay actualizaciones disponibles para los medios que se van a instalar
3.  Acción solicitada por el usuario: permite al usuario seleccionar y personalizar características
  

Este flujo de trabajo genera un único registro de resumen y un registro de detalle único para una instalación básica de SQL Server, o bien dos registros de detalle para cuando se instala una actualización, por ejemplo, un Service Pack, junto con la instalación básica. 
  
Además, hay archivos de almacén de datos que contienen una instantánea del estado de todos los objetos de configuración sometidos a seguimiento por el proceso de instalación y son útiles para solucionar errores de configuración. Para cada fase de ejecución se crean archivos de volcado XML, que se guardan en la subcarpeta de registro del almacén de datos de la carpeta de registro con marca de tiempo. 

En las secciones siguientes se describen los archivos de registro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="summarytxt-file"></a>Archivo Summary.txt 
  
### <a name="overview"></a>Información general  
 Este archivo muestra los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se detectaron durante la instalación, el entorno del sistema operativo, los valores de parámetros de línea de comandos, si se especifican, y el estado general de cada MSI/MSP que se ejecutó.
  
 El registro se organiza en las secciones siguientes:
  
-   Un resumen general de la ejecución  
-   Las propiedades y la configuración del equipo en el que se ejecutó el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas anteriormente en el equipo  
-   Descripción de la versión de instalación y las propiedades del paquete de instalación
-   Configuración de entrada en tiempo de ejecución proporcionada durante la instalación  
-   Ubicación del archivo de configuración  
-   Detalles de los resultados de la ejecución  
-   Reglas globales  
-   Reglas específicas del escenario de instalación  
-   Reglas con errores  
-   Ubicación del archivo de informe de reglas


  >[!NOTE]
  > Tenga en cuenta que, al aplicar una revisión, puede haber una serie de subcarpetas (una para cada instancia a la que se aplique la revisión y otra para las características compartidas) que contienen un conjunto similar de archivos (es decir, %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<AAAAMMDD_HHMM>\MSSQLSERVER). 
  
### <a name="location"></a>Ubicación  
 El archivo summary.txt se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 Para encontrar errores en el archivo de texto de resumen, busque en el archivo usando las palabras clave "error" o "failed".
  
## <a name="summary_machinename_yyyymmdd_hhmmsstxt-file"></a>Archivo Summary_\<MachineName>_AAAAMMDD_HHMMss.txt
  
### <a name="overview"></a>Información general  
 El archivo base de registro de resumen es similar al archivo de resumen y se genera durante el flujo de trabajo principal.
  
### <a name="location"></a>Ubicación  
 El archivo Summary_\<MachineName>_AAAAMMDD_HHMMss.txt se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\.
  
  
## <a name="detailtxt-file"></a>Archivo Detail.txt
  
### <a name="overview"></a>Información general
 El archivo Detail.txt se genera durante el flujo de trabajo principal, como la instalación o la actualización, y proporciona los detalles de la ejecución. Los registros del archivo se generan según la hora a la que se invocó cada acción de la instalación. En el archivo de texto se muestra el orden en el que se ejecutaron las acciones, así como sus dependencias.  
  
### <a name="location"></a>Ubicación  
 El archivo detail.txt se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\Detail.txt.  
  
 Si se produce un error durante el proceso de instalación, la excepción o el error se registran al final de este archivo. Para encontrar los errores en este archivo, examine primero el final del archivo y, después, realice una búsqueda en el mismo usando las palabras clave "error" o "exception"
    
## <a name="msi-log-files"></a>Archivos de registro de MSI
  
### <a name="overview"></a>Información general  
 Los archivos de registro de MSI proporcionan detalles del proceso de paquete de instalación. Los genera el programa MSIEXEC durante la instalación del paquete especificado.  
  
 Tipos de archivos de registro de MSI:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>Ubicación  
 Los archivos de registro de MSI se encuentran en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\<Nombre\>.log.  
  
 Al final del archivo se encuentra un resumen de la ejecución, que incluye el estado de corrección o error y las propiedades. Para encontrar el error en el archivo MSI, busque "value 3" y revise el texto anterior y posterior.  
  
## <a name="configurationfileini-file"></a>Archivo ConfigurationFile.ini
  
### <a name="overview"></a>Información general  
 El archivo de configuración contiene la configuración de entrada que se proporciona durante la instalación. Se puede usar para reiniciar la instalación sin tener que especificar la configuración manualmente. Sin embargo, las contraseñas de las cuentas, los PID y algunos parámetros no se guardan en el archivo de configuración. La configuración se puede agregar al archivo o se puede proporcionar usando la línea de comandos o la interfaz de usuario del programa de instalación. Para obtener más información, vea [Instalar SQL Server 2016 mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### <a name="location"></a>Ubicación  
 El archivo ConfigurationFile.ini se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\.  
  
## <a name="systemconfigurationcheck_reporthtm-file"></a>Archivo SystemConfigurationCheck_Report.htm
  
### <a name="overview"></a>Información general  
 El informe de comprobación de la configuración del sistema contiene una descripción breve de cada regla ejecutada y el estado de ejecución.
  
### <a name="location"></a>Ubicación  
El archivo SystemConfigurationCheck_Report.htm se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## <a name="see-also"></a>Vea también  
 [Instalar SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)
