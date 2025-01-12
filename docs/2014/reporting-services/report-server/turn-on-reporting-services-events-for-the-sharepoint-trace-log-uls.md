---
title: Activar eventos de Reporting Services para el registro de seguimiento de SharePoint (ULS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 81110ef6-4289-405c-a931-e7e9f49e69ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b292805f0cf24a220223adc3a1996b3e5effe54c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103160"
---
# <a name="turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls"></a>Activar eventos de Reporting Services para el registro de seguimiento de SharePoint (ULS)
  A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], los servidores de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en modo de SharePoint pueden escribir los eventos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en el registro de seguimiento del Servicio de creación de registros unificado (ULS). [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] están disponibles en la página Supervisión de Administración central de SharePoint.  
  
 En este tema:  
  
-   [Recomendaciones generales para el registro ULS](#bkmk_general)  
  
-   [Para activar y desactivar eventos de Reporting Services en la categoría de Reporting Services](#bkmk_turnon)  
  
-   [Configuración recomendada](#bkmk_recommended)  
  
-   [Lectura de las entradas de registro](#bkmk_readentries)  
  
-   [Lista de eventos de SQL Server Reporting Services](#bkmk_list)  
  
-   [Ver un archivo de registro con PowerShell](#bkmk_powershell)  
  
-   [Ubicación del registro de seguimiento](#bkmk_trace)  
  
##  <a name="bkmk_general"></a> Recomendaciones generales para el registro ULS  
 En la tabla siguiente se enumeran los niveles y categorías de eventos que se recomiendan para supervisar un entorno de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Cuando se registra un evento, cada entrada incluye el momento en que se registró, el nombre del proceso y el identificador de subproceso.  
  
|Category|Nivel|Descripción|  
|--------------|-----------|-----------------|  
|Base de datos|Verbose|Registra eventos que implican el acceso a bases de datos.|  
|General|Verbose|Registra eventos que implican el acceso a los elementos siguientes:<br /><br /> [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] páginas Web<br /><br /> Controlador HTTP del visor de informes<br /><br /> Acceso a informes (archivos .rdl)<br /><br /> Orígenes de datos (archivos .rsds)<br /><br /> Direcciones URL en el sitio de SharePoint (archivos .smdl)|  
|Office Server General|Excepción|Registra errores de inicio de sesión.|  
|Topología|Verbose|Registra información del usuario actual.|  
|elementos web|Verbose|Registra eventos que implican el acceso al elemento web Visor de informes.|  
  
##  <a name="bkmk_turnon"></a> Para activar y desactivar eventos de Reporting Services en la categoría de Reporting Services  
  
1.  En Administración central de SharePoint  
  
2.  Haga clic en **Supervisión**.  
  
3.  Haga clic en **Configurar el registro de diagnósticos** en el grupo **Informes** .  
  
4.  Busque **SQL Server Reporting Services** en la lista de categorías.  
  
5.  Haga clic en el signo más (+) para expandir las subcategorías en **SQL Server Reporting Services**.  
  
6.  Seleccione las categoría secundarias que se van a agregar al registro de seguimiento.  
  
7.  En la parte inferior de la lista de categorías, seleccione un nivel de evento para el **Evento crítico mínimo para notificar al registro de seguimiento**. Seleccione **Ninguno** para deshabilitar el seguimiento.  
  
> [!NOTE]  
>  **no admite la opción** Evento crítico mínimo para notificar al registro de eventos [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Se omitirá la opción.  
  
##  <a name="bkmk_recommended"></a> Configuración recomendada  
 Las siguientes opciones de registro son la configuración estándar recomendada:  
  
-   **Redirector de HTTP**  
  
-   **Proxy de cliente SOAP**  
  
-   Si tiene problemas de configuración, agregue **Páginas de configuración**.  
  
 Puede revisar todos los valores del registro de diagnóstico de la granja de servidores con el cmdlet de PowerShell siguiente:  
  
```  
Get-SPDiagnosticConfig  
```  
  
##  <a name="bkmk_readentries"></a> Lectura de las entradas de registro  
 El formato de las entradas de registro de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] es el siguiente.  
  
1.  **Producto: SQL Server Reporting Services.**  
  
2.  **Categoría:** Los eventos relacionados con el servidor tendrán los caracteres "Servidor de informes", al principio del nombre. Por ejemplo, "Tiempo de ejecución de alertas del servidor de informes". Estos eventos se registran también en los archivos de registro del servidor de informes.  
  
3.  **Categoría:** Los eventos relacionados o comunicados desde un componente front-end web no contendrán "Servidor de informes". Por ejemplo, "Proxy de aplicación de servicio - Tiempo de ejecución de alertas del servidor de informes". Las entradas de WFE contienen un CorrelationID pero no así las entradas del servidor.  
  
##  <a name="bkmk_list"></a> Lista de eventos de SQL Server Reporting Services  
 La tabla siguiente contiene una lista de eventos de la categoría SQL Server Reporting Services:  
  
|Nombre del área|Entradas de descripción o ejemplo|  
|---------------|-----------------------------------|  
|Páginas de configuración||  
|Redirector de HTTP||  
|Procesamiento de modo local||  
|Representación de modo local||  
|Proxy de cliente SOAP||  
|Páginas de la interfaz de usuario||  
|Power View|Entradas del registro escritas en la API de **LogClientTraceEvents** . Estas entradas se obtienen de aplicaciones cliente, como [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del complemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.<br /><br /> Todas las entradas de la API LogClientTraceEvents se registrarán en la **Categoría** de "SQL Server Reporting Services" y el **Área** de "Vista avanzada".<br /><br /> El contenido de las entradas registradas con el área de "Vista avanzada" viene determinado por la aplicación cliente.|  
|Tiempo de ejecución de alertas del servidor de informes||  
|Administrador de dominios de aplicación del servidor de informes||  
|Respuesta en búfer del servidor de informes||  
|Caché del servidor de informes||  
|Catálogo del servidor de informes||  
|Fragmento del servidor de informes||  
|Limpieza del servidor de informes||  
|Administrador de configuración del servidor de informes|Entradas de ejemplo:<br /><br /> Dirección URL interna del servidor de informes MediumUsing http://localhost:80/ReportServer.<br /><br /> Configuración UnexpectedMissing o ExtendedProtectionLevel no válido|  
|Criptografía del servidor de informes||  
|Extensión de datos del servidor de informes||  
|Sondeo de base de datos del servidor de informes||  
|Predeterminado del servidor de informes||  
|Extensión de correo electrónico del servidor de informes||  
|Representador de Excel del servidor de informes||  
|Fábrica de extensiones del servidor de informes||  
|Tiempo de ejecución HTTP del servidor de informes||  
|Representador de imágenes del servidor de informes||  
|Supervisión de la memoria del servidor de informes||  
|Notificación del servidor de informes||  
|Procesamiento del servidor de informes||  
|Proveedor del servidor de informes||  
|Representación del servidor de informes||  
|Vista previa de informes del servidor de informes||  
|Utilidad de recursos del servidor de informes|Entradas de ejemplo:<br /><br /> SKU de inicio de MediumReporting Services: Evaluation<br /><br /> Copia de MediumEvaluation: 180 días restantes|  
|Trabajos en ejecución del servidor de informes||  
|Solicitudes en ejecución del servidor de informes||  
|Programación del servidor de informes||  
|Seguridad del servidor de informes||  
|Controlador del servicio del servidor de informes||  
|Sesión del servidor de informes||  
|Suscripción del servidor de informes||  
|Tiempo de ejecución WCF del servidor de informes||  
|Servidor web del servidor de informes||  
|Proxy de aplicación de servicio||  
|Servicio compartido|Entradas de ejemplo:<br /><br /> MediumUpdating ReportingWebServiceApplication<br /><br /> Acceso de MediumGranting a las bases de datos de contenido.<br /><br /> Instancias de MediumProvisioning para ReportingWebServiceApplication<br /><br /> Cambio de la cuenta de servicio de MediumProcessing para ReportingWebServiceApplication<br /><br /> Permisos de base de datos de MediumSetting.|  
  
##  <a name="bkmk_powershell"></a> Ver un archivo de registro con PowerShell  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")Puede usar PowerShell para devolver una lista de los eventos relacionados con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] de un archivo de registro de ULS. Escriba el comando siguiente desde el Shell de administración de SharePoint 2010 para devolver una lista filtrada de filas desde el archivo de registro ULS UESQL11SPOINT-20110606-1530.log, que contiene "**sql server reporting services**":  
  
```  
Get-content -path "C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS\UESQL11SPOINT-20110606-1530.log" | select-string "sql server reporting services"  
```  
  
 Hay también muchas herramientas que puede descargar para leer registros ULS. Por ejemplo, el [visor de registros de SharePoint](http://sharepointlogviewer.codeplex.com/) o el [visor de registros ULS de SharePoint](http://ulsviewer.codeplex.com/workitem/list/basic). Ambos están disponibles en CodePlex.  
  
 Para más información sobre cómo usar PowerShell para ver datos de registro, vea [Visualización de registros de diagnóstico (SharePoint Server 2010)](https://technet.microsoft.com/library/ff463595.aspx).  
  
##  <a name="bkmk_trace"></a> Ubicación del registro de seguimiento  
 Los archivos de registro de seguimiento se encuentran normalmente en la carpeta **c:\Archivos de programa\Common files\Microsoft Shared\Web Server Extensions\14\logs** , pero puede comprobar o cambiar la ruta de acceso en la página **Registro de diagnóstico** de Administración central de SharePoint.  
  
 Para más información y conocer los pasos para configurar el registro de diagnóstico en un servidor de SharePoint en Administración Central de SharePoint 2010, vea [Configuración de las opciones del registro de diagnóstico (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkID=114423).  
  
  
