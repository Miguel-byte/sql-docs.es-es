---
title: MSSQLSERVER_3313 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3313 (Database Engine error)
ms.assetid: a244227b-8553-42df-9435-034f906c4c74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dc4d894dc03a53892b69f33dbf153cdd15fcf340
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914523"
---
# <a name="mssqlserver3313"></a>MSSQLSERVER_3313
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3313|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ERR_LOG_RID1|  
|Texto del mensaje|Durante la puesta al día de una operación registrada en la base de datos '%.*ls', se produjo un error en la entrada de registro con id. %S_LSN. Normalmente, el error específico se registra antes como un error en el servicio Registro de eventos de Windows. Restaure la base de datos a partir de una copia de seguridad completa o repare la base de datos.|  
  
## <a name="explanation"></a>Explicación  
 Este es un error de acumulación en la recuperación de una operación de rehacer. Este error ha colocado la base de datos en el estado SUSPECT. El grupo de archivos principal, y posiblemente otros grupos de archivos, es sospechoso y puede estar dañado. La base de datos no se puede recuperar durante el inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, por consiguiente, no está disponible. Se requiere una acción por parte del usuario para resolver el problema.  
  
 Tenga en cuenta que si este error se produce para **tempdb**, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cierra.  
  
## <a name="user-action"></a>Acción del usuario  
 Una condición transitoria que se dio en el sistema durante un intento determinado de iniciar la instancia del servidor o recuperar una base de datos puede producir este error. También puede deberse a un error permanente que se produce cada vez que se intenta iniciar la base de datos. Para obtener información acerca de la causa, examine el registro de eventos de Windows para ver si contiene un error anterior que indique el error concreto.  
  
 Tenga en cuenta que cuando se encuentra esta condición de error, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente genera tres archivos en la carpeta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **LOG**. El archivo SQLDump*nnnn*.txt contiene información de diagnóstico avanzada relacionada con los errores, incluidos detalles sobre la transacción y la página en las que se encontró el problema. El equipo de soporte técnico de productos suele usar esta información para analizar el motivo del error.  
  
 Para obtener información sobre la causa de esta repetición del error 3313, busque en el registro de eventos de Windows un error anterior que indique el error específico. La acción del usuario adecuada depende de si la información del registro de eventos de Windows indica que el error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo causó una condición transitoria o un error permanente. Para obtener información sobre las acciones del usuario para solucionar el error 3313, consulte los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
