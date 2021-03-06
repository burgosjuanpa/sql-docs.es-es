---
title: Proveedores necesarios para dar forma a datos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 049f635c9566a72bb84a7cef18aa62b80746c21b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="required-providers-for-data-shaping"></a>Proveedores deseados para dar forma a datos
Normalmente, la forma de datos requiere dos proveedores. El proveedor de servicios, [servicio de forma de datos para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), proporciona la funcionalidad y un proveedor de datos, como el proveedor OLE DB para SQL Server de forma de datos, proporciona filas de datos para rellenar la forma [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Se puede especificar el nombre del proveedor de servicios (MSDataShape) como el valor de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o la palabra clave de cadena de conexión "proveedor = MSDataShape;".  
  
 El nombre del proveedor de datos se puede especificar como el valor de la **proveedor de datos** propiedad dinámica, que se agrega a la **conexión** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección por el servicio de forma de datos de OLE DB o la palabra clave de cadena de conexión "**proveedor de datos = *** proveedor*".  
  
 Ningún proveedor de datos es necesaria si la **Recordset** no incluirá ningún dato (por ejemplo, al igual que en un fabricadas **Recordset** donde las columnas se crean con la palabra clave NEW). En ese caso, especifique "**proveedor de datos =** none;".  
  
## <a name="example"></a>Ejemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
