---
title: Migración de bases de datos a SQL Server en Linux
description: En este artículo, se describen las distintas opciones para migrar bases de datos y datos a SQL Server en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: e7affa88f1856571d0b2142f7dcfdf762ed79197
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68129352"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migración de bases de datos y datos estructurados a SQL Server en Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede migrar sus bases de datos y datos a una instancia de SQL Server que se ejecute en Linux. El método que use depende de los datos de origen y del escenario específico. En las secciones siguientes, encontrará procedimientos recomendados para distintos escenarios de migración.

## <a name="migrate-from-sql-server-on-windows"></a>Migrar desde SQL Server en Windows
Para migrar bases de datos de SQL Server en Windows a SQL Server en Linux, la técnica recomendada es usar la función de copia de seguridad y restauración de SQL Server.

1. Cree una copia de seguridad de la base de datos en el equipo con Windows.
2. Transfiera el archivo de copia de seguridad al equipo de destino con SQL Server para Linux.
3. Restaure la copia de seguridad en el equipo con Linux. 

Vea el tema siguiente para obtener instrucciones paso a paso de cómo migrar una base de datos con la función de copia de seguridad y restauración:

- [Restaurar una base de datos SQL Server de Windows a Linux](sql-server-linux-migrate-restore-database.md).

También puede exportar la base de datos a un archivo BACPAC (un archivo comprimido que contiene el esquema de la base de datos y los datos). Si tiene un archivo BACPAC, puede transferir el archivo al equipo con Linux y, después, importarlo en SQL Server. Para obtener más información, consulte los temas siguientes:

- [Exportar e importar una base de datos con SSMS o SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrar desde otros servidores de bases de datos
Puede migrar bases de datos que se encuentren en otros sistemas de bases de datos SQL Server en Linux. Algunos ejemplos son bases de datos de Microsoft Access, DB2, MySQL, Oracle y Sybase. En este escenario, use el Asistente para la administración de SQL Server (SSMA) para automatizar la migración a SQL Server en Linux. Para obtener más información, vea [Usar SSMA para migrar bases de datos a SQL Server en Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrar datos estructurados
También hay técnicas para importar datos sin procesar. Puede que tenga archivos de datos estructurados que se han exportado desde otras bases de datos u orígenes de datos. En este caso, puede usar la herramienta bcp para insertar los datos de forma masiva. También puede usar SQL Server Integration Services en Windows para importar los datos en una base de datos de SQL Server en Linux. SQL Server Integration Services le permite ejecutar transformaciones más complejas en los datos durante la importación. 

Para obtener más información sobre estas técnicas, vea los temas siguientes:

- [Copia masiva de datos con bcp](sql-server-linux-migrate-bcp.md)
- [Extraer, transformar y cargar datos para SQL Server en Linux con SSIS](sql-server-linux-migrate-ssis.md) 
