---
title: Seguridad del Agente de lectura de cola | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92b80f727ce87606b0c1c58954b0743734880422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021259"
---
# <a name="queue-reader-agent-security"></a>Seguridad del Agente de lectura de cola
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo **Seguridad del Agente de lectura de cola** le permitirá especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutará el Agente de lectura de cola y establecerá las conexiones locales al distribuidor. El agente se conecta al publicador a través de la cuenta especificada en el cuadro de diálogo **Propiedades del publicador** (disponible en el cuadro de diálogo **Propiedades del distribuidor** ); el agente se conectará al suscriptor a través del mismo contexto que el Agente de distribución para la suscripción. Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 La cuenta deberá ser válida y deberá especificarse la contraseña correcta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Cuenta de proceso**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de lectura de cola en el distribuidor. La cuenta de Windows que especifique debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** de la base de datos de distribución.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
## <a name="see-also"></a>Consulte también  
 [Identidad y control de acceso (replicación)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Procedimientos recomendados de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
