---
title: Método setBinaryStream (SQLServerBlob) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c32868257eeebc4cfc24945d853e1440e34ee78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setbinarystream-method-sqlserverblob"></a>Método setBinaryStream (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un flujo que se puede utilizar para escribir en el valor BLOB.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición en el valor BLOB donde se comienza a escribir.  
  
## <a name="return-value"></a>Valor devuelto  
 Un flujo de salida.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método setBinaryStream especificado por el método setBinaryStream en la interfaz java.sql.Blob.  
  
 El flujo de salida sobrescribe los datos en el objeto BLOB a partir de la posición especificada y puede exceder la longitud inicial del BLOB. Si se especifica un 1 valor, se anexarán bytes. Si se pasan valores position+2 o superiores (o cero o menos), se producirá un error de la posición.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
