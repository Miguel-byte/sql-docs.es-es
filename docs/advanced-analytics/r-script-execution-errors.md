---
title: Errores y solución de problemas de scripting de R
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 10ec78bf8627bfef3232dfc72d7ef7f638604b15
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715755"
---
# <a name="r-scripting-errors-in-sql-server"></a>Errores de scripting de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se documentan varios errores de scripting cuando se ejecuta código R en SQL Server. La lista no es completa. Hay muchos paquetes y los errores pueden variar entre las distintas versiones del mismo paquete. Se recomienda publicar los errores de script en el [Foro de machine learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), que admite los componentes de aprendizaje automático que se usan en R Services (en bases de datos), Microsoft R Client y Microsoft R Server.

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>Error de script válido en T-SQL o en procedimientos almacenados

Antes de ajustar el código R en un procedimiento almacenado, es una buena idea ejecutar el código R en un IDE externo o en una de las herramientas de R, como RTerm o RGui. Mediante el uso de estos métodos, puede probar y depurar el código mediante los mensajes de error detallados devueltos por R.

Sin embargo, a veces es posible que el código que funciona perfectamente en un IDE o una utilidad externos no se ejecute en un procedimiento almacenado o en un contexto de proceso de SQL Server. Si esto ocurre, hay una serie de problemas que hay que buscar antes de que pueda asumir que el paquete no funciona en SQL Server.

1. Compruebe si Launchpad se está ejecutando.

2. Revise los mensajes para ver si los datos de entrada o los datos de salida contienen columnas con tipos de datos incompatibles o no admitidos. Por ejemplo, las consultas en una base de datos SQL suelen devolver GUID o ROWGUID, y no se admiten. Para obtener más información, consulte [bibliotecas y tipos de datos de R](r/r-libraries-and-data-types.md).

3. Revise las páginas de ayuda de las funciones individuales de R para determinar si se admiten todos los parámetros para el contexto de proceso de SQL Server. Para obtener ayuda sobre ScaleR, use los comandos de ayuda de R en línea o consulte [referencia de paquete](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Si el tiempo de ejecución de R funciona pero el script devuelve errores, se recomienda que intente depurar el script en un entorno de desarrollo de R dedicado, como Herramientas de R para Visual Studio.

También se recomienda revisar y volver a escribir ligeramente el script para corregir cualquier problema con los tipos de datos que pueden surgir al trasladar datos entre R y el motor de base de datos. Para obtener más información, consulte [bibliotecas y tipos de datos de R](r/r-libraries-and-data-types.md).

Además, puede usar el paquete sqlrutils para empaquetar el script de R en un formato que se consuma más fácilmente como un procedimiento almacenado. Para obtener más información, vea:
* [paquete sqlrutils](r/ref-r-sqlrutils.md)
* [Crear un procedimiento almacenado mediante sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>El script devuelve resultados incoherentes

Los scripts de R pueden devolver valores diferentes en un contexto de SQL Server, por varias razones:

- La conversión de tipos implícita se realiza automáticamente en algunos tipos de datos, cuando los datos se pasan entre SQL Server y R. Para obtener más información, consulte [bibliotecas y tipos de datos de R](r/r-libraries-and-data-types.md).

- Determinar si el formato de bits es un factor. Por ejemplo, a menudo hay diferencias en los resultados de las operaciones matemáticas de las bibliotecas de punto flotante de 32 y 64 bits.

- Determine si se han producido Nan en cualquier operación. Esto puede invalidar los resultados.

- Se pueden amplificar pequeñas diferencias cuando se toma un valor recíproco de un número cerca de cero.

- Los errores de redondeo acumulados pueden provocar cosas como valores menores que cero en lugar de cero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticación implícita para la ejecución remota a través de ODBC

Si se conecta al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo para ejecutar comandos de R mediante las funciones **RevoScaleR** , podría recibir un error al utilizar llamadas ODBC que escriben datos en el servidor. Este error solo se produce cuando se usa la autenticación de Windows.

La razón es que las cuentas de trabajo que se crean para R Services no tienen permiso para conectarse al servidor. Por lo tanto, no se pueden ejecutar llamadas ODBC en su nombre. El problema no se produce con los inicios de sesión de SQL porque, con los inicios de sesión de SQL, las credenciales se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, a continuación, a ODBC. Sin embargo, el uso de inicios de sesión de SQL también es menos seguro que el uso de la autenticación de Windows.

Para permitir que las credenciales de Windows se pasen de forma segura desde un script que se inicia de forma remota, SQL Server debe emular las credenciales. Este proceso se denomina _autenticación implícita_. Para realizar este trabajo, las cuentas de trabajo que ejecutan scripts de R o Python en el equipo SQL Server deben tener los permisos correctos.

1. Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como administrador en la instancia de donde desea ejecutar el código de R.

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuarios, si ha cambiado el valor predeterminado, y los nombres de equipo y de instancia.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evitar borrar el área de trabajo mientras se ejecuta R en un contexto de proceso de SQL

Aunque es común borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias imprevistas en un contexto de cálculo de SQL.

`revoScriptConnection`es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde SQL Server. Sin embargo, si el código de R incluye un comando para borrar el área de `rm(list=ls())`trabajo (como), toda la información sobre la sesión y otros objetos en el área de trabajo de R también se borrará.

Como alternativa, evite el borrado indiscriminado de variables y otros objetos mientras ejecuta R en SQL Server. Puede eliminar variables específicas mediante la función **Remove** :

```R
remove('name1', 'name2', ...)
```

Si hay varias variables que eliminar, se recomienda guardar los nombres de las variables temporales en una lista y, a continuación, realizar las recolecciones de elementos no utilizados periódicas en la lista.



## <a name="next-steps"></a>Pasos siguientes

[Solución de problemas y problemas conocidos de Machine Learning Services](machine-learning-troubleshooting-faq.md)

[Recopilación de datos para la solución de problemas de machine learning](data-collection-ml-troubleshooting-process.md)

[Preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexiones del motor de base de datos](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
