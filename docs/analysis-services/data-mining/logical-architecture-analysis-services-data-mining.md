---
title: 'Arquitectura lógica (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7fa39b3e6e0bce7596ea38c6aa049fd7e942a08d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="logical-architecture-analysis-services---data-mining"></a>Arquitectura lógica (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La minería de datos es un proceso que implica la interacción de varios componentes.  
  
-   Puede tener acceso a orígenes de datos en una base de datos de SQL Server o cualquier otro origen de datos y usarlos para el entrenamiento, las pruebas o la predicción.  
  
-   Defina las estructuras y los modelos utilizando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o Visual Studio.  
  
-   Administre los objetos de minería de datos y cree predicciones y consultas mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Cuando la solución esté completa, puede implementarla en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 El proceso de creación de estos objetos de la solución se ha descrito previamente en otro lugar. Para obtener más información, vea [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
 En las secciones siguientes se describe la arquitectura lógica de los objetos de una solución de minería de datos.  
  
 [Datos de origen de la minería de datos](#bkmk_SourceData)  
  
 [Estructuras de minería de datos](#bkmk_Structures)  
  
 [Modelos de minería de datos](#bkmk_Models)  
  
 [Objetos de minería de datos personalizados](#bkmk_CustomObjects)  
  
##  <a name="bkmk_SourceData"></a> Datos de origen de la minería de datos  
 Los datos que se usan en la minería de datos no se almacenan en la solución de minería de datos; solo se almacenan los enlaces. Los datos podrían residir en una base de datos creada en una versión anterior de SQL Server, en un sistema CRM o incluso en un archivo plano. Cuando se entrena la estructura o el modelo mediante un proceso, se crea un resumen estadístico de los datos y se almacena en una memoria caché que puede conservarse para usarse en operaciones posteriores, o puede eliminarse después del procesamiento. Para obtener más información, vea [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 Combine datos dispares dentro del objeto de vista del origen de datos (DSV) de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], que proporciona una capa de abstracción sobre el origen de datos. También puede especificar combinaciones entre tablas o agregar tablas que tengan una relación de varios a uno para crear columnas de tabla anidadas. La definición de estos objetos, el origen de datos y la vista del origen de datos se almacenan en la solución con las extensiones de nombre de archivo *.ds y \*.dsv. Para obtener más información sobre cómo crear y usar orígenes de datos y vistas del origen del datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 También puede definir y modificar orígenes de datos y vistas del origen de datos utilizando AMO o XMLA. Para obtener más información sobre cómo trabajar con estos objetos mediante programación, vea [Información general de arquitectura lógica &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md).  
  
  
##  <a name="bkmk_Structures"></a> Mining Structures  
 Una estructura de minería de datos es un contenedor de datos lógico que define el dominio de datos a partir del cual se generan los modelos de minería de datos. Una sola estructura de minería de datos puede admitir varios modelos de minería de datos.  
  
 Cuando tenga que usar los datos en la solución de minería de datos, Analysis Services leerá los datos del origen y genera una memoria caché de agregados y otra información. De forma predeterminada, esta memoria caché se mantiene para poder reutilizar datos de entrenamiento y admitir modelos adicionales. Si necesita eliminar la memoria caché, cambie la propiedad **CacheMode** en el objeto de estructura de minería de datos por el valor **ClearAfterProcessing**. Para obtener más información, vea [Clases de minería de datos de AMO](../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md).  
  
 Analysis Services también proporciona la capacidad de separar los datos en conjuntos de datos, aprendizaje y prueba para que pueda probar sus modelos de minería de datos en un conjunto de datos representativo y seleccionado de forma aleatoria. Los datos no se almacenan en realidad por separado; en su lugar, los datos de caso de la memoria caché de la estructura se marcan con una propiedad que indica si ese caso se utiliza para el entrenamiento o para las pruebas. Si la memoria caché se elimina, esta información no se puede recuperar.  
  
 Para obtener más información, vea [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 Una estructura de minería de datos puede contener tablas anidadas. Una tabla anidada proporciona detalles adicionales sobre el caso que se modela en la tabla de datos principal. Para más información, vea [Tablas anidadas &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
  
##  <a name="bkmk_Models"></a> Mining Models  
 Antes del procesamiento un modelo de minería de datos solo es una combinación de propiedades de metadatos. Estas propiedades especifican una estructura de minería de datos, especifican un algoritmo de minería de datos y definen una colección de parámetros y configuraciones de filtro que afectan al modo en que se procesan los datos. Para obtener más información, vea [Modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md).  
  
 Al procesar el modelo, los datos de entrenamiento que se almacenan en la memoria caché de la estructura de minería de datos se utilizan para generar los patrones, según las propiedades estadísticas de los datos y la heurística definida por el algoritmo y sus parámetros. Esto se conoce como *entrenar* el modelo.  
  
 El resultado del entrenamiento es un conjunto de datos de resumen, contenido en el *contenido del modelo*, que describe los patrones encontrados y proporciona las reglas con las que generar predicciones. Para obtener más información, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 En escenarios limitados, la estructura lógica del modelo también se puede exportar a un archivo que representa las fórmulas y los enlaces de datos según un formato estándar, el lenguaje de marcado de modelado de predicción (PMML). Esta estructura lógica se puede importar en otros sistemas que utilizan PMML y el modelo así descrito puede utilizarse entonces para la predicción. Para obtener más información, vea [Descripción de la instrucción Select de DMX](../../dmx/understanding-the-dmx-select-statement.md).  
  
  
##  <a name="bkmk_CustomObjects"></a> Objetos de minería de datos personalizados  
 Otros objetos que se usan en el contexto de un proyecto de minería de datos, como los gráficos de precisión o las consultas de predicción, no se conservan en la solución, pero se pueden incluir en un script mediante ASSL o se pueden generar con AMO.  
  
 Además, puede ampliar los servicios y las características disponibles en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregando estos objetos personalizados:  
  
 **Ensamblados personalizados**  
 Los ensamblados .NET pueden definirse mediante cualquier idioma compatible con COM o CLR y, a continuación registrarse con una instancia de SQL Server. Los archivos de ensamblado se cargan desde la ubicación definida por la aplicación ; en el servidor se guarda una copia junto con los datos. La copia del archivo de ensamblado se usa para cargar el ensamblado cada vez que se inicia el servicio.  
  
 Para obtener más información, vea [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 **Procedimientos almacenados personalizados**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] minería de datos admite el uso de procedimientos almacenados para trabajar con objetos de minería de datos. Puede crear sus propios procedimientos almacenados para ampliar la funcionalidad y trabajar más fácilmente con los datos devueltos por las consultas de predicción y las consultas de contenido.  
  
 [Definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 Los procedimientos almacenados siguientes pueden usarse al realizar la validación cruzada.  
  
 [Procedimientos almacenados de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)  
  
 Además, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene muchos procedimientos almacenados del sistema que se usan internamente para la minería de datos. Aunque los procedimientos almacenados del sistema son para uso interno, es posible le resulten útiles. Microsoft se reserva el derecho de cambiar estos procedimientos almacenados según sea necesario; por consiguiente, para utilizarlos en producción, se recomienda crear consultas con DMX, AMO o XMLA.  
  
 **Crear algoritmos de complemento**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Proporciona un mecanismo para crear sus propios algoritmos y, a continuación, agregar los algoritmos como un nuevo servicio de minería de datos a la instancia del servidor.  
  
 Analysis Services utiliza las interfaces COM para comunicarse con los algoritmos de complemento. Para obtener más información sobre cómo implementar nuevos algoritmos, vea [Plugin Algorithms](../../analysis-services/data-mining/plugin-algorithms.md).  
  
 Debe registrar cada nuevo algoritmo para poder usarlo. Para registrar un algoritmo, agregue los metadatos requeridos para los algoritmos en el archivo .ini de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Debe agregar la información a cada instancia donde piense utilizar el nuevo algoritmo. Después de agregar el algoritmo, puede reiniciar la instancia y utilizar el conjunto de filas de esquema MINING_SERVICES para ver el nuevo algoritmo, incluidas las opciones y los proveedores que el algoritmo admite.  
  
  
## <a name="see-also"></a>Vea también  
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Extensiones de minería de datos & #40; DMX & #41; Referencia](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
