---
title: Creación de una clave maestra de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: aliceku
ms.author: aliceku
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8cc28ed0dcee4f8622a293114cfc4f83f5919240
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978050"
---
# <a name="create-a-database-master-key"></a>Crear la clave maestra de una base de datos

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
En este tema se describe cómo crear una clave maestra de base de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].

## <a name="security"></a>Seguridad

### <a name="permissions"></a>Permisos

Necesita el permiso CONTROL en la base de datos.

## <a name="using-transact-sql"></a>Usar Transact-SQL

### <a name="to-create-a-database-master-key"></a>Para crear la clave maestra de una base de datos

1. Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos.
2. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **Bases de datos del sistema**, haga clic con el botón derecho en `master` y, después, haga clic en **Nueva consulta**.
4. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.

   ```sql
     -- Creates the master key.
     -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
     CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   ```

Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md).
