---
title: sp_change_agent_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd737be5a1e71e46750f6c80fd68ad254cb6436f
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768943"
---
# <a name="spchangeagentparameter-transact-sql"></a>sp_change_agent_parameter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cambia un parámetro de un perfil de agente de replicación almacenado en la tabla del sistema [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) . Este procedimiento almacenado se ejecuta en el distribuidor en el que se está ejecutando el agente, en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id,`Es el identificador del perfil. *profile_id* es de **tipo int**y no tiene ningún valor predeterminado.  
  
`[ @parameter_name = ] 'parameter_name'`Es el nombre del parámetro. *parameter_name* es de **tipo sysname**y no tiene ningún valor predeterminado. Para los perfiles del sistema, los parámetros que se pueden cambiar dependen del tipo de agente. Para averiguar qué tipo de agente representa este *profile_id* , busque la columna *profile_id* en la tabla **Msagent_profiles** y anote el valor de *agent_type* .  
  
> [!NOTE]  
>  Si un parámetro es compatible con un *agent_type*determinado, pero no se ha definido en el perfil del agente, se devuelve un error. Para agregar un parámetro a un perfil de agente, debe ejecutar [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
 En el caso de una agente de instantáneas (*agent_type*=**1**), si se define en el perfil, se pueden cambiar las siguientes propiedades:  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **Genere**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **QueryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 En el caso de una agente de registro del log (*agent_type*=**2**), si se define en el perfil, se pueden cambiar las siguientes propiedades:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **Genere**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 En el caso de una agente de distribución (*agent_type*=**3**), si se define en el perfil, se pueden cambiar las siguientes propiedades:  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **Genere**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 En el caso de una agente de mezcla (*agent_type*=**4**), si se define en el perfil, se pueden cambiar las siguientes propiedades:  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **ChangesPerHistory**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **DownloadReadChangesPerBatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **InteractiveResolution**  
  
-   **InterruptOnMessagePattern**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **Genere**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **QueryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **Validar**  
  
-   **ValidateInterval**  
  
 En el caso de una agente de lectura de cola (*agent_type*=**9**), si se define en el perfil, se pueden cambiar las siguientes propiedades:  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **Genere**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 Para ver qué parámetros se han definido para un perfil determinado, ejecute **sp_help_agent_profile** y tenga en cuenta el *profile_name* asociado con *profile_id*. Con el *profile_id*adecuado, ejecute **sp_help_agent_parameters** con ese *profile_id* para ver los parámetros asociados al perfil. Los parámetros se pueden agregar a un perfil ejecutando [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md).  
  
`[ @parameter_value = ] 'parameter_value'`Es el nuevo valor del parámetro. *parameter_value* es de tipo **nvarchar (255)** y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_agent_parameter** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_change_agent_parameter**.  
  
## <a name="see-also"></a>Vea también  
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
