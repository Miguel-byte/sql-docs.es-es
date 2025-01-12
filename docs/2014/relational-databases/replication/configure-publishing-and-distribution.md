---
title: Configuración de la publicación y la distribución | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- publishing [SQL Server replication], configuring
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 557c3eb76dbaba037c289b93bc80bb1314e4d106
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721707"
---
# <a name="configure-publishing-and-distribution"></a>Configurar la publicación y la distribución
  En este tema se describe cómo configurar la publicación y distribución en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Replication Management Objects (RMO).  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener más información, consulte [implementación segura de replicación](security/view-and-modify-replication-security-settings.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Configure la distribución con el Asistente para nueva publicación o el Asistente para configurar la distribución. Después de configurar el distribuidor, vea y modifique las propiedades en el cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>** . Utilice el Asistente para configurar la distribución si desea configurar un distribuidor para que los miembros de los roles fijos de base de datos **db_owner** puedan crear publicaciones o si desea configurar un distribuidor remoto que no sea un publicador.  
  
#### <a name="to-configure-distribution"></a>Para configurar la distribución  
  
1.  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte con el servidor que será el distribuidor (en muchos casos, el publicador y el distribuidor están en el mismo servidor) y, a continuación, expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** y, a continuación, en **Configurar distribución**.  
  
3.  Siga las indicaciones del Asistente para configurar la distribución:  
  
    -   Seleccione un distribuidor. Para usar un distribuidor local, seleccione **'\<NombreServidor', que actuará como su propio distribuidor. SQL Server creará una base de datos y un registro de distribución**. Para utilizar un distribuidor remoto, seleccione **Utilizar el siguiente servidor como distribuidor**y, a continuación, seleccione un servidor. El servidor ya debe estar configurado como distribuidor y el publicador debe estar habilitado para usar el distribuidor. Para más información, vea [Habilitar un publicador remoto en un distribuidor &#40;SQL Server Management Studio&#41;](enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md).  
  
         Si selecciona un distribuidor remoto, debe escribir una contraseña en la página **Contraseña administrativa** para las conexiones realizadas desde el publicador al distribuidor. Esta contraseña debe coincidir con la especificada cuando se habilitó el publicador en el distribuidor remoto.  
  
    -   Especifique una carpeta de instantáneas raíz (para un distribuidor local). La carpeta de instantáneas es simplemente un directorio designado como recurso compartido; los agentes que leen y escriben en esta carpeta deben tener permisos de acceso suficientes a ella. Cada publicador que utiliza este distribuidor crea una carpeta bajo la carpeta raíz, y cada publicación crea carpetas bajo la carpeta de publicador donde almacena los archivos de instantáneas. Para más información sobre cómo proteger la carpeta adecuadamente, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
    -   Especifique la base de datos de distribución (para un distribuidor local). La base de datos de distribución almacena metadatos y datos del historial de todos los tipos de replicación y transacciones para la replicación transaccional.  
  
    -   Opcionalmente, habilite otros publicadores para utilizar el distribuidor. Si se habilitan otros publicadores para utilizar el distribuidor, debe escribir una contraseña en la página **Contraseña del distribuidor** para las conexiones realizadas desde esos publicadores al distribuidor.  
  
    -   Opcionalmente, genere un script de opciones de configuración. Para más información, consulte [Scripting Replication](scripting-replication.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 La publicación y distribución de replicaciones se puede configurar mediante programación usando procedimientos almacenados de replicación.  
  
#### <a name="to-configure-publishing-using-a-local-distributor"></a>Para configurar la publicación mediante un distribuidor local  
  
1.  Ejecute [sp_get_distributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql) para determinar si el servidor ya está configurado como un distribuidor.  
  
    -   Si el valor de **installed** en el conjunto de resultados es **0**, ejecute [sp_adddistributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql) en el distribuidor en la base de datos maestra.  
  
    -   Si el valor de **distribution db installed** en el conjunto de resultados es **0**, ejecute [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql) en el distribuidor en la base de datos maestra. Especifique el nombre de la base de datos de distribución para **@database** . Opcionalmente, puede especificar el período de retención de transacción máximo para **@max_distretention** y el período de retención del historial para **@history_retention** . Si se está creando una nueva base de datos, especifique los parámetros de propiedad de la base de datos que desee.  
  
2.  En el distribuidor, que también es el publicador, ejecute [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) y especifique el recurso compartido UNC que se usará como carpeta de instantáneas predeterminada para **@working_directory** .  
  
3.  En el publicador, ejecute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql). Especifique la base de datos que se publica para **@dbname** , el tipo de replicación para **@optname** y un valor de `true` para **@value** .  
  
#### <a name="to-configure-publishing-using-a-remote-distributor"></a>Para configurar la publicación mediante un distribuidor remoto  
  
1.  Ejecute [sp_get_distributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql) para determinar si el servidor ya está configurado como un distribuidor.  
  
    -   Si el valor de **installed** en el conjunto de resultados es **0**, ejecute [sp_adddistributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql) en el distribuidor en la base de datos maestra. Especifique una contraseña segura para **@password** . Esta contraseña para la cuenta **distributor_admin** la utilizará el publicador para conectarse al distribuidor.  
  
    -   Si el valor de **distribution db installed** en el conjunto de resultados es **0**, ejecute [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql) en el distribuidor en la base de datos maestra. Especifique el nombre de la base de datos de distribución para **@database** . Opcionalmente, puede especificar el período de retención de transacción máximo para **@max_distretention** y el período de retención del historial para **@history_retention** . Si se está creando una nueva base de datos, especifique los parámetros de propiedad de la base de datos que desee.  
  
2.  En el distribuidor, ejecute [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) y especifique el recurso compartido UNC que se usará como carpeta de instantáneas predeterminada para **@working_directory** . Si el distribuidor va a utilizar autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse al publicador, también debe especificar el valor **0** para **@security_mode** y la información de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@login** y **@password** .  
  
3.  En la base de datos maestra del publicador, ejecute [sp_adddistributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql). Especifique la contraseña segura utilizada en el paso 1 para **@password** . El publicador utilizará esta contraseña cuando se conecte al distribuidor.  
  
4.  En el publicador, ejecute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql). Especifique la base de datos que se está publicando para **@dbname** , el tipo de replicación para **@optname** y el valor true para **@value** .  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 El ejemplo siguiente muestra cómo configurar mediante programación la publicación y la distribución. En este ejemplo, se proporciona el nombre del servidor que se está configurando como un publicador y un distribuidor local mediante las variables de scripting. La publicación y distribución de replicaciones se puede configurar mediante programación usando procedimientos almacenados de replicación.  
  
 [!code-sql[HowTo#AddDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/adddistpub.sql#adddistpub)]  
  
##  <a name="RMOProcedure"></a> Uso de Replication Management Objects (RMO)  
  
#### <a name="to-configure-publishing-and-distribution-on-a-single-server"></a>Para configurar la publicación y distribución en un único servidor  
  
1.  Cree una conexión al servidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Pase el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionDatabase> .  
  
4.  Establezca la propiedad <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> en el nombre de la base de datos y la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
5.  Instale el distribuidor llamando al método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> . Transfiera el objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> del paso 3.  
  
6.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionPublisher> .  
  
7.  Establezca las siguientes propiedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - nombre del publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - el nombre de la base de datos creada en el paso 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - el recurso compartido utilizado para tener acceso a los archivos de instantáneas.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> : el modo de seguridad empleado cuando se conecta con el publicador. Se recomienda<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> .  
  
8.  Llame al método <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A>.  
  
#### <a name="to-configure-publishing-and-distribution-using-a-remote-distributor"></a>Para configurar la publicación y distribución mediante un distribuidor remoto  
  
1.  Cree una conexión al servidor del distribuidor remoto mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Pase el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionDatabase> .  
  
4.  Establezca la propiedad <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> en el nombre de la base de datos y la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
5.  Instale el distribuidor llamando al método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> . Especifique una contraseña segura (la que utiliza el publicador al conectarse al distribuidor remoto) y el objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> del paso 3. Para más información, vea [Proteger el distribuidor](security/secure-the-distributor.md).  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](https://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
6.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionPublisher> .  
  
7.  Establezca las siguientes propiedades de <xref:Microsoft.SqlServer.Replication.DistributionPublisher>:  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - nombre del servidor publicador local.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - el nombre de la base de datos creada en el paso 5.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - el recurso compartido utilizado para tener acceso a los archivos de instantáneas.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> : el modo de seguridad empleado cuando se conecta con el publicador. Se recomienda<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> .  
  
8.  Llame al método <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> .  
  
9. Cree una conexión al servidor publicador local mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
10. Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Transfiera el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 9.  
  
11. Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> . Pase el nombre del distribuidor remoto y la contraseña para el distribuidor remoto especificado en el paso 5.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](https://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por Windows .NET Framework.  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Puede configurar la publicación y distribución de replicación mediante programación utilizando Replication Management Objects (RMO).  
  
 [!code-csharp[HowTo#rmo_AddDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar distribución](configure-distribution.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Configurar la replicación para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) 
  
  
