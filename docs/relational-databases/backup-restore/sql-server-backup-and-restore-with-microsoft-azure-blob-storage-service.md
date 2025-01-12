---
title: Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 169e437c141d379401b7a3294f0ae852d756374f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041372"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>Copia de seguridad y restauración de SQL Server con el servicio Microsoft Azure Blob Storage.
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![Copia de seguridad en un gráfico de blobs de Azure](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "Copia de seguridad en un gráfico de blobs de Azure")  
  
 En este tema se describen las copias de seguridad y la restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir del [servicio de Almacenamiento de blobs de Microsoft Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). También se proporciona un resumen de las ventajas de usar el servicio BLOB de Microsoft Azure para almacenar copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 SQL Server permite almacenar las copias de seguridad del servicio de Almacenamiento de blobs de Microsoft Azure de las maneras siguientes:  
  
-   **Administrar las copias de seguridad de Microsoft Azure:** con los mismos métodos usados para hacer una copia de seguridad en disco y cinta, ahora puede realizar la copia de seguridad en el almacenamiento de Microsoft Azure mediante la especificación de la dirección URL como destino de copia de seguridad. Puede utilizar esta característica para realizar la copia de seguridad manualmente o para configurar su propia estrategia de copia de seguridad como haría para un almacenamiento local u otras opciones fuera de las instalaciones. Esta característica también se conoce como **Copia de seguridad en URL de SQL Server**. Para obtener más información, vea [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md). Esta característica está disponible en SQL Server 2012 SP1 CU2 o posterior. Esta característica se ha mejorado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para proporcionar un mayor rendimiento y funcionalidad mediante el uso de blobs en bloques, firmas de acceso compartido y la creación de bandas.  
  
    > [!NOTE]  
    >  En las versiones de SQL Server anteriores a SQL Server 2012 SP1 CU2, puede usar el complemento de la herramienta de Microsoft Azure Copia de seguridad de SQL Server para crear rápida y fácilmente copias de seguridad del Almacenamiento de Microsoft Azure. Para obtener más información, vea [centro de descarga](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Copias de seguridad de instantánea de archivos para archivos de base de datos en el Almacenamiento de blobs de Azure** Mediante el uso de instantáneas de Azure, las copias de seguridad de instantánea de archivo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrecen copias de seguridad y restauraciones casi instantáneas de archivos de base de datos almacenados mediante el servicio de Almacenamiento de blobs de Azure. Esta función permite simplificar las directivas de copia de seguridad y restauración y admite la restauración a un momento dado. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md). Esta característica está disponible en SQL Server 2016 o posterior.  
  
-   **Permitir que SQL Server administre las copias de seguridad en Microsoft Azure:** Configure SQL Server para administrar la estrategia de copia de seguridad y programar las copias de seguridad de una o varias bases de datos, o bien establezca valores predeterminados en el nivel de instancia. Esta característica se conoce como **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** . Para obtener más información, vea [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md). Esta característica está disponible en SQL Server 2014 o posterior.  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Ventajas de usar el servicio BLOB de Microsoft Azure para las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Almacenamiento externo flexible, fiable e ilimitado: El almacenamiento de las copias de seguridad en el servicio Microsoft Azure Blob Storage puede ser una opción externa cómoda, flexible y de fácil acceso. La creación de almacenamiento externo para las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser tan sencillo como modificar los scripts y trabajos existentes. Normalmente, el almacenamiento externo debe estar suficientemente alejado de la ubicación de la base de datos de producción para impedir que un desastre afecte a las ubicaciones de las bases de datos externa y de producción. La elección de la replicación geográfica en el almacenamiento de blobs permite disponer de un nivel de protección adicional en caso de que se produzca un desastre que pueda afectar a toda la región. Además, las copias de seguridad están disponibles desde cualquier lugar y en cualquier momento y se puede tener acceso a ellas fácilmente para las restauraciones.  
  
    > [!IMPORTANT]  
    >  Mediante el uso de blobs en bloques en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede crear bandas en su conjunto de copia de seguridad para admitir archivos de copia de seguridad de hasta 12,8 TB.  
  
-   Archivo de copia de seguridad: El servicio Microsoft Azure Blob Storage ofrece una alternativa mejor que la opción de cinta que se suele usar para archivar copias de seguridad. El almacenamiento en cinta puede requerir el transporte físico a una instalación externa y medidas para proteger los medios. El almacenamiento de las copias de seguridad en el servicio Azure Blob Storage proporciona una opción de archivado instantánea, de alta disponibilidad y duradera.  
  
-   No hay sobrecarga en la administración de hardware: No hay ninguna sobrecarga de administración de hardware con los servicios de Microsoft Azure. Los servicios de Microsoft Azure administran el hardware y proporcionan replicación geográfica para ofrecer redundancia y protección frente a errores de hardware.  
  
-   Actualmente, para las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en una máquina virtual de Microsoft Azure, se pueden realizar copias de seguridad en los servicios de Almacenamiento de blobs de Microsoft Azure mediante la creación de discos conectados. Sin embargo, hay un límite en cuanto al número de discos que puede conectar a una máquina virtual de Microsoft Azure. Este límite es de 16 discos para una instancia muy grande e inferior para instancias menores. Al habilitar una copia de seguridad directa en el Almacenamiento de blobs de Microsoft Azure, puede eludir el límite de 16 discos.  
  
     Además, el archivo de copia de seguridad que ahora se almacena en el servicio de Almacenamiento de blobs de Microsoft Azure está disponible directamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local o en otro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en una máquina virtual de Microsoft Azure, sin necesidad de adjuntar o separar bases de datos o de descargar y conectar el disco duro virtual.  
  
-   Ventajas de costo: Solo se paga por el servicio que se usa. Puede ser rentable como opción de archivado externo y de copia de seguridad. Vea la sección sobre [Consideraciones sobre la facturación de Microsoft Azure](#Billing) para obtener más información y vínculos.  
  
##  <a name="Billing"></a> Consideraciones sobre la facturación de Microsoft Azure:  
 Entender los costos de Almacenamiento de Microsoft Azure permite prever el costo de crear y almacenar copias de seguridad en Microsoft Azure.  
  
 La [calculadora de precios de Microsoft Azure](https://go.microsoft.com/fwlink/?LinkId=277060) puede ayudarle a calcular los costos.  
  
 **Storage:** Los cargos se basan en el espacio usado y se calculan según una escala graduada y el nivel de redundancia. Para obtener más detalles e información actualizada, vea la sección **Administración de datos** del artículo [Detalles de precios](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Transferencia de datos:** las transferencias de datos de entrada a Microsoft Azure son gratuitas. Las transferencias salientes se cobran por el uso de ancho de banda y se calculan según una escala graduada específica de la región. Para obtener más detalles, vea la sección [Transferencias de datos](https://go.microsoft.com/fwlink/?LinkId=277061) del artículo Detalles de precios.  
  
## <a name="see-also"></a>Consulte también  

[Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[Tutorial: Uso del servicio Microsoft Azure Blob Storage con bases de datos de SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[Copia de seguridad en URL de SQL Server](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
