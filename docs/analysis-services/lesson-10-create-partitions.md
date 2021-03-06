---
title: 'Lección 11: Crear particiones | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d738649ea357b172975505ff7993b56181ce0b4f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-10-create-partitions"></a>Lección 10: Crear particiones
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, va a crear particiones dividir la tabla FactInternetSales en piezas lógicas más pequeñas que se pueden procesar (actualiza) independientemente de otras particiones. De forma predeterminada, cada tabla que incluye en el modelo tiene una partición que incluye todas las columnas y filas de la tabla. Para la tabla FactInternetSales, queremos dividir los datos por año; una partición para cada uno de los cinco años de la tabla. Cada partición se podrá procesar entonces independientemente. Para obtener más información, consulte [Particiones](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 9: crear jerarquías](../analysis-services/lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Crear particiones  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Para crear particiones en la tabla FactInternetSales  
  
1.  En el Explorador de modelos tabulares, expanda **tablas**, haga clic en **FactInternetSales** > **particiones**.  
  
2.  En el cuadro de diálogo Administrador de particiones, haga clic en **copia**.  
  
3.  En **nombre de la partición**, cambie el nombre a **FactInternetSales2010**.  
  
    > [!TIP]  
    > Observe que los nombres de columna en la ventana de vista previa de tabla se muestran las columnas incluidas en la tabla del modelo (activada) con los nombres de columna del origen. Esto es porque la ventana Vista previa de la tabla muestra las columnas de la tabla de origen, no de la tabla del modelo.  
  
4.  Seleccione el **SQL** situado sobre el lado derecho de la ventana de vista previa para abrir el editor de la instrucción SQL.  
  
    Como desea que la partición solo incluya las filas de un determinado período, debe incluir una cláusula WHERE. Solo puede crear una cláusula WHERE usando una instrucción SQL.  
  
5.  En el **instrucción SQL** , a continuación, reemplace la instrucción existente copiando y pegando la instrucción siguiente:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Esta instrucción especifica que la partición debe incluir todos los datos de las filas en las que OrderDate corresponda al año del calendario 2010, tal y como se especifica en la cláusula WHERE.  
  
6.  Haga clic en **Validar**.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Para crear una partición para el año 2011  
  
1.  En la lista de particiones, haga clic en el **FactInternetSales2010** de partición que acaba de crear y, a continuación, haga clic en **copia**.  
  
2.  En **nombre de la partición**, tipo **FactInternetSales2011**.  
  
3.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2011, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>Para crear una partición para el año 2012  
  
- Siga los pasos anteriores, utilizando la siguiente cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>Para crear una partición para el año 2013  
  
- Siga los pasos anteriores, utilizando la siguiente cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>Para crear una partición para el año 2014  
  
- Siga los pasos anteriores, utilizando la siguiente cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>Eliminar la partición FactInternetSales
Ahora que tiene particiones para cada año, puede eliminar la partición FactInternetSales. Esto evita que se superponen al elegir todos los procesos cuando el procesamiento de particiones.
#### <a name="to-delete-the-factinternetsales-partition"></a>Para eliminar la partición FactInternetSales
-  Haga clic en la partición de FactInternetSales y, a continuación, haga clic en **eliminar**.



## <a name="process-partitions"></a>Procesar particiones  
En el Administrador de particiones, tenga en cuenta el **procesa última** columna para cada una de las nuevas particiones acaba de crear se muestra en estas particiones nunca se han procesado. Cuando crea nuevas particiones, debe ejecutar una operación Procesar particiones o Procesar tabla para actualizar los datos de esas particiones.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Para procesar las particiones FactInternetSales  
  
1.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo Administrador de particiones.  
  
2.  Haga clic en el **FactInternetSales** de tabla, a continuación, haga clic en el **modelo** menú > **proceso** > **procesar particiones**.  
  
3.  En el cuadro de diálogo procesar particiones, compruebe **modo** está establecido en **proceso predeterminado**.  
  
4.  Active la casilla de la columna **Procesar** para cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.  

    ![como-tabular-lesson10-proceso-particiones](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    Si se le pide las credenciales de suplantación, escriba el nombre de usuario de Windows y la contraseña que especificó en la lección 2.  
  
    Aparece el cuadro de diálogo **Procesamiento de datos** con los detalles del proceso de cada partición. Observe que se ha transferido un número diferente de filas para cada partición. Esto es porque cada partición incluye solamente las filas del año especificado en la cláusula WHERE de la instrucción SQL. Cuando finalice el procesamiento, continúe y cierre el cuadro de diálogo Procesamiento de datos.  
  
    ![como tabulares-lesson10-proceso-completo](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 11: crear Roles](../analysis-services/lesson-11-create-roles.md). 
