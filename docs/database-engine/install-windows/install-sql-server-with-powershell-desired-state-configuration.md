---
title: Instalar SQL Server con la configuración de estado deseado de PowerShell | Microsoft Docs
description: Obtenga información sobre cómo instalar SQL Server con Desired State Configuration (DSC) de PowerShell.
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 560e752e5559b0e79a4f123443d200ca70532ef5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63221966"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>Instalar SQL Server con la configuración de estado deseado de PowerShell

¿Cuántas veces ha recorrido la interfaz de instalación de SQL Server haciendo clic en los mismos botones y ha escrito la misma información sin pensarlo dos veces? La instalación ha finalizado y se ha olvidado de especificar el grupo DBA en el rol **sysadmin**. Después, tenía que hacer lo siguiente:
* Cambiar al modo de usuario único.
* Agregar los usuarios o grupos adecuados.
* Volver a activar SQL Server en el modo multiusuario.
* Hacer pruebas. 

Lo peor es que ya se tambalea su confianza en la totalidad de la instalación. "¿Qué más he olvidado?" podría preguntarse.

Obtenga información sobre [Desired State Configuration (DSC) de PowerShell](https://docs.microsoft.com/powershell/dsc/overview). Con DSC, se crea una plantilla de configuración que se puede volver a usar en cientos y miles de servidores. En función de la compilación, es posible que tenga que ajustar algunos de los parámetros de configuración. Pero eso no es un problema importante porque puede conservar toda la configuración estándar. Elimina la posibilidad de que se olvide de escribir un parámetro importante.

En este artículo se analiza la instalación inicial de una instancia independiente de SQL Server 2017 en Windows Server 2016 mediante el recurso de DSC **SqlServerDsc**. Tener conocimientos previos de DSC es útil ya que no se describirá el funcionamiento de DSC.

Los siguientes elementos son necesarios para realizar este tutorial:

- Un equipo en el que se ejecute Windows Server 2016.
- Medios de instalación de SQL Server 2017.
- El recurso de DSC **SqlServerDsc**.

## <a name="prerequisites"></a>Prerequisites

En la mayoría de los casos, se usa DSC para controlar los requisitos previos. Pero para los fines de esta demostración, se van a controlar de forma manual.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>Instalar el recurso de DSC SqlServerDsc

Descargue el recurso de DSC [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) desde la [Galería de PowerShell](https://www.powershellgallery.com/) con el cmdlet [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1). 

> [!NOTE]
> Asegúrese de que PowerShell se está ejecutando **Como administrador** para instalar el módulo.

```PowerShell
Install-Module -Name SqlServerDsc
```

### <a name="get-the-sql-server-2017-installation-media"></a>Obtención de los medios de instalación de SQL Server 2017
Descargue los medios de instalación de SQL Server 2017 en el servidor. Se ha descargado SQL Server 2017 Enterprise desde una suscripción de Visual Studio y se ha copiado el archivo ISO en `C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso`.

Ahora se debe extraer el archivo ISO en un directorio:

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>Crear la configuración

### <a name="configuration"></a>Configuración

Cree la función de configuración a la que se va a llamar para generar los documentos [Managed Object Format (MOF)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-):

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>Módulos

Importe los módulos a la sesión actual. Estos módulos indican al documento de configuración cómo crear los documentos MOF. También indican al motor de DSC cómo aplicar los documentos MOF en el servidor:

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>Recursos

#### <a name="net-framework"></a>.NET Framework

SQL Server se basa en .NET Framework. Por tanto, es necesario asegurarse de que está instalado antes de instalar SQL Server. El recurso **WindowsFeature** se usa para instalar la característica de Windows **Net-Framework-45-Core**:

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

El recurso **SqlSetup** se usa para indicar a DSC cómo instalar SQL Server. Los parámetros necesarios para una instalación básica son los siguientes:

- **InstanceName**. Nombre de la instancia. Use **MSSQLSERVER** para una instancia predeterminada.
- **Features**. Las características que se van a instalar. En este ejemplo, solo se instala la característica **SQLEngine**.
- **SourcePath**. La ruta de acceso a los medios de instalación de SQL. En este ejemplo, los medios de instalación de SQL se almacenan en `C:\SQL2017`. Un recurso compartido de red puede minimizar el espacio que se usa en el servidor.
- **SQLSysAdminAccounts**. Los usuarios o grupos que van a ser miembros del rol **sysadmin**. En este ejemplo, se concede acceso **sysadmin** al grupo local Administradores. 

> [!NOTE]
> No se recomienda esta configuración en un entorno de alta seguridad.

Hay una lista completa y una descripción de los parámetros disponibles en **SqlSetup** en el [repositorio SqlServerDsc de GitHub](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup).

El recurso **SqlSetup** solo instala SQL Server y **no** conserva la configuración aplicada. Un ejemplo es si se especifican **SQLSysAdminAccounts** en tiempo de instalación. Es posible que un administrador agregue inicios de sesión al rol **sysadmin** o los quite de él. Pero el recurso **SqlSetup** no se verá afectado. Si quiere que DSC exija la pertenencia del rol **sysadmin**, use el recurso [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole).

#### <a name="finish-configuration"></a>Finalización de la configuración

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>Compilar e implementar

### <a name="compile-the-configuration"></a>Compilar la configuración

Use el operador punto con el script de configuración:

```PowerShell
. .\SQLInstallConfiguration.ps1
```

Ejecute la función de configuración:

```PowerShell
SQLInstall
```

Se crea un directorio llamado **SQLInstall** en el directorio de trabajo. Contiene un archivo denominado **localhost.mof**. Examine el contenido del archivo MOF, que muestra la configuración de DSC compilada.

### <a name="deploy-the-configuration"></a>Implementar la configuración

Para iniciar la implementación de DSC de SQL Server, llame al cmdlet **Start-DscConfiguration**. Se proporcionan los parámetros siguientes al cmdlet:

- **Path**. La ruta de acceso a la carpeta que contiene los documentos MOF que se van a implementar. Un ejemplo es `C:\SQLInstall`.
- **Wait**. La espera hasta que finaliza el trabajo configuración.
- **Force**. La invalidación de cualquier configuración de DSC existente.
- **Verbose**. Se muestra la salida detallada. Resulta útil al insertar una configuración por primera vez para ayudar a solucionar problemas.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

Al aplicar la configuración, en la salida detallada se muestra lo que sucede. Siempre y cuando no se produzca ningún error (texto de color rojo), cuando aparezca **Operation "Invoke CimMethod" complete** (Se ha completado la operación "Invocar método de CIM") en la pantalla, SQL Server se habrá instalado.

## <a name="validate-installation"></a>Validar la instalación

### <a name="dsc"></a>DSC

Los cmdlets [Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) pueden determinar si el estado actual del servidor cumple el estado deseado. En este caso, es la instalación de SQL Server. El resultado de **Test-DscConfiguration** debe ser **True**:

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>Services

Ahora en la lista de servicios se devuelven los servicios de SQL Server:

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>Vea también

[Información general sobre la configuración de estado deseado de Windows PowerShell](https://docs.microsoft.com/powershell/dsc/overview)

[Instalación de SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[Instalación de SQL Server mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
