---
title: Columnas de la estructura de minería de datos | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cbdcd14127cdf45eb35dd7a24652be4f7c4d613
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="mining-structure-columns"></a>Columnas de la estructura de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Define las columnas de una estructura de minería de datos al crear dicha estructura eligiendo columnas de datos externos y especificando a continuación cómo se van a usar los datos para el modelado. Por tanto, las columnas de la estructura de minería de datos son más que copias de los datos de un origen de datos: definen cómo se van a usar los datos del origen en el modelo de minería de datos. Puede asignar propiedades que determinen cómo se discretizan los datos, las propiedades que describen cómo se distribuyen los valores de datos  
  
 Las columnas de la estructura de minería de datos se diseñan para ser flexibles y extensibles, porque cada algoritmo que se utilice para generar un modelo de minería de datos puede utilizar diferentes columnas de la estructura para interpretar los datos. En lugar de un conjunto de datos para cada modelo, puede utilizar una sola estructura de minería de datos y utilizar las columnas en ella para personalizar los datos de cada modelo.  
  
## <a name="defining-mining-structure-columns"></a>Definir columnas de la estructura de minería de datos  
 Los tipos de datos básicos y los tipos de contenido que definen las columnas de la estructura se derivan del origen de datos que se utiliza para crear la estructura. Puede cambiar esta configuración en la estructura de minería de datos; también puede establecer marcas de modelado y establecer la distribución de columnas continuas.  
  
 La definición de una columna de estructura de minería de datos debe contener la siguiente información:  
  
-   **Identificador**: nombre único de la columna, a menudo, el mismo que el nombre. Este dato no se puede cambiar después de crear la estructura de minería de datos, mientras que el nombre se puede cambiar.  
  
-   **Nombre**: nombre o alias de la columna.  
  
-   **Contenido**: enumeración que describe si los datos son discretos o continuos.  
  
-   **Tipo**: enumeración que indica el tipo de datos general.  
  
-   **Distribución**: enumeración que describe la distribución esperada de valores. Se incluye una distribución si la columna es continua.  
  
-   **Marcas de modelado**: enumeración que indica cómo tratar los valores que faltan y así sucesivamente. Las marcas de modelado también pueden definirse en el modelo de minería de datos, pero las marcas de modelo son diferentes de las marcas que se usan en las columnas de la estructura.  
  
-   **Enlaces**: propiedades que especifican que los datos de origen.  
  
 Los algoritmos de terceros también pueden incluir propiedades personalizadas que se pueden definir en la columna de la estructura de minería de datos.  
  
 Para más información sobre la estructura de minería de datos y el modelo de minería de datos, vea [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Vea los temas siguientes para obtener más información sobre cómo definir y usar las columnas de la estructura de minería de datos.  
  
|Tema|Vínculos|  
|-----------|-----------|  
|Describe los tipos de datos que se pueden utilizar para definir una columna de la estructura de minería de datos.|[Tipos de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-types-data-mining.md)|  
|Describe los tipos de contenido que están disponibles para cada tipo de datos contenido en una columna de estructura de minería de datos. Los tipos de contenido dependen del tipo de datos. El tipo de contenido se asigna en el modelo y determina cómo usa el modelo los datos de la columna.|[Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md)|  
|Presenta el concepto de tablas anidadas y explica el modo en que las tablas anidadas se pueden agregar al origen de datos como columnas de la estructura de minería de datos.|[Columnas clasificadas &#40;minería de datos&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md)|  
|Enumera y explica las propiedades de distribución que puede establecer en una columna de estructura de minería de datos para especificar la distribución esperada de valores de la columna.|[Distribuciones de columnas &#40;minería de datos&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md)|  
|Explica el concepto de *discretización* y describe métodos que proporciona Analysis Services para discretizar datos numéricos continuos.|[Métodos de discretización &#40;minería de datos&#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)|  
|Describe las marcas de modelado que se pueden establecer en una columna de la estructura de minería de datos.|[Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)|  
|Describe las columnas clasificadas, que son un tipo especial de columna que puede utilizar para relacionar una columna de la estructura de minería de datos con otra.|[Columnas clasificadas &#40;minería de datos&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md)|  
|Aprenda a agregar y modificar columnas de la estructura de minería de datos.|[Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>Vea también  
 [Estructuras de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md)  
  
  
