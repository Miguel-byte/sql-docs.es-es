---
title: Adición de funcionalidad adicional a través de la extensibilidad
titleSuffix: Azure Data Studio
description: Más información sobre el modelo de extensibilidad y las áreas de extensibilidad clave para extender la funcionalidad de Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20158894567c1452a8d605f5cec84354654c5e96
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959598"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>Introducción a la extensibilidad de [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos.md)] cuenta con varios mecanismos de extensibilidad para personalizar la experiencia del usuario y poner dichas personalizaciones a disposición de toda la comunidad de usuarios. La plataforma [!INCLUDE[name-sos](../includes/name-sos.md)] principal se basa en Visual Studio Code, por lo que la mayoría de las API de extensibilidad de Visual Studio Code están disponibles. Además, hemos facilitado otros puntos de extensibilidad para actividades específicas de la administración de datos.

Algunos de los principales puntos de extensibilidad son:

- API de extensibilidad de Visual Studio Code
- Herramientas de creación de extensiones de Azure Data Studio
- Administración de contribuciones del panel de pestañas Panel
- Información con experiencias de acciones
- API de extensibilidad de Azure Data Studio
- API del proveedor de datos personalizado

## <a name="visual-studio-code-extensibility-apis"></a>API de extensibilidad de Visual Studio Code

Dado que la plataforma [!INCLUDE[name-sos](../includes/name-sos.md)] principal se basa en Visual Studio Code, los detalles sobre las API de extensibilidad de Visual Studio Code se encuentran en la documentación sobre [creación de extensiones](https://code.visualstudio.com/docs/extensions/overview) y la [API de extensión](https://code.visualstudio.com/docs/extensionAPI/overview) en el sitio web de Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Administración de contribuciones del panel de pestañas Panel

Para obtener más información, consulte [Puntos de contribución](#contribution-points) y [Variables de contexto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>API de extensibilidad de Azure Data Studio

Para obtener más información, consulte [API de extensibilidad](extensibility-apis.md).


## <a name="contribution-points"></a>Puntos de contribución

En esta sección se tratan los distintos puntos de contribución que se definen en el manifiesto de la extensión package.json.

IntelliSense se admite en azuredatastudio.

## <a name="contributes-dashboard"></a>Panel de contribuciones

Pestaña Contribuir, contenedor, widget de información en el panel.

![Panel](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs crea las secciones de pestañas en la página del panel. Espera un objeto o una matriz de objetos.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

En lugar de especificar el contenedor del panel insertado (en dashboard.tab), puede registrar contenedores con dashboard.containers. Acepta un objeto o una matriz del objeto.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

Para hacer referencia al contenedor registrado, especifique el identificador del contenedor.

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

Puede registrar información con dashboard.insights. Es similar a lo que se indica en [Tutorial: Compilación de un widget de información personalizada](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>Tipos de contenedor del panel

Actualmente hay cuatro tipos de contenedor admitidos:

1. `widgets-container`

    ![Contenedor de widgets](media/extensibility/widgets-container.png)

    Lista de los widgets que se mostrarán en el contenedor. Es un diseño de flujo. Acepta la lista de widgets.

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![Contenedor de vistas web](media/extensibility/webview-container.png)

    La vista web se mostrará en todo el contenedor. Espera que el identificador de vista web sea igual al identificador de pestaña.

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![Contenedor de cuadrícula](media/extensibility/grid-container.png)

   Lista de los widgets o vistas web que se mostrarán en el contenedor

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![Sección de navegación](media/extensibility/nav-section.png)

    La sección de navegación se mostrará en el contenedor

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>Variables de contexto

Para obtener información general sobre el contexto en Visual Studio Code y posteriormente en Azure Data Studio, consulte el artículo sobre [extensibilidad](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

En Azure Data Studio, tenemos un contexto específico en torno a las conexiones de base de datos disponibles para las extensiones.

### <a name="dashboard"></a>Panel

En el panel, se proporcionan las siguientes variables de contexto:

|variable de contexto| description|
|:---|:---|
|`connectionProvider` | Cadena del identificador del proveedor de la conexión actual. Por ejemplo, Columnas en la tabla de origen capturadas`connectionProvider == 'MSSQL'`|
|`serverName`|Cadena del nombre de servidor de la conexión actual. Por ejemplo, Columnas en la tabla de origen capturadas`serverName == 'localhost'`|
|`databaseName` | Cadena del nombre de base de datos de la conexión actual. Por ejemplo, Columnas en la tabla de origen capturadas`databaseName == 'master'`|
|`connection` | Objeto de perfil de conexión completo de la conexión actual (IConnectionProfile).|
|`dashboardContext` | Una cadena del contexto de la página del panel está actualmente activada. "database" o "server". Por ejemplo, `dashboardContext == 'database'`|
