---
title: _ (comodín, coincidir un carácter) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb82b8abe1b5a7d37fc74945dfc82ccce1882740
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (comodín, coincidir un carácter) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Use el carácter de subrayado _ para hacer coincidir todos los caracteres de una operación de comparación de cadenas que implica una coincidencia de patrón como `LIKE` y `PATINDEX`.  
  
## <a name="examples"></a>Ejemplos  

## <a name="a-simple-example"></a>A: Ejemplo sencillo   

En el ejemplo siguiente se devuelven todos los nombres de base de datos que comienzan por la letra `m` y tienen `d` como la tercera letra. El carácter de subrayado especifica que el segundo carácter del nombre puede ser cualquier letra. Las bases de datos `model` y `msdb` cumplen este criterio. La base de datos `master` no lo cumple.

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
Puede tener bases de datos adicionales que cumplan este criterio.

Puede usar varios caracteres de subrayado para representar varios caracteres. Al cambiar el criterio `LIKE` para incluir dos caracteres de subrayado `'m__%` se incluye la base de datos maestra en el resultado.

### <a name="b-more-complex-example"></a>B: ejemplo más complejo
 En el siguiente ejemplo se usa el operador _ para buscar todas las personas de la tabla `Person` con un nombre de tres letras que termina en `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: escape del carácter de subrayado   
En el ejemplo siguiente se devuelven los nombres de los roles fijos de base de datos como `db_owner` y `db_ddladmin`, pero también se devuelve el usuario `dbo`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

El carácter de subrayado en la tercera posición de carácter se toma como un carácter comodín y no filtra solo las entidades de seguridad que empiezan con las letras `db_`. Para incluir el carácter de subrayado entre secuencias de escape, inclúyalo entre corchetes `[_]`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Ahora se excluye el usuario `dbo`.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Ver también  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (caracteres comodín para coincidencia)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (caracteres comodín para coincidencia)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (caracteres comodín para no coincidir)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
