---
title: Características de SQL Server Reporting Services admitidas en sus ediciones
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 06/20/2019
ms.openlocfilehash: 3e61381c2298a197be698ed82c247023ad708789
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893283"
---
# <a name="sql-server-reporting-services-features-supported-by-its-editions"></a>Características de SQL Server Reporting Services admitidas en sus ediciones

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

En este tema se explican las características de SQL Server Reporting Services (SSRS) admitidas en las diferentes ediciones de SQL Server. La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
  
 Para obtener las notas de la versión de SQL Server más recientes, vea [Notas de la versión de SQL Server 2017](../sql-server/sql-server-2017-release-notes.md). Para ver la información más reciente sobre las novedades, consulte [Novedades de Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

 ## <a name="try-sql-server-2017"></a>Probar SQL Server 2017

> [![Descargar SQL Server 2017](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **[Descargar SQL Server 2017 desde el Centro de evaluación](https://go.microsoft.com/fwlink/?LinkID=829477)**    
>
> ![Máquina virtual de Azure pequeña ](https://docs.microsoft.com/analysis-services/analysis-services/media/azure-virtual-machine-small.png) **[Poner en marcha una máquina virtual con SQL Server 2017 ya instalado](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    

Para conocer las características admitidas en las ediciones Evaluation y Developer, vea la columna SQL Server Enterprise Edition de la tabla siguiente.

##  <a name="SSRS"></a> SQL Server Reporting Services  
  
|Nombre de característica|Enterprise|Estándar|Web|Express con Advanced Services|Desarrollador|  
|------------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Informes móviles y análisis|Sí||||Sí|  
|Edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de base de datos de catálogo admitida|Estándar o superior|Estándar o superior|Web|Express|Estándar o superior|  
|Origen de datos compatibles con la edición [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|Servidor de informes|Sí|Sí|Sí|Sí|Sí|  
|Diseñador de informes|Sí|Sí|Sí|Sí|Sí|  
|Portal web de diseñador de informes|Sí|Sí|Sí|Sí|Sí|  
|Seguridad basada en roles|Sí|Sí|Sí|Sí|Sí|  
|Exportar a Excel, PowerPoint, Word, PDF e imágenes|Sí|Sí|Sí|Sí|Sí|  
|Medidores y gráficos mejorados|Sí|Sí|Sí|Sí|Sí|  
|Anclar elementos de informe a paneles de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]|Sí|Sí|Sí|Sí|Sí|  
|Autenticación personalizada|Sí|Sí|Sí||Sí|  
|Informe como fuentes de distribución de datos|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con los modelos|Sí|Sí|Sí||Sí|  
|Crear roles personalizados para la seguridad basada en roles|Sí|Sí|||Sí|  
|Seguridad de elementos del modelo|Sí|Sí|||Sí|  
|Clic sobre aviso (click-through) infinito|Sí|Sí|||Sí|  
|Biblioteca de componentes compartidos|Sí|Sí|||Sí|  
|Suscripciones y programación de recursos compartidos de archivo y correo electrónico|Sí|Sí|||Sí|  
|Historial de informes, instantáneas de ejecución y almacenamiento en caché|Sí|Sí|||Sí|  
|Integración de SharePoint<sup>2</sup>|Sí|Sí|||Sí|  
|Compatibilidad con orígenes de datos remotos y ajenos a SQL<sup>1</sup>|Sí|Sí|||Sí|  
|Extensibilidad de orígenes de datos, entrega, representación y RDCE|Sí|Sí|||Sí|  
|Marca personalizada|Sí||||Sí|  
|Suscripción de informe basada en datos|Sí||||Sí|  
|Implementación escalada (granja de servidores web)|Sí||||Sí|  
|Alertas<sup>2</sup> (SSRS 2016) |Sí||||Sí|  
|Power View<sup>2</sup> (SSRS 2016) |Sí||||Sí| 
|Comentarios<sup>3</sup> |Sí|Sí|Sí|Sí|Sí|  

 <sup>1</sup> Para más información sobre los orígenes de datos admitidos en SQL Server Reporting Services (SSRS), consulte [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Requiere SQL Server 2016 Reporting Services en modo SharePoint. Para más información, consulte [Instalación de SQL Reporting Services en modo de SharePoint](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md). A partir de SQL Server 2017 Reporting Services, la integración con SharePoint ya no está disponible. 

<sup>3</sup> Solo en Power BI Report Server y SQL Server 2017 Reporting Services y versiones posteriores.

> [!NOTE]
> SQL Server Express with Tools y SQL Server Express no admiten SQL Server Reporting Services.
  
## <a name="edition-requirements-for-the-report-server-database"></a>Requisitos de edición de la base de datos del servidor de informes
 Al crear una base de datos del servidor de informes, no se pueden usar todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para hospedarla. En la tabla siguiente se muestra qué ediciones de la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] se pueden usar para ediciones concretas de SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Use esta edición de la instancia del motor de base de datos para hospedar la base de datos|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edición Enterprise o Standard (local o remota)|  
|Estándar|Edición Enterprise o Standard (local o remota)|  
|Web|Web Edition (solo local)|  
|Express con Advanced Services|Express con Advanced Services (solo local).|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Clientes de inteligencia empresarial  
Las siguientes aplicaciones cliente de software están disponibles en el Centro de descarga de Microsoft. Estas le ayudan a crear documentos de inteligencia empresarial que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si hospeda estos documentos en un entorno de servidor, use una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la herramienta|Enterprise|Estándar|Web|Express con Advanced Services|Desarrollador|  
|---------------|----------------|--------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], **.rdl** y **.rds**|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)], **.rsmobile**|Sí||||Sí|  
|Aplicaciones de Power BI para dispositivos móviles (iOS, Windows 10 y Android), **.rsmobile**|Sí||||Sí|  
  
> [!NOTE]  
> * En la tabla anterior se identifican las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que son necesarias para permitir estas herramientas de cliente. Sin embargo, con estas herramientas se puede acceder a los datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] es el único punto para crear informes móviles. Conéctese a un servidor de SSRS para acceder a orígenes de datos y crear informes. Luego, publíquelos en el servidor de SSRS para que otros usuarios de la organización puedan acceder a ellos, ya sea en el servidor o en dispositivos móviles. También puede usar [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] de modo independiente con orígenes de datos locales.  
> * Tanto si usa [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] de forma local, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] en la nube, o ambos, como solución de entrega de informes, solo necesita una aplicación móvil para acceder a los paneles e informes móviles en dispositivos móviles. Las aplicaciones de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] se pueden descargar en las tiendas de aplicaciones de Windows, iOS y Android.  

## <a name="next-steps"></a>Pasos siguientes

* Lea acerca de las [características admitidas en las ediciones de SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md). 

* [Planear una instalación de SQL Server](../sql-server/install/planning-a-sql-server-installation.md)

* ¿Tiene alguna pregunta más? Pregunte en el [foro de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
