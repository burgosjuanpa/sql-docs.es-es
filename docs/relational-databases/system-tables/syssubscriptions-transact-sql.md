---
title: syssubscriptions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 620cc0de62221ad784c4e38dbf51aba39eea5047
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada suscripción de la base de datos. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Id. único de un artículo.|  
|**srvid**|**smallint**|Id. de servidor del suscriptor.|  
|**dest_db**|**sysname**|El nombre de la base de datos de destino.|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo.<br /><br /> **1** = suscrito.<br /><br /> **2** = activo.|  
|**sync_type**|**tinyint**|El tipo de sincronización inicial:<br /><br /> **1** = automático.<br /><br /> **2** = ninguno|  
|**login_name**|**sysname**|El nombre de inicio de sesión utilizado al agregar la suscripción.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> 0 = Inserción. El agente de distribución se ejecuta en el distribuidor.<br /><br /> 1 = Extracción. El agente de distribución se ejecuta en el suscriptor.|  
|**distribution_jobid**|**binary (16)**|Id. de trabajo del Agente de distribución.|  
|**timestamp**|**timestamp**|Marca de tiempo.|  
|**update_mode**|**tinyint**|Modo de actualización:<br /><br /> **0** = solo lectura.<br /><br /> **1** = actualización inmediata.|  
|**loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **0** = las envía.<br /><br /> **1** = no no volver a enviar.|  
|**queued_reinit**|**bit**|Especifica si el artículo está marcado para inicialización o reinicialización. Un valor de **1** especifica que el artículo suscrito está marcado para inicialización o reinicialización.|  
|**nosync_type**|**tinyint**|Tipo de inicialización de la suscripción:<br /><br /> **0** = automático (instantánea)<br /><br /> **1** = solo admite replicación<br /><br /> **2** = inicializar con copia de seguridad<br /><br /> **3** = inicializar del número de secuencia de registro (LSN)<br /><br /> Para obtener más información, consulte el **@sync_type** parámetro de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).|  
|**SRVNAME**|**sysname**|Nombre del suscriptor.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
