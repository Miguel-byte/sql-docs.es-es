---
title: Seguridad del agente &lt;NombreAgente&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d77f8d6acb449bc9aa2298dbcba9782fd7bc07e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62722127"
---
# <a name="ltagentnamegt-agent-security"></a>Seguridad del agente &lt;NombreAgente&gt;
  La página **Seguridad del Agente \<NombreAgente>** permite especificar las cuentas con las que el Agente de distribución (para replicación transaccional y de instantáneas) o el Agente de mezcla (para replicación de mezcla) ejecuta y realiza conexiones con los equipos de una topología de replicación. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, consulte [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md) y [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opciones  
 Haga clic en el botón de propiedades ( **...** ) de la fila de cada suscriptor para obtener acceso al cuadro de diálogo **Seguridad del Agente de distribución** o **Seguridad del Agente de mezcla** . Haga clic en **Ayuda** en el cuadro de diálogo que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada suscriptor.  
  
 **Conexión al distribuidor**  
 Se muestra para la replicación transaccional y de instantáneas. Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de inserción, la conexión local es la conexión al distribuidor, por lo que en este campo siempre se mostrará: **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** para las suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el campo se muestra uno de los siguientes: **Usar inicio de sesión "\<Inicio de sesión>"** , **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión con el publicador y distribuidor**  
 Se muestra para la replicación de mezcla. Contexto en el que se realizan las conexiones al publicador y al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de inserción, la conexión local es la conexión al publicador y al distribuidor, por lo que en este campo siempre se mostrará: **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** para las suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el campo se muestra uno de los siguientes: **Usar inicio de sesión "\<Inicio de sesión>"** , **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de extracción, la conexión local es la conexión al suscriptor, por lo que en este campo siempre se mostrará: **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** para las suscripciones de inserción.  
  
-   Para las suscripciones de inserción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el campo se muestra uno de los siguientes: **Usar inicio de sesión "\<Inicio de sesión>"** , **Suplantar "\<Dominio>\\<Inicio de sesión\>"** o **Suplantar "\<Equipo>\\<Inicio de sesión\>"** . [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## <a name="see-also"></a>Vea también  
 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md)   
 [Administrar inicios de sesión y contraseñas en la replicación](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md)   
 [Seguridad de replicación de SQL Server](security/view-and-modify-replication-security-settings.md)  
  
  
