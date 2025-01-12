---
title: sp_copysubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
author: stevestein
ms.author: sstein
ms.openlocfilehash: d1a093364192e3bab32a2fa0234c7198d8e0f3ff
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771429"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  La característica de suscripciones adjuntables ha quedado desusada y se retirará en versiones posteriores. Esta característica no se debe utilizar en nuevos trabajos de desarrollo. En las publicaciones de combinación en las que se han creado particiones mediante filtros con parámetros, se recomienda utilizar las nuevas características de las instantáneas con particiones, que simplifican la inicialización de un gran número de suscripciones. Para más información, consulte [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). En las publicaciones que no están divididas en particiones, puede inicializar una suscripción con una copia de seguridad. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Copia una base de datos de suscripciones que tiene suscripciones de extracción, pero no de inserción. Solo se pueden copiar bases de datos de un único archivo. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filename = ] 'file_name'`Es la cadena que especifica la ruta de acceso completa, incluido el nombre de archivo, en la que se guarda una copia del archivo de datos (. MDF). *el nombre de archivo* es **nvarchar (260)** y no tiene ningún valor predeterminado.  
  
`[ @temp_dir = ] 'temp_dir'`Es el nombre del directorio que contiene los archivos temporales. *temp_dir* es de tipo **nvarchar (260)** y su valor predeterminado es NULL. Si es null, [!INCLUDE[msCoName](../../includes/msconame-md.md)] se utilizará el directorio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos predeterminado. El directorio debe tener espacio suficiente para contener un archivo que tenga el tamaño de todos los archivos de la base de datos del suscriptor combinados.  
  
`[ @overwrite_existing_file = ] 'overwrite_existing_file'`Es una marca booleana opcional que especifica si se sobrescribirá o no un archivo existente con el mismo nombre especificado **@filename** en. *overwrite_existing_file*es de **bit**y su valor predeterminado es **0**. Si es **1**, sobrescribe el archivo especificado por **@filename** , si existe. Si es **0**, se produce un error en el procedimiento almacenado si el archivo existe y el archivo no se sobrescribe.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_copysubscription** se utiliza en todos los tipos de replicación para copiar una base de datos de suscripciones en un archivo como alternativa a la aplicación de una instantánea en el suscriptor. La base de datos se debe configurar para que solo admita suscripciones de extracción. Los usuarios que tengan los permisos apropiados pueden realizar copias de la base de datos de suscripciones y, a continuación, enviar por correo electrónico, copiar o transportar el archivo de suscripción (.msf) a otro suscriptor, donde se puede adjuntar como una suscripción.  
  
 El tamaño de la base de datos de suscripciones que se va a copiar debe ser inferior a 2 gigabytes (GB).  
  
 **sp_copysubscription** solo se admite para las bases de datos con suscripciones de cliente y no se puede ejecutar cuando la base de datos tiene suscripciones de servidor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_copysubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../relational-databases/replication/snapshot-options.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
