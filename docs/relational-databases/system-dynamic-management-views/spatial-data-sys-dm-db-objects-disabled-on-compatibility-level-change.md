---
title: sys.dm_db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30c3a5d7358e49c1e1762fbb9851066bdaf30871
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809901"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>Datos espaciales: sys. DM _ _db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Muestra los índices y las restricciones que se deshabilitarán como resultado de cambiar el nivel de compatibilidad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los índices y las restricciones que contienen columnas calculadas persistentes cuyas expresiones usan UDT espaciales se deshabilitarán después de actualizar o cambiar el nivel de compatibilidad. Use esta función de administración dinámica para determinar el impacto de un cambio en el nivel de compatibilidad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> Argumentos  
 *compatibility_level*  
 **entero** que identifica el nivel de compatibilidad que se va a establecer.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**class**|**int**|1 = restricciones<br /><br /> 7 = índices y montones|  
|**class_desc**|**nvarchar(60)**|OBJECT o COLUMN para restricciones<br /><br /> INDEX para índices y montones|  
|**major_id**|**int**|OBJECT ID de restricciones<br /><br /> OBJECT ID de la tabla que contiene índices y montones|  
|**minor_id**|**int**|NULL para restricciones<br /><br /> Index_id para índices y montones|  
|**pendiente**|**nvarchar(60)**|Descripción de la dependencia que está haciendo que se deshabilite la restricción o el índice. Los mismos valores también se usan en las advertencias que se producen durante la actualización. Entre otros, se incluyen los siguientes ejemplos:<br /><br /> “space” para intrínseca<br /><br /> “geometry” para UDT del sistema<br /><br /> "geography::Parse" para un método de UDT del sistema|  
  
## <a name="general-remarks"></a>Notas generales  
 Las columnas calculadas persistentes que usan algunas funciones intrínsecas se deshabilitan cuando se cambia el nivel de compatibilidad. Además, las columnas calculadas persistentes que emplean cualquier método Geometry o Geography se deshabilitan cuando se actualiza una base de datos.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>¿Qué funciones hacen que se deshabiliten las columnas calculadas persistentes?  
 Cuando las siguientes funciones se usan en la expresión de una columna calculada persistente, hacen que los índices y las restricciones que hacen referencia a esas columnas se deshabiliten cuando el nivel de compatibilidad se cambie entre 80 y 90:  
  
-   **IsNumeric**  
  
 Cuando las siguientes funciones se usan en la expresión de una columna calculada persistente, hacen que los índices y las restricciones que hacen referencia a esas columnas se deshabiliten cuando el nivel de compatibilidad se cambie entre 100 y 110 o superior:  
  
-   **Soundex**  
  
-   **Geografía:: GeomFromGML**  
  
-   **Geografía:: STGeomFromText**  
  
-   **Geografía:: STLineFromText**  
  
-   **Geografía:: STPolyFromText**  
  
-   **Geografía:: STMPointFromText**  
  
-   **Geografía:: STMLineFromText**  
  
-   **Geografía:: STMPolyFromText**  
  
-   **Geografía:: STGeomCollFromText**  
  
-   **Geografía:: STGeomFromWKB**  
  
-   **Geografía:: STLineFromWKB**  
  
-   **Geografía:: STPolyFromWKB**  
  
-   **Geografía:: STMPointFromWKB**  
  
-   **Geografía:: STMLineFromWKB**  
  
-   **Geografía:: STMPolyFromWKB**  
  
-   **Geografía:: STUnion**  
  
-   **Geografía:: STIntersection**  
  
-   **Geografía:: STDifference**  
  
-   **Geografía:: STSymDifference**  
  
-   **Geografía:: STBuffer**  
  
-   **Geografía:: BufferWithTolerance**  
  
-   **Geografía:: Analiza**  
  
-   **Geografía:: Reducen**  
  
### <a name="behavior-of-the-disabled-objects"></a>Comportamiento de los objetos deshabilitados  
 **Índices**  
  
 Si el índice clúster está deshabilitado, o si se fuerza un índice no clúster, se produce el siguiente error: "El procesador de consultas no puede producir un plan porque el índice '%. \*ls ' en la tabla o vista '%. \*ls ' está deshabilitado ". Para volver a habilitar estos objetos, vuelva a generar los índices después de la **actualización llamando a Alter index on... REBUILD**.  
  
 **Montones**  
  
 Si se usa una tabla con un montón deshabilitado, se produce el siguiente error. Para volver a habilitar estos objetos, vuelva a generar después de **la actualización llamando a Alter index All on... REBUILD**.  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 Si intenta volver a generar el montón durante una operación en línea, se produce un error.  
  
 **Restricciones check y claves externas**  
  
 Las restricciones CHECK y las claves externas deshabilitadas no generan ningún error. Sin embargo, las restricciones no se aplican cuando se modifican las filas. Para volver a habilitar estos objetos, compruebe las restricciones después de la actualización mediante una llamada **a ALTER TABLE... RESTRICCIÓN**CHECK.  
  
 **Columnas calculadas persistentes**  
  
 Puesto que no es posible deshabilitar una sola columna, se deshabilita toda la tabla al deshabilitar el índice clúster o el montón.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una consulta en **Sys. DM _ _db_objects_disabled_on_compatibility_level_change** para buscar los objetos afectados por el cambio del nivel de compatibilidad a 120.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
