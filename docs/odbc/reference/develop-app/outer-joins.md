---
title: Combinaciones externas | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15ab82f5623bad7d3c82729dfd9077ac967301e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="outer-joins"></a>Combinaciones externas
ODBC admite el SQL-92 dejado, sintaxis de combinación externa completa y derecho. Es la secuencia de escape para las combinaciones externas  
  
 **{oj** *outer-join ***}**  
  
 donde *combinación externa* es  
  
 *referencia de tabla* {**izquierda &#124; derecha &#124; completa} OUTER JOIN** {*referencia de tabla* &#124; *combinación externa*} **ON**  *condición de búsqueda*  
  
 *referencia de tabla* especifica un nombre de tabla y *condición de búsqueda* especifica la condición de combinación entre la *referencias de tabla*.  
  
 Una solicitud de combinación externa debe aparecer después de la **FROM** palabra clave y antes de la **donde** cláusula (si existe). Para obtener información de la sintaxis completa, consulte [secuencia de Escape de combinación externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) en Apéndice C: SQL gramática.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados que muestra a todos los clientes e indica que tiene pedidos abiertos. La primera instrucción utiliza la sintaxis de la secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Oracle y no es interoperable.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar los tipos de combinaciones externas que admiten un origen de datos y el controlador, una aplicación llama **SQLGetInfo** con el SQL_OJ_CAPABILITIES indicador. Los tipos de combinaciones externas que podrían ser compatibles son izquierdos, derecha, completo o combinaciones externas; anidadas combinaciones externas en que los nombres de columna en la **ON** cláusula no tiene el mismo orden que sus nombres de tabla correspondiente en el **OUTER JOIN** cláusula; las combinaciones internas junto con las combinaciones externas; y combinaciones externas mediante cualquier operador de comparación ODBC. Si el tipo de información de SQL_OJ_CAPABILITIES devuelve 0, no se admite ninguna cláusula de combinación externa.
