---
title: Establecer el nivel de compatibilidad para publicaciones de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7aecff691139b1041a928c42c3df2987c992cd91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68199318"
---
# <a name="set-the-compatibility-level-for-merge-publications"></a>Establecer el nivel de compatibilidad para publicaciones de mezcla
  En este tema se describe cómo establecer el nivel de compatibilidad para las publicaciones de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La replicación de mezcla emplea el nivel de compatibilidad de la publicación para determinar qué características pueden usar las publicaciones de una base de datos determinada.  
  
 **En este tema**  
  
-   **Para establecer el nivel de compatibilidad para publicaciones de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Establezca el nivel de compatibilidad en la página **Tipos de suscriptor** del Asistente para nueva publicación. Para obtener más información acerca de cómo obtener acceso a este asistente, vea [Create a Publication](create-a-publication.md). Después de crear una publicación de instantáneas, el nivel de compatibilidad se puede aumentar pero no se puede reducir. Aumente el nivel de compatibilidad en la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md). Si aumenta el nivel de compatibilidad, las suscripciones existentes en los servidores que se ejecuten con versiones anteriores al nivel de compatibilidad no se podrán sincronizar.  
  
> [!NOTE]  
>  Debido a que el nivel de compatibilidad tiene implicaciones en otras propiedades de la publicación y en cuanto a qué propiedades del artículo son válidas, no cambie el nivel de compatibilidad ni otras propiedades en el mismo uso del cuadro de diálogo. La instantánea de la publicación se volverá a generar después de cambiar la propiedad.  
  
#### <a name="to-set-the-publication-compatibility-level"></a>Para establecer el nivel de compatibilidad de la publicación  
  
-   En la página **Tipos de suscriptor** del Asistente para nueva publicación, seleccione los tipos de suscriptores que admitirá la publicación.  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>Para aumentar el nivel de compatibilidad de la publicación  
  
-   En la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , seleccione el valor deseado para **Nivel de compatibilidad**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 El nivel de compatibilidad para una publicación de combinación se puede establecer mediante programación cuando una publicación se crea o bien, se puede modificar mediante programación en un momento posterior. Puede usar procedimientos almacenados de replicación para establecer o cambiar esta propiedad de publicación.  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>Para establecer el nivel de compatibilidad de la publicación para una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), especificando un valor para **@publication_compatibility_level** para que la publicación sea compatible con versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Crear una suscripción](create-a-publication.md).  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>Para cambiar el nivel de compatibilidad de la publicación de una publicación de combinación  
  
1.  Ejecute [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando **publication_compatibility_level** para **@property** y el nivel de compatibilidad de la publicación adecuado para **@value** .  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>Para determinar el nivel de compatibilidad de la publicación de una publicación de combinación  
  
1.  Ejecute [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) especificando la publicación deseada.  
  
2.  Busque el nivel de compatibilidad de la publicación en la columna **de backward_comp_level** en el conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo crea una publicación de combinación y establece el nivel de compatibilidad de la publicación.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 Este ejemplo cambia el nivel de compatibilidad de la publicación para la publicación de combinación.  
  
> [!NOTE]  
>  Cambiar el nivel de compatibilidad de la publicación podría no permitirse si la publicación usa alguna característica que requiera un nivel de compatibilidad determinado. Para obtener más información, vea [Compatibilidad con versiones anteriores de replicación](../replication-backward-compatibility.md).  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 Este ejemplo devuelve el nivel de compatibilidad de la publicación actual para la publicación de combinación.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](create-a-publication.md)  
  
  
