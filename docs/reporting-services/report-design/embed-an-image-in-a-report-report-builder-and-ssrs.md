---
title: Insertar una imagen en un informe (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8da5d6851b9cf042d1b04e72b9c58257f9f9f509
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579327"
---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>Incrustar una imagen en un informe (Generador de informes y SSRS)
  Un informe puede incluir una imagen incrustada. El empleo de imágenes incrustadas asegura su disponibilidad permanente en un informe, pero también afecta al tamaño de la definición de informe, el archivo que lo define. Las imágenes incrustadas en un informe se enumeran en el panel Datos de informe.  
  
 Podría ser conveniente incrustar una imagen en la definición de informe antes de agregarla a la superficie de diseño. Para más información, vea [Agregar una imagen de fondo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>Incrustar una imagen en un informe  
  
1.  En la vista de diseño del informe, en la pestaña **Insertar** , haga clic en **Imagen**.  
  
2.  En la superficie de diseño, haga clic en un cuadro y, a continuación, arrástrelo hasta obtener el tamaño de la imagen que desee.  
  
3.  En la página **General** del cuadro de diálogo **Propiedades de la imagen** , escriba un nombre en el cuadro de texto **Nombre** o acepte el nombre predeterminado.  
  
4.  (Opcional) En el cuadro de texto de **Información sobre herramientas** , escriba el texto que quiere que aparezca cuando el usuario mantenga el mouse sobre la imagen en el informe representado.  
  
5.  En **Seleccionar el origen de la imagen**, seleccione **Incrustado**.  
  
6.  Hacer clic en el botón **Importar** al lado del cuadro de texto **Usar esta imagen**  
  
7.  En **Archivos de tipo**, seleccione el tipo de archivo de imagen, navegue al archivo y, a continuación, haga clic en **Abrir**.  
  
8.  En el cuadro de diálogo **Propiedades de la imagen** , haga clic en **Aceptar**.  
  
     La imagen se muestra en el cuadro que dibujó en la superficie del diseño, y el archivo se muestra bajo la carpeta Imágenes en el panel Datos de informe.  
  
    > [!NOTE]  
    >  El tipo MIME (por ejemplo, bmp) se deriva automáticamente cuando se importa la imagen. Para cambiar el tipo MIME, vea el procedimiento siguiente.  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>(Opcional) Cambiar el tipo MIME de una imagen importada  
  
1.  Abra el informe en la vista Diseño.  
  
2.  Seleccione la imagen en la superficie de diseño. El panel **Propiedades** muestra las propiedades de la imagen.  
  
    > [!NOTE]  
    >  Si el panel de propiedades no está visible, en la pestaña **Vista** , haga clic en **Propiedades**.  
  
3.  Haga clic en el cuadro de texto situado junto a la propiedad **MIMEType** y seleccione un nuevo tipo MIME en la lista desplegable.  
  
## <a name="see-also"></a>Consulte también  
 [Imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Agregar una imagen enlazada a datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de Propiedades de la imagen, General &#40;Generador de informes y SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
