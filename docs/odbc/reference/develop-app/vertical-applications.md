---
title: Las aplicaciones verticales | Documentos de Microsoft
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
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f71f960043a843c2aad5f7e3a7eb5cc997b0a6ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="vertical-applications"></a>Aplicaciones verticales
Aplicaciones verticales suelen realizan una tarea bien definida en un DBMS único. Por ejemplo, una aplicación de entrada de pedidos realiza un seguimiento de los pedidos de una empresa. Lo que estos tipos de aplicaciones tienen en común es que el esquema de base de datos normalmente se diseña el desarrollador de aplicaciones y, mientras que la aplicación puede funcionar con un número de diferentes DBMS, funciona con un DBMS único para un único cliente.  
  
 Debido a las aplicaciones verticales suelen requieran cierta funcionalidad, como cursores desplazables o de las transacciones, rara vez admiten todos los DBMS. En su lugar, tienden a ser muy interoperable entre un conjunto limitado de DBMS. Por lo general, los desarrolladores de aplicaciones vertical eligen admitir los DBMS que representan una gran parte del mercado y pasar por alto el resto. Incluso puede optar por la compatibilidad de controladores específicos para los DBMS para reducir las pruebas y los costes de soporte de producto.  
  
 Dado que las aplicaciones verticales pueden admitir un conjunto conocido de DBMS, a veces contienen código específico del controlador o específicos del DBMS. Sin embargo, este código es mejor guardar en un mínimo porque requiere tiempo adicional para mantener.
