---
title: IsSibling (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ISSIBLING
dev_langs:
- kbMDX
helpviewer_keywords:
- IsSibling function
ms.assetid: 12f302f0-141e-4ec0-ad5f-329aade17a4d
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bf72e1e366edd280abec3a250ff5d68c408e9909
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="issibling-mdx"></a>IsSibling (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Informa de si un miembro especificado está en el mismo nivel que otro miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression1*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Member_Expression2*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **IsSibling** función devuelve **true** si el primer miembro especificado está en un elemento relacionado del segundo miembro especificado. En caso contrario, la función devuelve **false**.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo devuelve TRUE si el miembro actual en la jerarquía Fiscal de la dimensión Date es un elemento relacionado de julio 2002:  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
