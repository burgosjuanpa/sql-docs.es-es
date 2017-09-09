---
title: DROP EVENT NOTIFICATION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab32a9ffadce83635e8ef987607af913fe0f2472
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un desencadenador de notificación de eventos de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *notification_name*  
 Es el nombre de la notificación de eventos que se va a quitar. Se pueden especificar varias notificaciones de eventos. Para ver una lista de las notificaciones de eventos creadas actualmente, utilice [sys.event_notifications &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 Indica que el ámbito de la notificación de eventos se aplica al servidor actual. Se debe especificar SERVER si se especificó cuando se creó la notificación de eventos.  
  
 DATABASE  
 Indica que el ámbito de la notificación de eventos se aplica a la base de datos actual. Se debe especificar DATABASE si se especificó cuando se creó la notificación de eventos.  
  
 COLA *nombre_de_cola*  
 Indica el ámbito de la notificación de eventos se aplica a la cola especificada por *nombre_de_cola*. Se debe especificar QUEUE si se especificó cuando se creó la notificación de eventos. *nombre_de_cola* es el nombre de la cola y también debe especificarse.  
  
## <a name="remarks"></a>Comentarios  
 Si una notificación de eventos se activa y se quita en la misma transacción, la instancia de notificación de eventos se envía y después se quita la notificación de eventos.  
  
## <a name="permissions"></a>Permissions  
 Para quitar una notificación de eventos que pertenece al ámbito de la base de datos, como mínimo, un usuario debe ser el propietario de la notificación de eventos o tener el permiso ALTER ANY DATABASE EVENT NOTIFICATION en la base de datos actual.  
  
 Para quitar una notificación de eventos que pertenece al ámbito del servidor, como mínimo, un usuario debe ser el propietario de la notificación de eventos o tener el permiso ALTER ANY EVENT NOTIFICATION en el servidor.  
  
 Para quitar una notificación de eventos en una cola específica, como mínimo, un usuario debe ser el propietario de la notificación de eventos o tener el permiso ALTER en la cola primaria.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una notificación de eventos que pertenece al ámbito de la base de datos y después se elimina.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR la notificación de eventos &#40; Transact-SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sys.event_notifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [Sys.Events &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  