---
title: Varios hstmts (controlador de Paradox) | Documentos de Microsoft
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
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 244df409b4706d60c78d37318d3c0fd21a716e10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="multiple-hstmts-paradox-driver"></a>Varios hstmts (controlador de Paradox)
Cuando se utiliza el controlador ODBC Paradox, si desea usar más de una *hstmt* para ejecutar consultas en una tabla, la tabla debe tener un índice único (clave principal Paradox).
