---
title: Preparado (propiedad, ADO) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a5f02d8c1536192832622e26fa4e128a7c04c66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="prepared-property-ado"></a>Propiedad Prepared (ADO)
Indica si se debe guardar una versión compilada de un [comando](../../../ado/reference/ado-api/command-object-ado.md) antes de la ejecución.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **booleano** valor que, si se establece en **True**, indica que el comando debe estar preparado.  
  
## <a name="remarks"></a>Comentarios  
 Use la **Prepared** propiedad para que el proveedor guarde una versión preparada (o compilada) de la consulta especificada en el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad antes de un [comando](../../../ado/reference/ado-api/command-object-ado.md) del objeto primera ejecución. Esto puede ralentizar la primera ejecución de un comando, pero una vez que el proveedor compila un comando, el proveedor utilizará la versión compilada del comando para las ejecuciones posteriores, lo que dará como resultado un mejor rendimiento.  
  
 Si la propiedad es **False**, el proveedor ejecutará el **comando** objeto directamente, sin necesidad de crear una versión compilada.  
  
 Si el proveedor no admite la preparación de comandos, puede devolver un error cuando se establece esta propiedad en **True**. Si el proveedor no devolvió un error, simplemente omite la solicitud para preparar el comando y establece la **Prepared** propiedad **False**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad preparada (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Ejemplo de la propiedad Prepared (VC ++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
