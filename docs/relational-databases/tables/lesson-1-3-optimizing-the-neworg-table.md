---
title: Optimización de la tabla NewOrg | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be243734f05365ea7376e2e48e30479e46a7865c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>Lección 1-3: Optimizar la tabla NewOrg
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
La tabla **NewOrd** que ha creado en la tarea [Rellenar una tabla con los datos jerárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contiene toda la información del empleado y representa la estructura jerárquica mediante un tipo de datos **hierarchyid** . Esta tarea agrega los nuevos índices que admiten las búsquedas en la columna **hierarchyid** .  
  
## <a name="clustered-index"></a>Índice agrupado  
La columna **hierarchyid** (**OrgNode**) es la clave principal de la tabla **NewOrg** . Al crear la tabla, contenía un índice agrupado denominado **PK_NewOrg_OrgNode** para exigir la singularidad de la columna **OrgNode** . Este índice clúster también admite una búsqueda con prioridad a la profundidad de la tabla.  
  
## <a name="nonclustered-index"></a>Índice no agrupado  
Este paso crea dos índices no clúster que admiten búsquedas típicas.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>Para indizar la tabla NewOrg a fin de realizar búsquedas eficaces  
  
1.  Si quiere ayudar a realizar consultas en el mismo nivel de la jerarquía, use el método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para crear una columna calculada que contenga el nivel en la jerarquía. Después cree un índice compuesto en el nivel y **Hierarchyid**. Ejecute el código siguiente para crear la columna calculada y el índice con prioridad a la amplitud:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Cree un índice único en la columna **EmployeeID** . Esta es la búsqueda singleton tradicional de un empleado único por número de **EmployeeID** . Ejecute el código siguiente para crear un índice en **EmployeeID**:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Ejecute el código siguiente para recuperar los datos en la tabla en el orden de cada uno de los tres índices:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Compare los conjuntos de resultados para ver cómo se almacena el orden en cada tipo de índice. Solo siguen las primeras cuatro filas de cada de salida.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Índice con prioridad a la profundidad: los registros del empleado se almacenan junto a su administrador.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    El índice con prioridad a **EmployeeID**: las filas se almacenan en secuencia de **EmployeeID**.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> Para diagramas que muestran la diferencia entre un índice con prioridad a la profundidad y uno con prioridad a la amplitud, consulte [Datos jerárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>Para eliminar las columnas innecesarias  
  
1.  La columna **ManagerID** representa la relación de empleado/administrador, que representa ahora la columna **OrgNode** . Si el resto de aplicaciones no necesitan la columna **ManagerID** , considere la posibilidad de quitarla mediante la siguiente instrucción:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  La columna **EmployeeID** también es redundante. La columna **OrgNode** identifica singularmente a cada empleado. Si otras aplicaciones no necesitan la columna **EmployeeID** , considere la posibilidad de quitar el índice y, después, la columna mediante el código siguiente:  
  
    ```  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>Para sustituir la tabla original por la nueva tabla  
  
1.  Si la tabla original contenía algún índice o restricción adicional, agréguelos a la tabla **NewOrg** .  
  
2.  Reemplace la antigua tabla **EmployeeDemo** por la nueva. Ejecute el código siguiente para quitar la tabla antigua y, a continuación, cambie el nombre de la nueva tabla con el nombre anterior:  
  
    ```  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Ejecute el código siguiente para examinar la tabla final:  
  
    ```  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Resumen: Conversión de una tabla en una estructura jerárquica](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  
