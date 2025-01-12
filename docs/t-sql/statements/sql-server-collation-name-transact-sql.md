---
title: Nombre de intercalación de SQL Server (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e867584c9c9a0e50022d0964a1772ac2c3a1b1e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099983"
---
# <a name="sql-server-collation-name-transact-sql"></a>Nombre de intercalación de SQL Server (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Es una cadena que especifica el nombre de intercalación de una intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite intercalaciones de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admite un número limitado (<80) de las intercalaciones denominadas intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se desarrollaron antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitiera intercalaciones de Windows. Las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se siguen admitiendo por compatibilidad con versiones anteriores, pero no se deben utilizar en nuevos trabajos de desarrollo. Para obtener más información sobre la intercalación de Windows, consulte [Nombre de intercalación de Windows](../../t-sql/statements/windows-collation-name-transact-sql.md).

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxis

```
<SQL_collation_name> :: =
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>

<ComparisonStyle> ::=
_CaseSensitivity_AccentSensitivity | _BIN
```

## <a name="arguments"></a>Argumentos

*SortRules* Cadena que identifica el alfabeto o el idioma cuyas reglas de ordenación se aplican cuando se especifica el orden del diccionario. Por ejemplo: Latin1_General o Polish.

**Pref** Especifica la preferencia de mayúsculas. Aunque la comparación distinga entre mayúsculas y minúsculas, la versión en mayúsculas de una letra se ordena antes que la versión en minúsculas, cuando no existe ningún otro tipo de diferenciación.

*Codepage* Especifica un número de uno a cuatro dígitos que identifica la página de códigos que la intercalación utiliza. **CP1** especifica la página de códigos 1252; en los demás casos se especifica el número de página de códigos completo. Por ejemplo, **CP1251** especifica la página de códigos 1251 y **CP850** especifica la página de códigos 850.

*CaseSensitivity*
**CI** especifica que no se diferencia mayúsculas de minúsculas, **CS** especifica que se diferencia mayúsculas de minúsculas.

*AccentSensitivity*
**AI** especifica que no se distinguen acentos, **AS** especifica que se distinguen acentos.

**BIN** Especifica el criterio de ordenación binario que se va a utilizar.

## <a name="remarks"></a>Notas

Para enumerar las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitidas por el servidor, ejecute la consulta siguiente.

```sql
SELECT * FROM sys.fn_helpcollations()
WHERE name LIKE 'SQL%';
```

> [!NOTE]
> Para el identificador de criterio de ordenación 80, utilice cualquiera de las intercalaciones de Windows con la página de códigos 1250 y orden binario. Por ejemplo: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.

## <a name="see-also"></a>Consulte también

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [Constantes](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [table](../../t-sql/data-types/table-transact-sql.md)
- [sys.fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
