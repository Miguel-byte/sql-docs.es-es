---
title: Generar scripts (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: mathoma
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 800153a20651b649d644fecfeacf11d48958fab8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265453"
---
# <a name="generate-scripts-sql-server-management-studio"></a>Generar scripts (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona dos mecanismos para generar scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Puede crear scripts para varios objetos con el **Asistente Generar y publicar scripts**. También puede generar un script para objetos individuales o varios objetos con el menú **Incluir como** del **Explorador de objetos**.  

Para obtener un tutorial detallado sobre cómo crear script de varios objetos mediante SQL Server Management Studio (SSMS), consulte [Tutorial: Creación de scripts en SSMS](https://docs.microsoft.com/sql/ssms/tutorials/scripting-ssms).

  
## <a name="before-you-begin"></a>Antes de empezar  
 Elija el mecanismo que mejor cumpla sus requisitos.  
  
###  <a name="GenPubScriptWiz"></a> Asistente generar y publicar scripts  
 Use el **Asistente Generar y publicar scripts** para crear un script [!INCLUDE[tsql](../../includes/tsql-md.md)] para muchos objetos. El asistente genera un script de todos los objetos de una base de datos o un subconjunto de los objetos que seleccione. El asistente dispone de muchas opciones para los scripts, como la posibilidad de incluir permisos, la intercalación, las restricciones, etc. Para obtener instrucciones acerca de cómo usar el asistente, vea [Generate and Publish Scripts Wizard](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Menú Incluir como del Explorador de objetos  
 Puede usar el menú **Incluir como del Explorador de objetos** para generar un script de un solo objeto, de varios objetos o de varias instrucciones para un único objeto. Puede elegir uno de varios tipos de scripts; por ejemplo crear, modificar o quitar el objeto. Puede guardar un script en una ventana del Editor de consultas, en un archivo o en el Portapapeles. El script se crea en formato Unicode.  
  
##  <a name="ScriptSingleObject"></a> Para generar un script de un solo objeto  
 **Para generar un script de un solo objeto**  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, y a continuación expanda la base de datos que contiene el objeto que se debe incluir en un script.  
  
3.  Expanda la categoría del objeto. Por ejemplo, expanda el nodo **Vistas** o **Tablas** .  
  
4.  Haga clic con el botón derecho en el objeto y vaya a **Incluir \<tipo de objeto> como**; por ejemplo, vaya a **Incluir tabla como**.  
  
5.  Seleccione el tipo de script, como **Create to** o **Alter to**.  
  
6.  Seleccione la ubicación para guardar el script, como **Nueva ventana del Editor de consultas** o **Portapapeles**.  

    ![Tabla de scripting](media/generate-scripts-sql-server-management-studio/scripttable.png)
  
  
 Puede usar el panel **Detalles del Explorador de objetos** para generar un script para varios objetos de la misma categoría.  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, y a continuación expanda la base de datos que contiene los objetos que se deben incluir en un script.  
  
3.  Expanda el nodo de categoría de los tipos de objeto que desea incluir en el script, como el nodo **Tablas** .  
  
4.  Abra el panel **Detalles del Explorador de objetos** seleccionando **F7**o abriendo el menú **Ver** y seleccionando **Detalles del Explorador de objetos**.  
  
5.  Haga clic con el botón primario en uno de los objetos que desea incluir en el script.  
  
6.  Presione Crtl y haga clic con el botón primario en el segundo objeto que desea incluir en el script.  
  
7.  Haga clic con el botón derecho en uno de los objetos seleccionados y elija **Incluir \<tipo de objeto> como**.  

    ![Explorador de objetos](media/generate-scripts-sql-server-management-studio/objectexplorerdetails.png)
  
  
