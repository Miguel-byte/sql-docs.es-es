---
title: SandDance para Azure Data Studio
titleSuffix: Azure Data Studio
description: Uso de SandDance en Azure Data Studio
ms.custom: seodec18
ms.date: 07/03/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e6576d383011a47eb963774f2834a854dec4416e
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212326"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para Azure Data Studio, versión preliminar
Azure Data Studio ahora ofrece una forma de crear visualizaciones rápidas de los datos. Esta extensión es útil cuando se intenta examinar los datos y comprender lo que sucede. Usamos una tecnología denominada SandDance de Microsoft Research, que puede generar visualizaciones en contexto de los datos.

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Con vistas fáciles de entender, SandDance le ayuda a extraer información sobre los datos, lo que, a su vez, le ayuda a crear un relato a partir de esos datos, crear casos basados en la evidencia, probar hipótesis, profundizar en las explicaciones superficiales, apoyar las decisiones de compras o poner en relación los datos con un contexto más amplio del mundo real.

SandDance usa visualizaciones unitarias que aplican una asignación individual entre las filas de la base de datos, con marcas en la pantalla.
Las transiciones animadas y fluidas entre vistas ayudan a mantener el contexto mientras se interactúa con los datos.

## <a name="usage"></a>Uso

### <a name="view-csv-or-tsv-files"></a>Visualización de archivos .csv o .tsv
Esto incluye archivos locales o archivos en HDFS en el clúster de macrodatos de SQL Server 2019.
 
A partir del menú Archivo, use Abrir carpeta o [CTRL+K Ctrl+O] para abrir el directorio que contiene el archivo .csv.  Después, en el panel del explorador, haga clic con el botón derecho en el archivo .csv o .tsv y seleccione *View in SandDance* (Ver en SandDance).

Haga clic con el botón derecho en un archivo .csv o .tsv en HDFS si está conectado al clúster de macrodatos de SQL Server 2019 y seleccione *View in SandDance* (Ver en SandDance).

### <a name="view-sql-query-results"></a>Visualización de resultados de consultas SQL

Desde una ventana de consulta SQL, ejecute una consulta para obtener una cuadrícula de resultados. Haga clic en el icono del visualizador situado en el lado derecho del panel de resultados.

## <a name="known-issues"></a>Problemas conocidos

En este momento, no se delimita el número de filas que se visualizan. Sin embargo, el consumo de memoria aumenta proporcionalmente al número de filas, por lo que se recomienda que el conjunto de datos o la vista se limiten a unas 100 000 filas.

Vea [Problemas conocidos](https://microsoft.github.io/SandDance/#known-issues).

## <a name="release-notes"></a>Notas de la versión

### <a name="100"></a>1.0.0

Versión inicial de azdata-sanddance

## <a name="next-steps"></a>Next Steps
Para obtener más información, [visite el repositorio de GitHub](https://github.com/Microsoft/SandDance).
