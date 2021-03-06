---
title: Crear historial de informes (Reporting Services en el modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7154d4fc454861f3e0340c363d2a10e8cab1e1dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>Crear historial de informes (Reporting Services en el modo integrado de SharePoint)
  El historial de informes es un conjunto de instantáneas de informe que se crean a lo largo del tiempo. Cada instantánea es una copia del informe como existía cuando se creó. Incluye el diseño y los datos del informe cuando se creó la instantánea. La información de representación no está almacenada con la instantánea. Al abrir una instantánea en un historial de informes, se abre en un HTML en el elemento web Visor de informes. Una vez representada, puede exportarla a otros formatos de aplicación.  
  
 Para crear el historial de informes, el informe debe poder ejecutarse en modo desatendido (es decir, el servidor de informes debe ser capaz de ejecutar el informe sin la intervención del usuario). Debe tener el permiso Editar elementos en la biblioteca que contiene el informe. Para ver o eliminar el historial de informes, debe contar con los permisos Ver versiones o Eliminar versiones.  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>Crear una instantánea o historial de informes a petición  
  
1.  Elija el informe.  
  
2.  Haga clic para que se muestre la flecha abajo y, a continuación, seleccione **Ver historial de informes**.  
  
3.  Haga clic en **Nueva instantánea**. Si el botón no está visible, se debe a que no tiene permiso para crear instantáneas en el historial de informes.  
  
4.  Para ver la instantánea que acaba de crear, selecciónela en la lista. Cada instantánea se identifica mediante una marca de tiempo que muestra cuándo se creó la instantánea. No puede cambiar el nombre de una instantánea, ni moverla a otra ubicación ni modificarla.  
  
### <a name="to-schedule-report-history"></a>Para programar el historial de informes  
  
1.  Elija el informe.  
  
2.  Haga clic para que se muestre la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de instantáneas del historial**, haga clic en **Crear instantáneas del historial de informes según una programación**.  
  
4.  Si tiene una programación compartida que contiene la información de programación que desea usar, haga clic en **Según una programación compartida** y seleccione la programación que desee usar. De lo contrario, haga clic en **Según una programación personalizada**y, a continuación, haga clic en **Configurar** para especificar las opciones para crear el historial según una programación periódica.  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>Para crear el historial de informes cuando se actualizan los datos de un informe  
  
1.  Elija el informe.  
  
2.  Haga clic para que se muestre la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de instantáneas del historial**, haga clic en **Almacenar todas las instantáneas de datos de informe en el historial de informes**.  
  
## <a name="see-also"></a>Ver también  
 [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  
