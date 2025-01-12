---
title: sp_adddistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2190e31245cde19eca4c5a47f21ac48e12f57f53
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771388"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Configura un publicador para que utilice una base de datos de distribución determinada. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos. Tenga en cuenta que los procedimientos almacenados [sp_adddistributor &#40;Transact&#41; -SQL](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) y [ &#40;sp_adddistributiondb de&#41; Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) deben ejecutarse antes de usar este procedimiento almacenado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @distribution_db = ] 'distribution_db'`Es el nombre de la base de datos de distribución. *distributor_db* es de **tipo sysname**y no tiene ningún valor predeterminado. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
`[ @security_mode = ] security_mode`Es el modo de seguridad implementado. Este parámetro solo lo utilizan los agentes de replicación para conectarse al publicador para las suscripciones de actualización en cola o con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un publicador que no sea de. *security_mode* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Los agentes de replicación del distribuidor utilizan la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse al publicador.|  
|**1** (predeterminado)|Los agentes de replicación del distribuidor utilizan la autenticación de Windows para conectarse al publicador.|  
  
`[ @login = ] 'login'`Es el inicio de sesión. Este parámetro es necesario si *security_mode* es **0**. *login* es de tipo **sysname** y su valor predeterminado es NULL. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
`[ @password = ] 'password']`Es la contraseña. *password* es de **tipo sysname y su**valor predeterminado es NULL. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura.  
  
`[ @working_directory = ] 'working_directory'`Es el nombre del directorio de trabajo utilizado para almacenar los archivos de datos y de esquema para la publicación. *working_directory* es de tipo **nvarchar (255)** y su valor predeterminado es la carpeta ReplData para esta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instancia de, `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`por ejemplo. El nombre se debe especificar en el formato UNC.  

 Para Azure SQL Database, use `\\<storage_account>.file.core.windows.net\<share>`.

`[ @storage_connection_string = ] 'storage_connection_string'`Se requiere para SQL Database. Use la clave de acceso de Azure portal en configuración de > de almacenamiento.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'`Este parámetro está en desuso y solo se proporciona por compatibilidad con versiones anteriores. *Trusted* es de tipo **nvarchar (5)** y establecerlo en cualquier cosa, pero **false** producirá un error.  
  
`[ @encrypted_password = ] encrypted_password`Ya no se admite la configuración de *encrypted_password* . Si se intenta establecer este parámetro de **bits** en **1** se producirá un error.  
  
`[ @thirdparty_flag = ] thirdparty_flag`Es cuando el publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]es. *thirdparty_flag* es de **bit**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**1**|Otra base de datos distinta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
`[ @publisher_type = ] 'publisher_type'`Especifica el tipo de publicador cuando el publicador no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]lo es. *publisher_type* es de tipo sysname y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (predeterminado).|Especifica un publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica un publicador estándar de Oracle.|  
|**PUERTA DE ENLACE DE ORACLE**|Especifica un publicador de puerta de enlace de Oracle.|  
  
 Para obtener más información acerca de las diferencias entre un publicador de Oracle y un publicador de puerta de enlace de Oracle, vea [configurar un publicador de Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adddistpublisher** se utiliza en la replicación de instantáneas, la replicación transaccional y la replicación de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_adddistpublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
