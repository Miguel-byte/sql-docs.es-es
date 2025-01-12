---
title: Migración de la configuración de copia de seguridad administrada de SQL Server 2014 a SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7d8945b0e37185f5ec0433a9780aa876d4be526c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033753"
---
# <a name="migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016"></a>Migración de la configuración de copia de seguridad administrada de SQL Server 2014 a SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se tratan las consideraciones de migración para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] al actualizar desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
 Los procedimientos y el comportamiento subyacente de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] han cambiado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. En las secciones siguientes se describen los cambios funcionales y sus implicaciones.  
  
## <a name="overview"></a>Información general  
 En la tabla siguiente se describen algunas de las principales diferencias funcionales para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] entre [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
|Área|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
|----------|---------------------------|---------------------------|  
|**Espacio de nombres:**|smart_admin|managed_backup|  
|**Procedimientos almacenados del sistema:**|sp_set_db_backup<br /><br /> sp_set_instance_backup|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)<br /><br /> [sp_backup_config_advanced](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)<br /><br /> [sp_backup_config_schedule](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|  
|**Seguridad:**|Credencial de SQL con una clave de acceso y la cuenta de almacenamiento de Microsoft Azure.|Credencial de SQL con un token de firma de acceso compartido (SAS) de Microsoft Azure.|  
|**Almacenamiento subyacente:**|Almacenamiento de Microsoft Azure mediante blobs en páginas.|Almacenamiento de Microsoft Azure mediante blobs en bloques.|  
  
## <a name="benefits"></a>Ventajas  
 Hay varias ventajas en usar la nueva funcionalidad en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
-   Los blobs en bloques cuestan menos que el almacenamiento.  
  
-   Con el seccionamiento, puede almacenar copias de seguridad mucho mayores (12 TB en comparación con 1 TB para blobs en páginas).  
  
-   El seccionamiento también mejora el tiempo de restauración para bases de datos grandes  
  
-   Para conocer otras mejoras de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], vea [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="considerations"></a>Consideraciones  
 Después de actualizar desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], tenga en cuenta las siguientes consideraciones de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :  
  
-   Las bases de datos configuradas previamente para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] continuarán usando los procedimientos del sistema y el comportamiento subyacente de **smart_admin** en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
-   Los procedimientos de **smart_admin** no se admiten para las nuevas configuraciones de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Debe usar los procedimientos y la funcionalidad nuevos de **managed_backup** .  
  
## <a name="see-also"></a>Consulte también  
 [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
