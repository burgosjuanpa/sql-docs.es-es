---
title: Campo (ADO - sintaxis WFC) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b355a11d2916403c7574c547aac02c61d7b0d71
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="field-ado---wfc-syntax"></a>Campo (ADO - sintaxis WFC)
## <a name="package-commswfcdata"></a>paquete com.ms.wfc.data  
  
### <a name="methods"></a>Métodos  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>Propiedades  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (Para obtener más información, consulte la documentación para la interfaz com.ms.wfc.data.IDataFormat.)  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>Métodos de descriptor de acceso de campo  
 El [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad de un [campo](../../../ado/reference/ado-api/field-object.md) objeto Obtiene o establece el contenido de ese objeto. El contenido se representa como una variante, un tipo de objeto que se puede asignar un valor y cualquiera de varios tipos de datos.  
  
 ADO/WFC implementa la **valor** propiedad con el **getValue** método, que devuelve un objeto VARIANT; y la **setValue** método, que toma una variante como argumento. Los tipos Variant son muy eficaces en algunos lenguajes, como Microsoft Visual Basic.  
  
 Además el **valor** propiedad ADO/WFC proporciona *descriptor de acceso* métodos que usan tipos de datos de Java para obtener y establecer el contenido de **campo** objetos. La mayoría de estos métodos tiene nombres de la forma **obtener *** DataType* o **establecer *** DataType*.  
  
 Existen dos excepciones notables: uno de los **getObject** métodos devuelve un objeto convertido en una clase especificada. No hay ningún **getNull** propiedad; en su lugar, hay una **isNull** propiedad que devuelve un valor booleano que indica si el campo es null.  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
