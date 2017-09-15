---
title: PERCENTILE_CONT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENTILE_CONT_TSQL
- PERCENTILE_CONT
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, PERCENTILE_CONT
- PERCENTILE_CONT function
ms.assetid: d019419e-5297-4994-97d5-e9c8fc61bbf4
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 424e3ac668bb979a2d30446ff1ecb57346a0e8ac
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="percentilecont-transact-sql"></a>PERCENTILE_CONT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Calcula un percentil basándose en una distribución continua de valores de columna en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El resultado se interpola y puede no ser igual que ninguno de los valores concretos de la columna.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
PERCENTILE_CONT ( numeric_literal )   
    WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_literal*  
 El percentil que se va a calcular. El valor debe estar entre 0,0 y 1,0.  
  
 EN el grupo **(** ORDER BY *order_by_expression* [ **ASC** | DESC]**)**  
 Especifica una lista de valores numéricos para ordenar y cuyo percentil se va a calcular. Solo un *order_by_expression* está permitido. La expresión debe evaluarse como un tipo numérico exacto (**int**, **bigint**, **smallint**, **tinyint**, **numérico**, **bits**, **decimal**, **smallmoney**, **dinero**) o un tipo numérico aproximado ( **float**, **real**). No se permiten otros tipos de datos. El criterio de ordenación predeterminado es ascendente.  
  
 SOBRE **(** \<partition_by_clause > **)**  
 Divide el conjunto de resultados generado por la cláusula FROM en particiones a las que se aplica la función de percentil. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md). El \<cláusula ORDER BY > y \<filas o cláusula range > de la sintaxis OVER no se pueden especificar en una función PERCENTILE_CONT.  
  
## <a name="return-types"></a>Tipos devueltos  
 **float(53)**  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 En el nivel de compatibilidad 110 y posteriores, WITHIN GROUP es una palabra clave reservada. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Notas generales  
 Se omite cualquier valor NULL del conjunto de datos.  
  
 PERCENTILE_CONT es no determinista. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-basic-syntax-example"></a>A. Ejemplo de sintaxis básica  
 En el ejemplo siguiente se usa PERCENTILE_CONT y PERCENTILE_DISC para buscar el salario medio de los empleados de cada departamento. Tenga en cuenta que estas funciones pueden no devolver el mismo valor. Esto se debe a que PERCENTILE_CONT interpola el valor adecuado, tanto si existe en el conjunto de datos como si no existe, mientras que PERCENTILE_DISC siempre devuelve un valor real del conjunto.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 `DepartmentName        MedianCont    MedianDisc`  
  
 `--------------------   ----------   ----------`  
  
 `Document Control       16.8269      16.8269`  
  
 `Engineering            34.375       32.6923`  
  
 `Executive              54.32695     48.5577`  
  
 `Human Resources        17.427850    16.5865`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. Ejemplo de sintaxis básica  
 En el ejemplo siguiente se usa PERCENTILE_CONT y PERCENTILE_DISC para buscar el salario medio de los empleados de cada departamento. Tenga en cuenta que estas funciones pueden no devolver el mismo valor. Esto se debe a que PERCENTILE_CONT interpola el valor adecuado, tanto si existe en el conjunto de datos como si no existe, mientras que PERCENTILE_DISC siempre devuelve un valor real del conjunto.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianCont  
,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 `DepartmentName        MedianCont    MedianDisc`  
  
 `--------------------   ----------   ----------`  
  
 `Document Control       16.826900    16.8269`  
  
 `Engineering            34.375000    32.6923`  
  
 `Human Resources        17.427850    16.5865`  
  
 `Shipping and Receiving 9.250000      9.0000`  
  
## <a name="see-also"></a>Vea también  
 [PERCENTILE_DISC &#40; Transact-SQL &#41;](../../t-sql/functions/percentile-disc-transact-sql.md)  
  
  


