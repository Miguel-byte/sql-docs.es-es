---
title: Adición de una base de datos cifrada a un grupo de disponibilidad
description: Pasos para agregar una base de datos cifrada (o descifrada recientemente) a un grupo de disponibilidad Always On.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b5e86fe6a4f37e4ac21afb3a9aa72d80d48f3544
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000196"
---
# <a name="add-an-encrypted-database-to-an-always-on-availability-group"></a>Adición de una base de datos cifrada a un grupo de disponibilidad Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema contiene información sobre el uso de bases de datos actualmente cifradas o recientemente descifradas con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
##  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si una base de datos está cifrada o incluso contiene una clave de cifrado de base de datos (DEK), no puede usar el [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] ni el [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] para agregar la base de datos a un grupo de disponibilidad. Aunque se haya descifrado una base de datos cifrada, sus copias de seguridad de registros pueden contener datos cifrados. En este caso, la sincronización de datos completa inicial podría producir errores en la base de datos. Esto se debe a que la operación de restaurar registro puede requerir el certificado utilizado por las claves de cifrado de base de datos (DEK) y ese certificado podría no estar disponible.  
  
     Para que una base de datos descifrada se pueda agregar a un grupo de disponibilidad mediante el asistente:  
  
    1.  Cree una copia de seguridad de registros de la base de datos principal.  
  
    2.  Cree una copia de seguridad completa de la base de datos principal.  
  
    3.  Restaure la copia de seguridad de base de datos en la instancia del servidor que hospeda la réplica secundaria.  
  
    4.  Cree una nueva copia de seguridad de registros a partir de la base de datos principal.  
  
    5.  Restaure esta copia de seguridad de registros en la base de datos secundaria.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Cifrado de datos transparente &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
