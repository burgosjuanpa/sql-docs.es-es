---
title: Sys.trigger_event_types (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trigger_event_types_TSQL
- sys.trigger_event_types_TSQL
- sys.trigger_event_types
- trigger_event_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_event_types catalog view
ms.assetid: 054aed54-7151-4760-934a-149fa434f1ae
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e2b9d5f6df14e02395ea204f7037d2324a0f936b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="systriggereventtypes-transact-sql"></a>sys.trigger_event_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada evento o grupo de eventos en el que se puede activar un desencadenador.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Tipo**|**int**|Tipo de evento o grupo de eventos que provoca la activación de un desencadenador.|  
|**type_name**|**nvarchar(64)**|Nombre de un evento o grupo de eventos. Esto se puede especificar en la cláusula FOR de una [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) instrucción.|  
|**parent_type**|**int**|Tipo de grupo de eventos que es el elemento primario del evento o grupo de eventos.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
