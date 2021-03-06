---
title: Compatibilidad con versiones anteriores de Analysis Services de SQL Server de 2017 | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7dc1581fd2940ec5bad7698985eeab2c8ed96b2c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Compatibilidad con versiones anteriores de Analysis Services (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Este artículo describe los cambios en la disponibilidad de las características y el comportamiento entre la versión actual y la versión anterior.

## <a name="deprecated-features"></a>Características desusadas
A *característica en desuso* se interrumpirá del producto en una versión futura, pero todavía admitido e incluido en la versión actual para mantener la compatibilidad con versiones anteriores. Se recomienda que suspender el uso de características en desuso en proyectos nuevos y existentes para mantener la compatibilidad con futuras versiones.

Las siguientes características están en desuso en esta versión:
  
|||  
|-|-|  
|**Modo/categoría**|**Característica**|
|Multidimensional|Minería de datos|
|Multidimensional|Grupos de medida vinculados remotos|
|Tabular|Modelos en el nivel de compatibilidad 1100 y 1103|
|Tabular|Propiedades del modelo de objetos tabulares: Column.TableDetailPosition, Column.IsDefaultLabel, Column.IsDefaultImage|
|Herramientas|SQL Server Profiler para captura de seguimiento<br /><br /> La sustitución es usar el Generador de perfiles de eventos extendidos integrado en SQL Server Management Studio.  <br /> Consulte [Supervisar Analysis Services con SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Herramientas|Server Profiler para reproducción de seguimiento <br />Sustitución. No hay ninguna sustitución.|  
|Objetos de administración de seguimiento y API de seguimiento|Objetos de Microsoft.AnalysisServices.Trace (contiene las API para los objetos Trace y Replay de Analysis Services). La sustitución abarca varias partes:<br /><br /> -Configuración de seguimiento: Microsoft.SqlServer.Management.XEvent<br />: Hacer seguimiento de lectura: Microsoft.SqlServer.XEvent.Linq<br />- Reproducción de seguimiento: ninguna|  


## <a name="discontinued-features"></a>Características no incluidas
A *no incluye la característica* ha quedado obsoleta en la versión anterior. Puede continuar para incluirse en la versión actual, pero ya no se admite. Se pueden quitar características no incluidas en una futura versión completamente o actualizar.

Las siguientes características están en desuso en la versión anterior y ya no se admiten en esta versión.
  
|||  
|-|-|  
|**Modo/categoría**|**Característica**|  
|Tabular|Valor de propiedad de memoria de VertipaqPagingPolicy (2), habilitar la paginación en el disco mediante memoria archivos asignados.|
|Multidimensional|Particiones remotas|  
|Multidimensional|Grupos de medida vinculados remotos|  
|Multidimensional|Reescritura de dimensiones|  
|Multidimensional|Dimensiones vinculadas|


## <a name="breaking-changes"></a>Cambios importantes
A *cambio problemático* hace una característica, el modelo de datos, el código de aplicación o el script ya no funcione después de actualizar a la versión actual.

No hay ningún cambio importante en esta versión.

## <a name="behavior-changes"></a>Cambios de comportamiento
A *cambio de comportamiento* afecta al funcionamiento de la misma función en la versión actual en comparación con la versión anterior. Se describen sólo los cambios de comportamiento importante. No se incluyen cambios en la interfaz de usuario.

Cambios en MDSCHEMA_MEASUREGROUP_DIMENSIONS y DISCOVER_CALC_DEPENDENCY, que se detallan en el [cuáles son las novedades de CTP de SQL Server de 2017 2.1 para Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) anuncio.


## <a name="see-also"></a>Vea también
[Compatibilidad con versiones anteriores de Analysis Services (SQL Server 2016)](analysis-services-backward-compatibility.md)
