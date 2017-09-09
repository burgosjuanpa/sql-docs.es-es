---
title: COLA de destino (Transact-SQL) | Documentos de Microsoft
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
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51920e14a3a24f9bfb48f11c07414812da1694b9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una cola existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos que contiene la cola que se va a quitar. Si no *database_name* se proporciona, el valor predeterminado es la base de datos actual.  
  
 *schema_name (objeto)*  
 Nombre del esquema propietario de la cola que se va a quitar. Si no *schema_name* se proporciona, el valor predeterminado es el esquema predeterminado para el usuario actual.  
  
 *nombre_de_cola*  
 Nombre de la cola que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 No se puede quitar una cola si hay servicios que hacen referencia a ella.  
  
## <a name="permissions"></a>Permissions  
 Permiso para quitar una cola tiene como valor predeterminado el propietario de la cola, los miembros de la **db_ddladmin** o **db_owner** se han corregido los roles de base de datos y los miembros de la **sysadmin** fijo rol de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el **ExpenseQueue** cola de la base de datos actual.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  