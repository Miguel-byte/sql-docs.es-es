---
title: sp_browsemergesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: stevestein
ms.author: sstein
ms.openlocfilehash: 92df93d1c14b10aa6587d0eaf13f4de81bc4d7f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046009"
---
# <a name="spbrowsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la ruta de acceso completa de la última instantánea generada para una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(2000)**|Ruta de acceso completa del directorio de instantáneas.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_browsemergesnapshotfolder** se utiliza en la replicación de mezcla.  
  
 Si la publicación está configurada para generar archivos de instantáneas en el directorio de trabajo y en la carpeta de instantáneas del publicador, el conjunto de resultados contendrá dos filas: la primera fila contendrá la carpeta de instantáneas de la publicación y la segunda fila contendrá el directorio de trabajo del publicador.  
  
 **sp_browsemergesnapshotfolder** es útil para determinar el directorio donde se generan los archivos de instantáneas de mezcla. Esta carpeta o ruta de acceso y su contenido se pueden copiar en un medio extraíble, así como la instantánea utilizada para sincronizar una suscripción desde una ubicación de instantáneas alternativa.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_browsemergesnapshotfolder**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
