---
title: Con servicios de componentes de Microsoft | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: addf942a3813c1be918720756954eab14f6bc274
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-component-services"></a>Uso de servicios de componentes de Microsoft
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Puede habilitar una base de datos de Oracle trabajar con servicios de componentes (o MTS, si está utilizando Windows NT) transaccional en Microsoft Windows NT o Windows 2000 y Microsoft Windows 95 o Windows 98. Para habilitar una base de datos de Oracle trabajar con servicios de componentes que admiten transacciones, los administradores del sistema deben crear una vista denominada V$ XATRANS$. Para crear esta secuencia de comandos, debe ejecutar un script proporcionado por Oracle. Para obtener más información, consulte la Ayuda de servicios de componente o la documentación de Oracle.