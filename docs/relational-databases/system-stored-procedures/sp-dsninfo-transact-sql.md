---
title: sp_dsninfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5a9c04611a342f81b6aa0a0b403eb6ff4ce8a643
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información del origen de datos ODBC u OLE DB tomada del distribuidor asociado con el servidor actual. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dsn =**] **'***dsn***'**  
 Es el nombre del DSN ODBC o del servidor vinculado OLE DB. *DSN* es **varchar (128)**, no tiene ningún valor predeterminado.  
  
 [  **@infotype =**] **'***tipo_de_info***'**  
 Es el tipo de información que se va a devolver. Si *tipo_de_info* no se especifica o si se especifica NULL, se devuelven todos los tipos de información. *tipo_de_info* es **varchar (128)**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**DBMS_NAME**|Especifica el nombre del proveedor del origen de datos.|  
|**DBMS_VERSION**|Especifica la versión del origen de datos.|  
|**DATABASE_NAME**|Especifica el nombre de la base de datos.|  
|**O SQL_SUBSCRIBER**|Especifica que el origen de datos puede ser un suscriptor.|  
  
 [  **@login =**] **'***inicio de sesión***'**  
 Es el nombre de inicio de sesión del origen de datos. Si el origen de datos incluye un inicio de sesión, especifique NULL u omita el parámetro. *inicio de sesión*es **varchar (128)**, su valor predeterminado es null.  
  
 [  **@password =**] **'***contraseña***'**  
 Es la contraseña del inicio de sesión. Si el origen de datos incluye un inicio de sesión, especifique NULL u omita el parámetro. *contraseña*es **varchar (128)**, su valor predeterminado es null.  
  
 [  **@dso_type=**] *dso_type*  
 Es el tipo del origen de datos. *dso_type* es **int**, y puede tener uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Origen de datos ODBC|  
|**3**|Origen de datos OLE DB|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Tipo de información**|**nvarchar(64)**|Tipos de información, como DBMS_NAME, DBMS_VERSION, DATABASE_NAME o SQL_SUBSCRIBER.|  
|**Valor**|**nvarchar(512)**|Valor del tipo de información asociado.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_dsninfo** se utiliza en todos los tipos de replicación.  
  
 **sp_dsninfo** recupera ODBC u OLE DB información de origen de datos que muestra si la base de datos puede utilizarse para la replicación o la consulta.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_dsninfo**.  
  
## <a name="see-also"></a>Vea también  
 [sp_enumdsn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
