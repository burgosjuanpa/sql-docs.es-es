---
title: PH timeout (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: affca4b8aff839831848c726cd99b060d6d4539e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ph-timeout-server-configuration-option"></a>PH timeout (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción ph timeout para especificar el tiempo, en segundos, que el controlador de protocolo de texto completo debe esperar para conectarse a una base de datos antes de que se agote el tiempo de espera. El valor predeterminado es 60 segundos. Aumente el valor de ph timeout cuando se esté agotando el tiempo de espera de los intentos de conexión debido a problemas de red temporales.  
  
 El controlador de protocolo de texto completo se aloja en el host de demonio de filtro y se utiliza para capturar de SQL Server los datos cuyo índice de texto completo se va a crear. Para obtener más información sobre los componentes de búsqueda de texto completo, vea [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md).  
  
 Al intentar capturar una fila de datos, si el controlador de protocolo no puede conectar con SQL Server dentro del tiempo especificado, notifica un error de tiempo de espera para esa fila. El recopilador de texto completo lo volverá a intentar más tarde. Para obtener más información sobre el recopilador de texto completo, vea [Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="see-also"></a>Ver también  
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
