---
title: STAsText (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 57eb5c213761b0161f0fd38bc0f25cfc2374aae1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="stastext-geography-data-type"></a>STAsText (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de **geography**. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de valor devuelto de CLR: **SqlChars**  
  
## <a name="remarks"></a>Notas  
 El tipo OGC de una instancia de **geography** se puede determinar mediante la invocación de [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el conjunto de resultados posibles devuelto en el servidor se ha ampliado a las instancias de **FullGlobe**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STAsText()` para crear una instancia de `LineString``geography` de (-122.360, 47.656) a (-122.343, 47.656) a partir de texto. A continuación, devuelve el resultado en forma de texto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
