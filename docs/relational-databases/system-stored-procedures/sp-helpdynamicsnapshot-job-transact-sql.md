---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 55d7ad0dfd941102cfeb6661e65980f980fa8b2d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770976"
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve información sobre trabajos del agente que generan instantáneas de datos filtrados. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y su **%** valor predeterminado es, que devuelve información sobre todos los trabajos de instantánea de datos filtrados que coinciden con los valores de *dynamic_snapshot_jobid*y *dynamic_snapshot_jobname*especificados para todos los aquellas.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`Es el nombre de un trabajo de instantánea de datos filtrados. *dynamic_snapshot_jobname*es de **%** **tipo sysname y su**valor predeterminado es ', que devuelve todos los trabajos dinámicos de una publicación con el *dynamic_snapshot_jobid*especificado. Si no se especificó un nombre de trabajo explícitamente cuando se creó el trabajo, el formato del nombre del trabajo es el siguiente:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`Es un identificador para un trabajo de instantánea de datos filtrados. *dynamic_snapshot_jobid*es de tipo **uniqueidentifier**y su valor predeterminado es null, que devuelve todos los trabajos de instantáneas que coinciden con el *dynamic_snapshot_jobname*especificado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica el trabajo de instantáneas de datos filtrados.|  
|**job_name**|**sysname**|Nombre del trabajo de instantáneas de datos filtrados.|  
|**job_id**|**uniqueidentifier**|Identifica el [!INCLUDE[msCoName](../../includes/msconame-md.md)] trabajo del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente en el distribuidor.|  
|**dynamic_filter_login**|**sysname**|Valor utilizado para evaluar la función [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) en un filtro de fila con parámetros definido para la publicación.|  
|**dynamic_filter_hostname**|**sysname**|Valor utilizado para evaluar la función [host_name](../../t-sql/functions/host-name-transact-sql.md) en un filtro de fila con parámetros definido para la publicación.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Ruta a la carpeta de la que se leen los archivos de instantáneas si se utiliza un filtro de fila con parámetros.|  
|**frequency_type**|**int**|Se trata de la frecuencia de ejecución programada del agente, que puede ser uno de estos valores.<br /><br /> **1** = una vez<br /><br /> **2** = a petición<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente relativo<br /><br /> **64** = AutoStart<br /><br /> **128** = recurrente|  
|**frequency_interval**|**int**|Los días en los que se ejecuta el agente; puede tener los valores siguientes.<br /><br /> **1** = Domingo<br /><br /> **2** = lunes<br /><br /> **3** = martes<br /><br /> **4** = miércoles<br /><br /> **5** = jueves<br /><br /> **6** = viernes<br /><br /> **7** = sábado<br /><br /> **8** = día<br /><br /> **9** = días de la semana<br /><br /> **10** = días del fin de semana|  
|**frequency_subday_type**|**int**|Es el tipo que define la frecuencia con que se ejecuta el agente cuando *frequency_type* es **4** (Daily) y puede tener uno de estos valores.<br /><br /> **1** = en el momento especificado<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que se producen entre la ejecución programada del agente.|  
|**frequency_relative_interval**|**int**|Es la semana en la que el agente se ejecuta en un mes determinado cuando *frequency_type* es **32** (relativo mensual) y puede tener uno de estos valores.<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**int**|Número de semanas o meses entre las ejecuciones programadas del agente.|  
|**active_start_date**|**int**|Fecha en que se programa la primera ejecución del agente, con el formato AAAAMMDD.|  
|**active_end_date**|**int**|Fecha en que se programa la última ejecución del agente, con el formato AAAAMMDD.|  
|**active_start_time**|**int**|Hora en que se programa la primera ejecución del agente, con el formato HHMMSS.|  
|**active_end_time**|**int**|Hora en que se programa la última ejecución del agente, con el formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdynamicsnapshot_job** se utiliza en la replicación de mezcla.  
  
 Si se utilizan todos los valores de parámetros predeterminados, se devuelve información sobre todos los trabajos de instantáneas de datos con particiones para toda la base de datos de publicaciones.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , del rol fijo de base de datos **db_owner** y de la lista de acceso a la publicación pueden ejecutar **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
