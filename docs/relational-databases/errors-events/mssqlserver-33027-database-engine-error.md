---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 71600394f3d89883414dd6ae8f7a34494ad3d173
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33027|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto del mensaje|No se pudo cargar el proveedor de servicios criptográficos '%.*ls' debido a una firma Authenticode o una ruta de archivo no válida. Revise los mensajes de otros errores anteriores.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha podido utilizar el proveedor de servicios criptográficos enumerado en el mensaje de error porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha podido cargar la DLL. O el nombre no es válido o la firma Authenticode no es válida.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que el archivo está presente y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene permiso de acceso a esa ubicación. Compruebe el registro de errores para ver posibles mensajes relacionados adicionales. De lo contrario, póngase en contacto con el proveedor de servicios criptográficos para obtener más información.  
  
