---
title: Administración de la finalización mediante tabulador (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec946a26c898c4ed66bd60e1ad71e69c008766df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922956"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>Administrar la finalización mediante tabulador (SQL Server PowerShell)
  Los complementos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell presentan tres variables (`$SqlServerMaximumTabCompletion`, `$SqlServerMaximumChildItems` y `$SqlServerIncludeSystemObjects`) para controlar la finalización mediante el tabulador de Windows PowerShell. La finalización mediante el tabulador reduce la cantidad de texto que se debe escribir al devolver las tablas de elementos cuyos nombres empiezan por la cadena que está escribiendo.  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Con la finalización mediante el tabulador de PowerShell, cuando se ha escrito parte de una ruta de acceso o nombre de cmdlet, se puede presionar la tecla Tab para obtener una lista de los elementos cuyos nombres coincidan con lo que ya se ha escrito. Se puede seleccionar a continuación el elemento que desee en la lista sin tener que escribir el resto del nombre.  
  
 Si está trabajando en una base de datos que tiene muchos objetos, las listas para finalización mediante tabulador pueden llegar a ser muy grandes. Algunos tipos de objeto de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como las vistas, también tienen una gran cantidad de objetos de sistema.  
  
 Los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] presentan tres variables del sistema que se pueden usar para controlar la cantidad de información presentada por la finalización mediante tabulador y **Get-ChildItem**.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Especifica el número máximo de objetos que se incluyen en una lista de finalización mediante tabulador. Si selecciona Tab en un nodo de ruta de acceso que tiene más de *n* objetos, la lista de finalización mediante tabulador se trunca en *n*. *n* es un entero. El valor predeterminado es 0, es decir, no hay límite para el número de objetos que se muestran.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Especifica el número máximo de objetos mostrados por **Get-ChildItem**. Si se ejecuta **Get-ChildItem** en un nodo de ruta de acceso que tiene más de *n* objetos, la lista se trunca en *n*. *n* es un entero. El valor predeterminado es 0, es decir, no hay límite para el número de objetos que se muestran.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** |  **$False** }  
 Si es **$True**, los objetos del sistema se muestran con finalización mediante tabulador y **Get-ChildItem**. Si es **$False**, no se muestran objetos del sistema. El valor de configuración predeterminado es **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Establecer las variables de finalización mediante tabulador de SQL Server  
 Para cualquiera de las variables a las que desee cambiar el valor predeterminado, establezca la variable en el nuevo valor.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el ejemplo siguiente se establecen las tres variables y se enumeran sus valores:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
