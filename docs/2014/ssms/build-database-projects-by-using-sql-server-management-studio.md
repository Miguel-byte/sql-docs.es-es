---
title: Generar proyectos de bases de datos mediante SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 134ac290601e463063f78a59ea8fd5923d095663
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211264"
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>Generar proyectos de bases de datos mediante SQL Server Management Studio
  Un proyecto de scripts de base de datos es un conjunto organizado de scripts, información de conexión y plantillas asociado a una base de datos o a parte de ella. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrar y diseñar bases de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el contexto de un proyecto de script. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] incluye diseñadores, editores, guías y asistentes para ayudar a los usuarios a desarrollar, implementar y mantener bases de datos.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es un conjunto de herramientas administrativas que permite administrar los componentes que pertenecen a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Este entorno integrado permite a los usuarios realizar varias tareas, como realizar copias de seguridad de los datos, editar consultas y automatizar funciones comunes en una misma interfaz.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] incluye las siguientes herramientas:  
  
-   El Editor de código es un editor de script completo que sirve para escribir y modificar scripts. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] proporciona cuatro versiones del Editor de código: el Editor de consultas del [!INCLUDE[ssDE](../includes/ssde-md.md)] para scripts [!INCLUDE[tsql](../includes/tsql-md.md)] , el Editor de consultas de MDX, el Editor de consultas de MDX y el Editor de consultas de XML/A.  
  
-   El Explorador de objetos sirve para buscar, modificar e incluir en scripts objetos que pertenecen a instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]o ejecutarlos.  
  
-   El Explorador de plantillas sirve para buscar plantillas y crear scripts para ellas.  
  
-   El Explorador de soluciones sirve para organizar y almacenar scripts relacionados como partes de un proyecto.  
  
-   La Ventana Propiedades sirve para mostrar las propiedades actuales de los objetos seleccionados.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite desarrollar procesos de trabajo de manera eficaz al proporcionar:  
  
-   Acceso sin conexión. Puede escribir y modificar scripts sin conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Creación de scripts desde cualquier cuadro de diálogo. Puede crear un script desde cualquier cuadro de diálogo para que pueda leer, modificar, almacenar y reutilizar los scripts después de crearlos.  
  
-   Cuadros de diálogo no modales. Al obtener acceso a un cuadro de diálogo de interfaz de usuario, puede examinar otros recursos en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sin cerrar el cuadro de diálogo.  
  
## <a name="solutions-and-script-projects"></a>Soluciones y proyectos de scripts  
 El Explorador de soluciones es una utilidad que sirve para almacenar y volver a abrir soluciones de bases de datos. Las soluciones organizan proyectos de scripts y archivos relacionados. Los proyectos de script almacenan archivos de scripts de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , plantillas SQL, información de conexión y otros archivos varios. Cuando se guarda un script en un proyecto de scripts, los usuarios pueden:  
  
-   Mantener un control de versiones de los scripts.  
  
-   Almacenar opciones de resultados con un script.  
  
-   Organizar los scripts relacionados en un solo proyecto de script.  
  
-   Guardar información de conexión con scripts.  
  
 El Explorador de soluciones es una herramienta para los programadores que crean y reutilizan scripts relacionados con el mismo proyecto. Si se requiere realizar una tarea similar posteriormente, puede utilizar el grupo de scripts que se almacenó en un proyecto. Si creó aplicaciones mediante [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], el Explorador de soluciones le resultará muy familiar.  
  
 Una solución consta de uno o más proyectos de script. Un proyecto está formado por uno o más scripts o conexiones. Un proyecto también puede incluir archivos que no sean scripts.  
  
## <a name="see-also"></a>Vea también  
 [Usar SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Soluciones &#40;SQL Server Management Studio&#41;](solution/solutions-sql-server-management-studio.md)  
  
  
