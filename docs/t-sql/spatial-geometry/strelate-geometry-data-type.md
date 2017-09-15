---
title: STRelate (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 68978595626be0dae1c81c5dbc1f1187dbed6d5f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="strelate-geometry-data-type"></a>STRelate (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve 1 si una **geometry** está relacionada con otra instancia **geometry** instancia, donde la relación está definida por un valor de matriz de patrones de Dimensionally Extended 9 Intersection Model (DE-9IM); en caso contrario , devuelve 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 Es otra **geometry** instancia va a comparar con la instancia en la que `STRelate()` se invoca.  
  
 *intersection_pattern_matrix*  
 Es una cadena de tipo **nchar(9)** codifica valores aceptables para el dispositivo de matriz de patrones DE-9IM entre los dos **geometry** instancias.  
  
## <a name="remarks"></a>Comentarios  
 Este método siempre devuelve null si los identificadores de referencia espacial (SRID) de la **geometry** instancias no coinciden. Este método producirá una **ArgumentException** si la matriz no está bien formada.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **bits**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `STRelate()` para comprobar si dos **geometry** instancias para espacial separado utilizando un patrón DE-9IM explícito.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de Geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
