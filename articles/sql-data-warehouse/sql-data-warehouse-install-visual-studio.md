---
title: Instalación de Visual Studio y SSDT para SQL Data Warehouse | Microsoft Docs
description: Instalación de herramientas de desarrollo de Visual Studio y SQL Server Data Tools (SSDT) para Azure SQL Data Warehouse
services: sql-data-warehouse
ms.custom: vs-azure
ms.workload: azure-vs
author: KavithaJonnakuti
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.subservice: consume
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: e27a3d4f2fe4b8421b637e485d77d6376d15bf9a
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2019
ms.locfileid: "55461498"
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Instalación de Visual Studio y SSDT para SQL Data Warehouse
Si desea desarrollar aplicaciones para SQL Data Warehouse, se recomienda usar la versión más reciente de Visual Studio, junto con la última versión de SQL Server Data Tools (SSDT).  También se admite Visual Studio 2013 Update 5 con SSDT por compatibilidad con versiones anteriores.  

Con Visual Studio con SSDT puede usar el Explorador de objetos de SQL Server para explorar visualmente tablas, vistas, procedimientos almacenados y muchos más objetos en su instancia de SQL Data Warehouse, así como para ejecutar consultas.

> [!NOTE]
> SQL Data Warehouse no es compatible aún con proyectos de base de datos de Visual Studio. Para recibir actualizaciones periódicas sobre esta característica, vote en [UserVoice].
> 
> 

## <a name="step-1-install-visual-studio"></a>Paso 1: Instalación de Visual Studio
Siga estos vínculos para descargar e instalar Visual Studio. Si ya tiene Visual Studio 2013 o una versión posterior instalada, vaya directamente al paso 2 para instalar SSDT.

1. [Descarga de Visual Studio][].
2. Siga la guía [Instalar Visual Studio][Installing Visual Studio] en MSDN y elija las configuraciones predeterminadas.

## <a name="step-2-install-ssdt"></a>Paso 2: Instalar SSDT
Para instalar SSDT para Visual Studio, primero busque una actualización de SSDT desde dentro de Visual Studio siguiendo estos pasos.

1. En Visual Studio, haga clic en **Herramientas** / **Extensiones y actualizaciones...** / **Actualizaciones**
2. Seleccione **Actualizaciones de productos** y busque la actualización **Microsoft SQL Server Update para herramientas de base de datos**.

Si no hay ninguna actualización, debería tener la última versión instalada.  Para confirmar que SSDT está instalado, haga clic en **Ayuda** / **Acerca de Microsoft Visual Studio** y busque SQL Server Data Tools en la lista. La versión más reciente de SSDT es 14.0.60525.0. Si la opción para instalar no está disponible en Visual Studio, también puede visitar la página [Descargar las últimas herramientas de datos SQL Server][SSDT Download] para descargar e instalar SSDT manualmente.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene la versión más reciente de SSDT, ya puede [conectarse][connect] a su instancia de SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Descarga de Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
