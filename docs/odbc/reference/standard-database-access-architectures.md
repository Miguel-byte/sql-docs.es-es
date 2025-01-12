---
title: Arquitecturas de acceso de base de datos estándar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b2113167bb3440c0d772a99b4b8098104d7ed11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129247"
---
# <a name="standard-database-access-architectures"></a>Arquitecturas de acceso a base de datos estándar
Observar los componentes de acceso de la base de datos que se describe en la sección anterior, pero resulta que dos de ellos - programación e interfaces de protocolos de transmisión de datos: son buenos candidatos para la estandarización. Los otros dos componentes: mecanismo IPC y protocolos de red: no sólo residen en un nivel demasiado bajo, pero son ambos sumamente dependiente de la red y el sistema operativo. También hay un tercer enfoque - puertas de enlace - que ofrece posibilidades de normalización.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Interfaz de programación estándar](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de flujo de datos estándar](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Puerta de enlace estándar](../../odbc/reference/standard-gateway.md)
