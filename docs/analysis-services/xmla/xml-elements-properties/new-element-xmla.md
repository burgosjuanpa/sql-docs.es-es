---
title: Nuevo elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: acb0043613c784b5677f3446beef22b6ecc12321
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="new-element-xmla"></a>Elemento New (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene la nueva ubicación de almacenamiento de sistema de archivos utilizada por un [carpeta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Carpeta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **New** elemento contiene una ruta de acceso UNC que reemplaza el valor de la **Original** elemento incluido en el elemento primario **carpeta** (elemento) para todos los objetos restaurados o sincronizados, respectivamente, durante un **restaurar** o **sincronizar** comando. El valor de la **Original** elemento se compara con el valor de la **StorageLocation** (elemento) para cada cubo, grupo de medida o partición y, si se encuentra una coincidencia, el valor de este elemento se utiliza para actualizar el **StorageLocation** del objeto durante la restauración o sincronización.  
  
 Para obtener más información acerca de la copia de seguridad y restauración de objetos, consulte [realizar copias de seguridad y restauración de objetos (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Original elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [Restaurar elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Storagelocation, elemento & #40; ASSL & #41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Sincronizar el elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
