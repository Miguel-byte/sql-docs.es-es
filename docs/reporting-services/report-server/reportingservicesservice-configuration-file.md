---
title: Archivo de configuración ReportingServicesService | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- traces [Reporting Services]
- Report Server Windows service, ReportingServicesService configuration file
- ReportingServicesService configuration file
ms.assetid: 40f4a401-cb61-4c42-b1ec-01acdacdacd1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dfb0f48bb35e6341e2b2a9a72007ef4eb09c2b9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506632"
---
# <a name="reportingservicesservice-configuration-file"></a>archivo de configuración ReportingServicesService

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)]
  
El archivo ReportingServicesService.exe.config incluye valores que configuran la traza.  
  
## <a name="file-location"></a>Ubicación del archivo  
Este archivo podría estar ubicado en cualquiera de las rutas de acceso siguiente:  

``` Paths  
\Reporting Services\Report Server\Bin  
\Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin  
```  
 
## <a name="editing-guidelines"></a>Directrices para editar  
 Puede modificar este archivo para cambiar el nombre del archivo de registro, o bien para aumentar o disminuir los niveles de seguimiento. No modifique ningún otro parámetro. Para obtener instrucciones, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Para más información sobre los registros de seguimiento, vea [Registro de seguimiento del servicio del servidor de informes](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Ejemplo de configuración  
 El siguiente ejemplo muestra los parámetros de configuración y los valores predeterminados que se encuentran en el archivo ReportingServicesService.exe.config.  
  
```  
<configSections>  
      <section name="RStrace" type="Microsoft.ReportingServices.Diagnostics.RSTraceSectionHandler,Microsoft.ReportingServices.Diagnostics" />  
</configSections>  
\<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
\</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="debugwindow, file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
<runtime>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
             <dependentAssembly>  
                    <assemblyIdentity name="Microsoft.ReportingServices.Interfaces"  
                        publicKeyToken="89845dcd8080cc91"  
                        culture="neutral" />  
                    <bindingRedirect oldVersion="8.0.242.0"  
                                     newVersion="10.0.0.0"/>  
                    <bindingRedirect oldVersion="9.0.242.0"  
                                     newVersion="10.0.0.0"/>  
             </dependentAssembly>  
      </assemblyBinding>  
      <gcServer enabled="true" />  
</runtime>  
```  
  
## <a name="configuration-settings"></a>Parámetros de configuración  
 La siguiente tabla proporciona información sobre parámetros específicos. Los parámetros se presentan en el orden en que aparecen en el archivo de configuración.  
  
|Configuración|Descripción|  
|-------------|-----------------|  
|**RStrace**|Especifica espacios de nombres utilizados para errores y traza.|  
|**DefaultTraceSwitch**|Especifica el nivel de información que se incluye en el registro de seguimiento de ReportServerService. Cada nivel incluye la información proporcionada para todos los niveles inferiores. No se recomienda deshabilitar la traza. Los valores válidos incluyen:<br /><br /> 0= Deshabilita la traza<br /><br /> 1= Excepciones y reinicios<br /><br /> 2= Excepciones, reinicios y advertencias<br /><br /> 3= Excepciones, reinicios, advertencias y mensajes de estado (predeterminado)<br /><br /> 4= Modo detallado|  
|**FileName**|Especifica la primera parte del nombre del archivo de registro. El valor especificado en **Prefix** completa el resto del nombre. El nombre predeterminado es ReportServerService_.|  
|**FileSizeLimitMb**|Especifica un límite superior para el tamaño del registro de seguimiento. El tamaño del archivo se indica en megabytes. Los valores válidos son de 0 a un número entero definido como máximo. El valor predeterminado es 32.|  
|**KeepFilesForDays**|Especifica los días tras los que se elimina un archivo de registro de seguimiento. Los valores válidos son de 0 a un número entero definido como máximo. El valor predeterminado es 14.|  
|**Prefix**|Especifica un valor generado que distingue una instancia de registro de otra. De manera predeterminada, se anexan valores de marca de tiempo a los nombres de los archivos de registro de seguimiento. Este valor se establece en " tid, time ". No modifique este parámetro.|  
|**TraceListeners**|Especifica un destino de salida para el contenido del registro de seguimiento. Se pueden especificar varios destinos separados por comas. Los valores válidos incluyen:<br /><br /> DebugWindow (predeterminado)<br /><br /> File (predeterminado)<br /><br /> StdOut|  
|**TraceFileMode**|Especifica si los registros de seguimiento incluyen datos de un período de 24 horas. Es recomendable tener un único registro de seguimiento para cada componente y día. Este valor se establece en "Unique (default)". No modifique este valor.|  
|**Components**|Especifica los componentes para los que se crean registros de seguimiento. El valor predeterminado es **all**. Otros valores válidos para este parámetro son los nombres de los componentes internos. No modifique este valor.|  
|**Tiempo de ejecución**|Especifica valores de configuración que ofrecen compatibilidad con versiones anteriores. Los valores de tiempo de ejecución se utilizan para redirigir a la nueva versión las solicitudes destinadas a versiones anteriores de Microsoft.ReportingServices.Interfaces.<br /><br /> Todos los valores de configuración de esta sección están descritos en la documentación del producto [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Para obtener más información, vea la sección sobre los valores de esquema de tiempo de ejecución en el sitio web de MSDN o en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .|  
  
## <a name="see-also"></a>Vea también  
[Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)  
[Registro de seguimiento del servicio del servidor de informes](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
