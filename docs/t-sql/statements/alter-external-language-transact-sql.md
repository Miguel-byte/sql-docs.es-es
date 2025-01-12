---
title: ALTER EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5a503c77b49b8e57139ded0b29873fc18cd2b342
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893733"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Modifica el contenido de una extensión de lenguaje externo existente en la base de datos.

## <a name="syntax"></a>Sintaxis

```text
ALTER EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]
{
    SET <file_spec>
    | ADD <file_spec>
    | REMOVE <file_spec>
}
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = {<external_lang_specifier> | <content_bits>,
    FILE_NAME = <external_lang_file_name>
    [, PLATFORM = <platform> ]
    [, PARAMETERS = <external_lang_parameters> ]
    [, ENVIRONMENT_VARIABLES = <external_lang_env_variables> ] )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
   | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'

<platform> :: =
{
   WINDOWS
  | LINUX
}

< external_lang_parameters > :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>Argumentos

**language_name**

Los lenguajes son objetos del ámbito de la base de datos. Los nombres del lenguaje deben ser únicos en la base de datos.

**owner_name**

Especifica el nombre del usuario o rol que es propietario del lenguaje externo. Si no se especifica, la propiedad se otorga al usuario actual. Dependiendo de los permisos, puede ser que haya que conceder permisos explícitos a otros usuarios para ejecutar scripts mediante un lenguaje específico.

**file_spec**

Especifica el contenido de la extensión del lenguaje. Solo se permite un argumento filespec para un lenguaje específico por plataforma. 

**external_lang_specifier**

La ruta de acceso completa al archivo .zip o tar.gz que contiene el código de las extensiones. Este contenido puede ser una ruta de acceso a un archivo .zip (en Windows) o tar.gz (en Linux).

**content_bits**

Especifica el contenido del lenguaje como un literal hexadecimal, similar a los ensamblados.
Esta opción es útil si necesita crear un lenguaje o modificar uno ya existente (y tiene los permisos necesarios para hacerlo), pero el sistema de archivos en el servidor está restringido y no puede copiar los archivos de la biblioteca en una ubicación a la que pueda tener acceso el servidor.

**external_lang_file_name**

Nombre del archivo con extensión .dll o .so. Es necesario para identificar el archivo correcto en casos donde hay varios archivos .dll o .so en el <external_lang_specifier> .zip o tar.gz.

**external_lang_parameters**

Proporciona la posibilidad de conceder un conjunto de parámetros al tiempo de ejecución del lenguaje externo. Los valores de los parámetros se proporcionan para el tiempo de ejecución externo una vez iniciado el proceso externo. Sin embargo, la extensión del lenguaje puede acceder a las variables de entorno antes del inicio del proceso externo.

**external_lang_env_variables**

Proporciona la posibilidad de conceder un conjunto de variables de entorno al tiempo de ejecución del lenguaje externo antes del inicio del proceso externo. Un ejemplo de una variable de entorno sería, por ejemplo, el directorio principal del mismo tiempo de ejecución. Por ejemplo: JRE_HOME.

**platform**

Este parámetro es necesario para escenarios de sistemas operativos híbridos. En una arquitectura híbrida, el lenguaje debe registrarse una vez por cada plataforma. El nombre de la plataforma y del lenguaje será la clave única por el lenguaje externo. Si no se especifica ninguna plataforma, se usará el sistema operativo actual.

## <a name="remarks"></a>Notas

En CTP 3.0, no se admite **PARAMETERS** ni **ENVIRONMENT_VARIABLES**.

## <a name="permissions"></a>Permisos

Requiere el permiso `ALTER ANY EXTERNAL LANGUAGE`. De forma predeterminada, cualquier usuario que tenga **dbo** y sea miembro del rol **db_owner** tiene permisos para modificar un lenguaje externo. Para todos los demás usuarios, debe concederles explícitamente permiso con una instrucción [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) y especificando ALTER ANY EXTERNAL LANGUAGE como privilegio.

## <a name="examples"></a>Ejemplos

### <a name="alter-an-external-language-in-a-database"></a>Modificar un lenguaje externo en una base de datos  

En el ejemplo siguiente se agrega un lenguaje externo denominada Java a una base de datos de SQL Server en Windows.

```sql
ALTER EXTERNAL LANGUAGE Java 
SET (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

## <a name="see-also"></a>Vea también

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
