---
title: Generar automáticamente valores para el atributo Code (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d837d188dc28e0c06d3e66162d1ab12755ac809d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047491"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Generar automáticamente valores para el atributo Code (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], genere automáticamente valores para el atributo Code de una entidad si quiere que se asigne de forma automática un entero al valor Code cada vez que se cree un miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   La entidad debe existir. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para generar automáticamente valores Code  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Administrar modelo** , seleccione la fila correspondiente al modelo que contiene la entidad que desea editar y luego haga clic en **Entidades**.  
  
3.  En la página **Administrar entidad** , seleccione la fila correspondiente a la entidad para la que quiere generar códigos y luego haga clic en **Editar**.  
  
4.  Active la casilla **Crear automáticamente valores Code** .  
  
5.  En el cuadro **Empezar con** , escriba un número para ir incrementándolo. Si ya existen miembros, el valor Code se establece según el mayor valor existente. Por ejemplo, si el mayor valor Code existente es 299, el valor Code del miembro siguiente se establecerá en 300.  
  
6.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Creación automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Generar automáticamente valores de atributo que no sean Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
