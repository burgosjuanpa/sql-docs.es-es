---
title: Cómo editar las propiedades de la instancia de CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a480e8353f501e7bd1ba7ff86df25e5ec736469
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>Cómo editar las propiedades de la instancia CDC
  En este procedimiento se describe cómo usar la Consola del diseñador CDC para editar las propiedades de configuración de una instancia CDC.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>Para editar las propiedades de configuración de la instancia CDC  
  
1.  En el menú **Inicio** , seleccione **Consola del diseñador CDC**.  
  
2.  En el panel izquierdo, expanda **Captura de datos modificados** y expanda después el servicio que contiene la instancia cuyas propiedades desea editar.  
  
3.  Seleccione el nombre de la instancia cuyas propiedades desea editar.  
  
4.  En el panel Acciones situado en el lado derecho de la Consola del diseñador CDC, haga clic en **Propiedades**.  
  
     También puede hacer clic con el botón derecho en la instancia cuyas propiedades quiere editar y luego hacer clic en **Propiedades**.  
  
5.  En el editor de propiedades, edite las propiedades en las pestañas siguientes:  
  
    -   **Oracle**: use la pestaña **Oracle** del editor de propiedades para realizar cambios en la descripción que proporcionó en la página Crear base de datos CDC del Asistente para nueva instancia y para realizar cambios en la información de conexión a bases de datos de Oracle Log Mining.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
    -   **Tablas**: use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
    -   **Scripts**: use la pestaña **Scripts** para ejecutar o volver a ejecutar un script en la base de datos de origen de Oracle que configurará el registro complementario.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Review and Generate Supplemental Logging Scripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Avanzadas**: use la pestaña **Avanzadas** para agregar propiedades especiales a la instancia CDC.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
  
