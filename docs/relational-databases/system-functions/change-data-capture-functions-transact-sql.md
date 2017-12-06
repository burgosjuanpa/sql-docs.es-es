---
title: Cambiar las funciones de captura de datos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: change data capture [SQL Server], functions
ms.assetid: e5270557-aca3-44ab-8715-daccd498b88d
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2b21d8191c7c16b62fca2b9c670cd06daae241bb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="change-data-capture-functions-transact-sql"></a>Funciones de captura de datos modificados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El mecanismo de captura de datos modificados registra las operaciones de inserción, actualización y eliminación aplicadas sobre las tablas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proporcionando los detalles de los cambios en un formato relacional de fácil uso. Para las filas modificadas, se captura la información de columna que duplica la estructura de las columnas de una tabla de origen sometida a seguimiento, junto con los metadatos necesarios para aplicar los cambios a un entorno de destino. Las siguientes funciones se usan para devolver información acerca de los cambios.  
  
|||  
|-|-|  
|[CDC.fn_cdc_get_all_changes_ &#60; capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)|[Sys.fn_cdc_has_column_changed &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)|  
|[CDC.fn_cdc_get_net_changes_ &#60; capture_instance &#62; &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)|[Sys.fn_cdc_increment_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)|  
|[Sys.fn_cdc_decrement_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)|[Sys.fn_cdc_is_bit_set &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)|  
|[Sys.fn_cdc_get_column_ordinal &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)|[Sys.fn_cdc_map_lsn_to_time &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)|  
|[Sys.fn_cdc_get_max_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)|[Sys.fn_cdc_map_time_to_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)|  
|[Sys.fn_cdc_get_min_lsn &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)||  
  
## <a name="see-also"></a>Vea también  
 [Tablas de captura de datos de cambio &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)   
 [Procedimientos almacenados de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  