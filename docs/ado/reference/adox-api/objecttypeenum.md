---
title: ObjectTypeEnum | Documentos de Microsoft
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
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3654a63d4fc327a2fd3ea6d8ff60c59fba75404
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Especifica el tipo de objeto de base de datos para el que se establecerán permisos o propiedad.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|El objeto es una columna.|  
|**adPermObjDatabase**|3|El objeto es una base de datos.|  
|**adPermObjProcedure**|4|El objeto es un procedimiento.|  
|**adPermObjProviderSpecific**|-1|El objeto es un tipo definido por el proveedor. Se producirá un error si la *ObjectType* parámetro es **adPermObjProviderSpecific** y *valor de ObjectTypeId* no se proporciona.|  
|**adPermObjTable**|1|El objeto es una tabla.|  
|**adPermObjView**|5|El objeto es una vista.|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[GetObjectOwner (método, ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions (método, ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
