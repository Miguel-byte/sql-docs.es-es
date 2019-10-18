---
title: El registro de transacciones (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fb0aef082375ebc3c278e982232b7a69fe41d187
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083937"
---
# <a name="the-transaction-log-sql-server"></a>El registro de transacciones (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen un registro de transacciones, las cuales registran todas las transacciones y modificaciones que cada transacción realiza en la base de datos.
  
El registro de transacciones es un componente esencial de la base de datos. Si hay un error del sistema, ese registro será necesario para devolver la base de datos a un estado coherente. 

Para obtener información sobre la arquitectura del registro de transacciones y los elementos internos, vea la [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

> [!WARNING] 
> No elimine ni mueva este registro nunca, a menos que tenga pleno conocimiento de las consecuencias de hacerlo. 

> [!TIP]
> Los puntos de comprobación crean puntos buenos conocidos a partir de los cuales se empiezan a aplicar los registros de transacciones durante la recuperación de base de datos. Para obtener más información, consulte [Puntos de comprobación de base de datos (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="operations-supported-by-the-transaction-log"></a>Operaciones compatibles con el registro de transacciones  
 El registro de transacciones permite las siguientes operaciones:  
  
-   Recuperación de transacciones individuales.  
-   Recuperación de todas las transacciones incompletas cuando se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
-   Puesta al día de una base de datos, un archivo, un grupo de archivos o una página restaurados hasta el momento exacto del error.  
-   Permitir replicación transaccional.  
-   Compatibilidad con soluciones de alta disponibilidad y recuperación ante desastres: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], creación de reflejo de la base de datos y trasvase de registros.

### <a name="individual-transaction-recovery"></a>Recuperación de transacciones individuales
Si una aplicación emite una instrucción `ROLLBACK` o si el motor de base de datos detecta un error, como la pérdida de comunicación con un cliente, se usan los registros para revertir todas las modificaciones efectuadas por una transacción incompleta. 

### <a name="recovery-of-all-incomplete-transactions-when-includessnoversionincludesssnoversion-mdmd-is-started"></a>Recuperación de todas las transacciones incompletas cuando se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
Si un servidor produce errores, las bases de datos pueden quedar en un estado en que algunas modificaciones no han llegado a escribirse desde la caché del búfer a los archivos de datos; estos pueden contener modificaciones como resultado de transacciones incompletas. Cuando se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se ejecuta la recuperación de todas las bases de datos. Todas las modificaciones del registro que no se hayan podido escribir en los archivos de datos se ponen al día. Las transacciones incompletas que se encuentren en el registro de transacciones se revierten para asegurar la integridad de la base de datos. 

### <a name="rolling-a-restored-database-file-filegroup-or-page-forward-to-the-point-of-failure"></a>Puesta al día de una base de datos, un archivo, un grupo de archivos o una página restaurados hasta el momento exacto del error
Después de una pérdida de hardware o un error de disco que afecten a los archivos de base de datos, ésta se puede restaurar al punto del error. En primer lugar, restaure la última copia de seguridad completa de base de datos y la última copia de seguridad diferencial de base de datos y, después, restaure la secuencia de copias de seguridad del registro de transacciones al punto del error. 

Según restaura cada copia de seguridad del registro, el motor de base de datos vuelve a aplicar todas las modificaciones incluidas en el registro para poner al día todas las transacciones. Cuando se restaura la última copia de seguridad, el motor de base de datos usa la información del registro para revertir todas las transacciones no completadas hasta ese momento. 

### <a name="supporting-transactional-replication"></a>Permitir la replicación transaccional
El Agente de registro del LOG supervisa el registro de transacciones de cada base de datos configurada para crear replicaciones transaccionales y copia las transacciones marcadas para la replicación desde el registro de transacciones a la base de datos de distribución. Para obtener más información, consulte [Cómo funciona la replicación transaccional](https://msdn.microsoft.com/library/ms151706.aspx).

### <a name="supporting-high-availability-and-disaster-recovery-solutions"></a>Compatibilidad con las soluciones de alta disponibilidad y recuperación ante desastres
Las soluciones de servidor en espera, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], creación de reflejo de la base de datos y trasvase de registros dependen en gran medida del registro de transacciones. 

En un **escenario de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]** , cada actualización de una base de datos, la réplica principal, se reproduce de inmediato en copias completas e independientes de la base de datos, las réplicas secundarias. La réplica principal envía las entradas del registro inmediatamente a las réplicas secundarias, que aplican las entradas del registro entrantes a las bases de datos de los grupos de disponibilidad, poniéndolas al día. Para obtener más información, consulte [Instancias de clúster de conmutación por error de AlwaysOn](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)

En un **escenario de trasvase de registros**, el servidor principal envía el registro de transacciones activo de la base de datos principal a uno o varios destinos. Los servidores secundarios restauran el registro en su base de datos secundaria local. Para obtener más información, consulte [Acerca del trasvase de registros](../../database-engine/log-shipping/about-log-shipping-sql-server.md). 

En un **escenario de creación de reflejo de la base de datos**, las actualizaciones de una base de datos (la principal) se reproducen inmediatamente en una copia completa e independiente de la base de datos (la base de datos reflejada). La instancia de servidor principal envía de forma inmediata los registros a la instancia del servidor reflejado, que los aplica a la base de datos reflejada, poniéndola al día de forma continua. Para obtener más información, consulte [Creación de reflejo de la base de datos](../../database-engine/database-mirroring/database-mirroring-sql-server.md).

##  <a name="Characteristics"></a>Transaction Log characteristics

Características del registro de transacciones de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]: 
-  El registro de transacciones se implementa como un archivo o un grupo de archivos separado en la base de datos. La caché del registro se administra por separado respecto a la caché del búfer para las páginas de datos, lo cual da lugar a un código sencillo, rápido y sólido en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Para obtener más información, consulte [Arquitectura física del registro de transacciones](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch).
-  El formato de los registros y las páginas no tiene las restricciones de formato de las páginas de datos.
-  El registro de transacciones se puede implementar en varios archivos. Si se establece el valor `FILEGROWTH` del registro, se puede definir que los archivos se expandan automáticamente. Esto reduce las posibilidades de quedarse sin espacio en el registro de transacciones, al mismo tiempo que se reduce el trabajo administrativo. Para obtener más información, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
-  El mecanismo para volver a utilizar el espacio de los archivos de registro es rápido y tiene un efecto mínimo en el rendimiento de las transacciones.

Para obtener información sobre la arquitectura del registro de transacciones y los elementos internos, vea la [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

##  <a name="Truncation"></a> Truncamiento del registro de transacciones  
El truncamiento del registro libera el espacio en el archivo de registro para que lo pueda reutilizar el registro de transacciones. Debe truncar el registro de transacciones periódicamente para evitar que se llene el espacio asignado. Varios factores pueden retrasar el truncamiento del registro, por lo que es importante supervisar su tamaño. Algunas operaciones se pueden registrar mínimamente para reducir su impacto sobre el tamaño del registro de transacciones.  
 
El truncamiento del registro elimina los [archivos de registro virtuales (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) inactivos del registro de transacciones lógico de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], liberando espacio en el registro lógico para que lo reutilice el registro de transacciones físico. Si un registro de transacciones no se trunca nunca, acabará ocupando todo el espacio de disco asignado a los archivos de registro físicos.  
  
Para evitar quedarse sin espacio, a menos que el truncamiento del registro se retrase por algún motivo, el truncamiento se produce automáticamente después de los eventos siguientes:  
  
- En el modelo de recuperación simple, después de un punto de comprobación.  
- En el modelo de recuperación completa o de recuperación optimizado para cargas masivas de registros, si se ha producido un punto de comprobación desde la copia de seguridad anterior, el truncamiento se produce después de una copia de seguridad de registros (a menos que sea una copia de seguridad de registros de solo copia).  
  
 Para obtener más información, vea [Factores que pueden ralentizar el truncamiento del registro](#FactorsThatDelayTruncation), más adelante en este tema.  
  
> [!NOTE]
> El truncamiento del registro no reduce el tamaño del archivo de registro físico. Para reducir el tamaño físico de un archivo de registro físico, debe reducir el archivo de registro. Para obtener información sobre cómo reducir el tamaño de un archivo de registro físico, vea [Manage the Size of the Transaction Log File](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
> Pero tenga en cuenta los [Factores que pueden ralentizar el truncamiento del registro](#FactorsThatDelayTruncation). Si se requiere el espacio de almacenamiento de nuevo después de reducir un registro, el registro de transacciones volverá a crecer y esto implicará una sobrecarga de rendimiento durante las operaciones de ampliación de registro.
  
##  <a name="FactorsThatDelayTruncation"></a> Factors that can delay log truncation  
 Cuando las entradas de registro permanecen activas durante una transacción de larga duración, se retrasa el truncamiento del registro y es posible que se llene el registro de transacciones, como ya hemos mencionado anteriormente en este tema largo.  
  
> [!IMPORTANT]
> Para obtener más información sobre cómo actuar ante un registro de transacciones lleno, vea [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 En realidad, el truncamiento del registro se puede retrasar por diversos motivos. Para saber qué es lo que impide el truncamiento del registro, si hay alguna causa, consulte las columnas **log_reuse_wait** y **log_reuse_wait_desc** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). En la tabla siguiente se describen los valores de estas columnas.  
  
|valor log_reuse_wait|valor log_reuse_wait_desc|Descripción|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Hay actualmente uno o más [archivos de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) reutilizables.|  
|1|CHECKPOINT|No se ha producido ningún punto de comprobación desde el último truncamiento o el encabezado del registro no se ha movido más allá de un [archivo de registro virtual (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch). (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual para retrasar el truncamiento. Para obtener más información, vea [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|Se requiere una copia de seguridad del registro para que se pueda truncar el registro de transacciones. (Solo modelos de recuperación completa u optimizada para cargas masivas de registros)<br /><br /> Cuando se completa la siguiente copia de seguridad de registros, es posible que se pueda reutilizar parte del espacio de registro.|  
|3|ACTIVE_BACKUP_OR_RESTORE|Existe una recuperación o copia de seguridad de datos en curso (todos los modelos de recuperación).<br /><br /> Si la copia de seguridad de una base de datos impide el truncamiento del registro, la cancelación de la operación de copia de seguridad podría ayudar a solucionar el problema inmediato.|  
|4|ACTIVE_TRANSACTION|Existe una transacción activa (todos los modelos de recuperación):<br /><br /> Podría existir una transacción de larga duración en el inicio de la copia de seguridad del registro. En este caso, para liberar espacio se podría requerir otra copia de seguridad del registro. Tenga en cuenta que las transacciones de ejecución prolongada impiden el truncamiento del registro en todos los modelos de recuperación, incluido el modelo de recuperación simple, en el que, por lo general, el registro de transacciones se trunca en cada punto de comprobación automático.<br /><br /> Una transacción está diferida. Una *transacción diferida* es efectivamente una transacción activa cuya reversión se bloquea debido a algún recurso no disponible. Para obtener más información sobre las causas de las transacciones diferidas y cómo sacarlas del estado diferido, vea [Transacciones diferidas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).<br /> <br /> Las transacciones de larga ejecución también podrían llenar el registro de transacciones de tempdb. Las transacciones de usuario usan implícitamente tempdb para objetos internos como tablas de trabajo para ordenar, archivos de trabajo para crear valores hash, tablas de trabajo de cursor y versiones de fila. Incluso si la transacción de usuario incluye datos de solo lectura (consultas de `SELECT`), los objetos internos se pueden crear y usar en las transacciones de usuario. Después, se puede rellenar el registro de transacciones de tempdb.|  
|5|DATABASE_MIRRORING|Se realiza una pausa en la creación de reflejo de la base de datos o, en el modo de alto rendimiento, la base de datos reflejada está notablemente detrás de la base de datos principal. (Solo para el modelo de recuperación completa)<br /><br /> Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICATION|Durante las replicaciones transaccionales, las transacciones pertinentes para las publicaciones no se han entregado aún a la base de datos de distribución. (Solo para el modelo de recuperación completa)<br /><br /> Para obtener información acerca de la replicación transaccional, vea [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Se está creando una instantánea de base de datos. (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual, por lo general breve, para retrasar el truncamiento del registro.|  
|8|LOG_SCAN|Se está realizando un examen de registro. (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual, por lo general breve, para retrasar el truncamiento del registro.|  
|9|AVAILABILITY_REPLICA|Una réplica secundaria de un grupo de disponibilidad está aplicando entradas del registro de transacciones de esta base de datos a una base de datos secundaria correspondiente. (Modelo de recuperación completa)<br /><br /> Para obtener más información, vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|-|Exclusivamente para uso interno.|  
|11|-|Exclusivamente para uso interno.|  
|12|-|Exclusivamente para uso interno.|  
|13|OLDEST_PAGE|Si una base de datos está configurada para usar puntos de comprobación indirectos, la página más antigua de la base de datos podría ser anterior al [número de secuencia de registro (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) del punto de comprobación. En este caso, la página más antigua puede retrasar el truncamiento del registro. (Todos los modelos de recuperación)<br /><br /> Para obtener más información sobre los puntos de comprobación indirectos, vea [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|No se utiliza este valor actualmente.|  
  
##  <a name="MinimallyLogged"></a> Operaciones que se pueden registrar mínimamente  
El*registro mínimo* implica registrar únicamente la cantidad de información necesaria para recuperar la transacción sin permitir la recuperación a un momento dado. En este tema se identifican las operaciones que se registran mínimamente en el [modelo de recuperación](../backup-restore/recovery-models-sql-server.md) optimizado para cargas masivas de registros (y en el modelo de recuperación simple, excepto cuando se está ejecutando una copia de seguridad).  
  
> [!NOTE]
> Las tablas optimizadas para memoria no admiten el registro mínimo.  
  
> [!NOTE]
> Con el [modelo de recuperación](../backup-restore/recovery-models-sql-server.md)completa, todas las operaciones masivas se registran completamente. Sin embargo, puede usar el registro mínimo en un conjunto de operaciones masivas cambiando la base de datos temporalmente al modelo de recuperación optimizado para cargas masivas de registros para este tipo de operaciones. El registro mínimo resulta más eficaz que el registro completo y reduce la posibilidad de que una operación masiva a gran escala termine por ocupar todo el espacio del registro de transacciones durante una transacción masiva. Sin embargo, si la base de datos se daña o se pierde cuando el registro mínimo está activo, no se podrá recuperar la base de datos hasta el momento del error.  
  
 Las operaciones siguientes, que se registran completamente en el modelo de recuperación completa, se registran mínimamente en el modelo de recuperación simple y en el optimizado para cargas masivas de registros:  
  
-   Operaciones de importación en bloque ([bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [INSERT... SELECT](../../t-sql/statements/insert-transact-sql.md)). Para obtener más información sobre cuándo se registra mínimamente una importación masiva en una tabla, vea [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
Cuando la replicación transaccional está habilitada, las operaciones `BULK INSERT` se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
-   Operaciones [SELECT INTO](../../t-sql/queries/select-into-clause-transact-sql.md).  
  
Cuando la replicación transaccional está habilitada, las operaciones SELECT INTO se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
-   Actualizaciones parciales de tipos de datos de valores grandes que usan la cláusula `.WRITE` de la instrucción [UPDATE](../../t-sql/queries/update-transact-sql.md) al insertar o anexar datos nuevos. Tenga en cuenta que el registro mínimo no se utiliza cuando se actualizan valores existentes. Para obtener más información sobre los tipos de datos de valores grandes, vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Las instrucciones[WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) y [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) al insertar o anexar datos nuevos en las columnas de tipos de datos **text**, **ntext**, y **image** . Tenga en cuenta que el registro mínimo no se utiliza cuando se actualizan valores existentes.  
  
    > [!WARNING]
    > Las instrucciones `WRITETEXT` y `UPDATETEXT` ha quedado **en desuso**; evite usarlas en las nuevas aplicaciones.  
  
-   Si la base de datos está establecida en el modelo de recuperación optimizado para cargas masivas de registros o simple, algunas operaciones DDL de índices se registran mínimamente con independencia de si la operación se ejecuta sin conexión o con conexión. Las operaciones de índice con registro mínimo son:  
  
    -   Operaciones[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) (incluidas las vistas indexadas).  
  
    -   Operaciones[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) REBUILD o DBCC DBREINDEX.  
  
        > [!WARNING]
        > La instrucción `DBCC DBREINDEX` ha quedado **en desuso**, de modo que no conviene usarla en las aplicaciones nuevas.  
  
    -   Regeneración del nuevo montón [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) (si procede). La desasignación de páginas de índice durante una operación `DROP INDEX` **siempre** se registra completamente.
  
##  <a name="RelatedTasks"></a> Related tasks  
**Administrar el registro de transacciones**  
  
-   [Administrar el tamaño del archivo de registro de transacciones](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)  
  
-   [Solucionar problemas de un registro de transacciones lleno &#40;Error 9002 de SQL Server&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
**Realizar copia de seguridad de un registro de transacciones (modelo de recuperación completa)**  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
**Restaurar el registro de transacciones (modelo de recuperación completa)**  
  
-   [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
[Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)   
[Controlar la durabilidad de las transacciones](../../relational-databases/logs/control-transaction-durability.md)   
[Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
[Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
[Puntos de comprobación de base de datos &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
[Ver o cambiar las propiedades de una base de datos](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)   
[Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
[Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  
  
