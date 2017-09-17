---
title: "Descripciones de parámetros | Documentos de Microsoft"
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
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d78b3b7ac10fae37bb35f88cefaf5983e0df09a4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="describing-parameters"></a>Descripciones de parámetros
**SQLBindParameter** tiene argumentos que describen el parámetro: su tipo SQL, precisión y escala. El controlador utiliza esta información, o *metadatos,* para convertir el valor del parámetro en el tipo necesario por el origen de datos. A primera vista, podría parecer que el controlador está en una posición mejor saber los metadatos de parámetros de la aplicación; Después de todo, el controlador puede detectar fácilmente los metadatos para un resultado de conjunto de columnas. Como resultado, no es el caso. En primer lugar, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detectar los metadatos del parámetro. Segundo, la mayoría de las aplicaciones ya conocen los metadatos.  
  
 Si una instrucción SQL está codificado de forma rígida en la aplicación, el escritor de la aplicación ya conoce el tipo de cada parámetro. Si se construye una instrucción SQL por la aplicación en tiempo de ejecución, la aplicación puede determinar los metadatos cuando genera la instrucción. Por ejemplo, cuando la aplicación crea la cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 puede llamar a **SQLColumns** para la columna OrderID.  
  
 La única situación en la que la aplicación no puede determinar con facilidad los metadatos de parámetros es cuando el usuario escriba una instrucción con parámetros. En este caso, la aplicación llama **SQLPrepare** para preparar la instrucción **SQLNumParams** para determinar el número de parámetros, y **SQLDescribeParam** para describir cada parámetro. Sin embargo, tal y como se indicó anteriormente, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detectar los metadatos del parámetro, por lo que **SQLDescribeParam** no se admite ampliamente.