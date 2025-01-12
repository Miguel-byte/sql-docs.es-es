---
title: Propiedades de las réplicas de disponibilidad (página General) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07652cec7b3b7a17c4b994eb68afd939e15244a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791909"
---
# <a name="availability-replica-properties-general-page"></a>Propiedades de las réplicas de disponibilidad (página General)
  Use este cuadro de diálogo para ver las propiedades de una réplica de disponibilidad.  
  
## <a name="task-list"></a>Lista de tareas  
 **Para ver las propiedades de una réplica de disponibilidad**  
  
-   [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre del grupo de disponibilidad**  
 Nombre del grupo de disponibilidad. Es un nombre definido por el usuario que debe ser único dentro del clúster de conmutación por error de Windows Server (WSFC).  
  
 **Instancia del servidor**  
 Nombre de servidor de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda esta réplica y, para una instancia no predeterminada, su nombre de instancia.  
  
 **Rol**  
 **Principal**  
 Actualmente la réplica principal.  
  
 **Secundario**  
 Actualmente una réplica secundaria.  
  
 **Resolver**  
 Actualmente el rol de la réplica están en proceso de resolverse al rol principal o al rol secundario.  
  
 **Modo de disponibilidad**  
 Modo de disponibilidad de la réplica, que puede ser alguno de los siguientes:  
  
 **Confirmación asincrónica**  
 La réplica principal puede confirmar transacciones sin esperar a que la réplica secundaria escriba el registro en disco.  
  
 **Confirmación sincrónica**  
 La réplica principal espera para confirmar una determinada transacción hasta que la réplica secundaria escribe la transacción en el disco.  
  
 Para obtener más información, consulte [modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md).  
  
 **Failover mode**  
 Modo de conmutación por error de la réplica, que puede ser uno de los siguientes:  
  
 **Automático**  
 Conmutación por error automática. La réplica es un destino de las conmutaciones por error automáticas. Esto solo se admite si el modo de disponibilidad se establece en confirmación sincrónica.  
  
 **Manual**  
 Conmutación por error manual. La réplica solo puede ser objeto de conmutación por error manual por parte del administrador de base de datos.  
  
 **Conexiones el en rol principal**  
 El tipo de conexiones de cliente admitidas cuando la réplica posee el rol principal.  
  
 **Permitir todas las conexiones**  
 Se permiten todas las conexiones con las bases de datos de la réplica principal. Esta es la configuración predeterminada.  
  
 **Permitir conexiones de lectura o escritura**  
 No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** . Cuando la propiedad Application Intent está establecida en **ReadWrite** o la propiedad Application Intent Connection no tiene ningún valor, se permite la conexión.  
  
 **Secundario legible**  
 Si una réplica de disponibilidad que está realizando el rol secundario (es decir, una réplica secundaria) puede aceptar conexiones de clientes; puede tener uno de los valores siguientes:  
  
 **No**  
 No se permiten conexiones directas a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
 **Solo intento de lectura**  
 Únicamente se permiten conexiones directas de solo lectura a las bases de datos secundarias de esta réplica. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 **Sí**  
 Se permiten todas las conexiones a las bases de datos secundarias de esta réplica, pero solo para acceso de lectura. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
 Para más información, consulte [Secundarias activas: Réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **Tiempo de espera de sesión (segundos)**  
 Período de tiempo de espera, en segundos. El período de tiempo de espera es el tiempo máximo que la réplica espera hasta recibir un mensaje de otra réplica antes de considerar que se ha producido un error en la conexión entre la réplica principal y la secundaria. El tiempo de espera de la sesión detecta si las réplicas secundarias están conectadas a la réplica principal. Al detectar un error en la conexión con una réplica secundaria, la réplica principal considera que la réplica secundaria no se ha sincronizado (NOT_SYNCHRONIZED). Al detectar un error en la conexión con la réplica principal, la réplica secundaria intenta volver a conectarse.  
  
> [!NOTE]  
>  Cuando se agota el tiempo de espera de la sesión, no se realiza una conmutación por error automática.  
  
 **Dirección URL del extremo**  
 Representación en forma de cadena de la base de datos definida por el usuario que crea un reflejo del extremo usado por las conexiones entre las réplicas principal y secundaria para la sincronización de datos. Para obtener más información sobre la sintaxis de las direcciones URL del punto de conexión, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
