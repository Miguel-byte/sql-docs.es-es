---
title: Inicializar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e88387df824cea6d617633fffcb27eeee8db9129
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770606"
---
# <a name="initialize-a-subscription"></a>Inicializar una suscripción
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Los suscriptores de una topología de replicación se deben inicializar con el fin de que tengan una copia del esquema de cada artículo de la publicación a la que están suscritos y de los objetos de replicación que se requieran, como procedimientos almacenados, desencadenadores y tablas de metadatos. Además, el suscriptor normalmente recibe un conjunto de datos inicial. El método de inicialización predeterminado usa una instantánea completa que incluye el esquema, objetos de replicación y datos, aunque las publicaciones también se pueden inicializar sin una instantánea completa.  
  
 Para obtener más información, consulte [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) y [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
