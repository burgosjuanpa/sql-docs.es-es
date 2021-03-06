---
title: DATABASEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
caps.latest.revision: 84
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c7525291002bb22109c05600e25fdcd551c86b9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve la configuración actual de una opción o propiedad de base de datos especificada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*database*  
Es una expresión que representa el nombre de la base de datos para la que se devuelve la información de la propiedad con nombre. *database* es **nvarchar(128)**.  
Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)], debe ser el nombre de la base de datos actual. Devuelve NULL para todas las propiedades si se proporciona un nombre de base de datos diferente.
  
*property*  
Es una expresión que representa el nombre de la propiedad de base de datos que se va a devolver. *property* es **varchar (128)** y puede ser uno de estos valores. El tipo de valor devuelto es **sql_variant**. En la siguiente tabla se muestra el tipo de datos base de cada valor de propiedad.
  
> [!NOTE]  
>  Si no se inicia la base de datos, las propiedades que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recupera mediante acceso directo a la base de datos, en lugar de obtener el valor de los metadatos devolverán NULL. Es decir, si la base de datos tiene AUTO_CLOSE establecido en ON o si la base de datos está sin conexión.  
  
|Propiedad|Description|Valor devuelto|  
|---|---|---|
|Intercalación|Nombre de intercalación predeterminado para la base de datos.|Nombre de intercalación<br /><br /> NULL = La base de datos no se ha iniciado.<br /><br /> Tipo de datos base: **nvarchar(128)**|  
|ComparisonStyle|El estilo de comparación de Windows de la intercalación. ComparisonStyle es un mapa de bits que se calcula usando los siguientes valores para los posibles estilos.<br /><br /> Omitir mayúsculas y minúsculas: 1<br /><br /> Omitir acento: 2<br /><br /> Omitir Kana: 65536<br /><br /> Omitir ancho: 131072<br /><br /> <br /><br /> Por ejemplo, el valor predeterminado 196609 es el resultado de combinar las opciones de omitir mayúsculas y minúsculas, omitir Kana y omitir ancho.|Devuelve el estilo de comparación.<br /><br /> Devuelve 0 para todas las intercalaciones binarias.<br /><br /> Tipo de datos base: **int**|  
|Edición|El nivel de servicio o edición de la base de datos.|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> Uso general<br /><br /> Crucial para la empresa<br /><br /> Básico<br /><br /> Standard<br /><br /> Premium<br /><br /> System (de la base de datos maestra)<br /><br /> NULL = La base de datos no se ha iniciado.<br /><br /> Tipo de datos base: **nvarchar**(64)|  
|IsAnsiNullDefault|La base de datos sigue las reglas ISO para permitir los valores NULL.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAnsiNullsEnabled|Todas las comparaciones con un valor NULL tienen un resultado desconocido.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAnsiPaddingEnabled|Las cadenas se rellenan a la misma longitud antes de comparar o insertar.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAnsiWarningsEnabled|Se produce un mensaje de error o de advertencia cuando tiene lugar una condición de error estándar.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsArithmeticAbortEnabled|Las consultas se cancelan cuando hay un error de desbordamiento o división por cero durante su ejecución.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAutoClose|La base de datos se cierra sin problemas y libera los recursos cuando sale el último usuario.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAutoCreateStatistics|El optimizador de consultas crea estadísticas de columna única, según sea necesario, para mejorar el rendimiento de las consultas.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAutoCreateStatisticsIncremental|Las estadísticas de columna única creadas automáticamente son incrementales siempre que sea posible.|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAutoShrink|Los archivos de base de datos son candidatos para la reducción periódica automática.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsAutoUpdateStatistics|El optimizador de consultas actualiza las estadísticas existentes cuando las usa una consulta y podrían estar obsoletas.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|
|IsClone|La base de datos es una copia de solo estadísticas y esquema de una base de datos de usuario creada con DBCC CLONEDATABASE. Para obtener más información, vea este [artículo de Soporte técnico de Microsoft](http://support.microsoft.com/help/3177838).|**Se aplica a**: de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**| 
|IsCloseCursorsOnCommitEnabled|Los cursores que están abiertos se cierran cuando se confirma una transacción.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsFulltextEnabled|La base de datos está habilitada para la indización semántica y de texto completo.|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**<br /><br /> **Nota:** El valor de esta propiedad no tiene ningún efecto. En las bases de datos de usuario siempre está habilitada la búsqueda de texto completo. Esta columna se quitará en una próxima versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No utilice esta columna en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que actualmente usan cualquiera de estas columnas.|  
|IsInStandBy|La base de datos está en línea como de solo lectura con el registro de restauración permitido.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsLocalCursorsDefault|El valor predeterminado de las declaraciones de cursores es LOCAL.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|Se tiene acceso a las tablas con optimización en memoria mediante el aislamiento de instantánea cuando el valor de configuración TRANSACTION ISOLATION LEVEL de la sesión se establece en un nivel de aislamiento inferior, READ COMMITTED o READ UNCOMMITTED.|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> Tipo de datos base: **int**|  
|IsMergePublished|Las tablas de una base de datos se pueden publicar para la replicación de mezcla, si está instalada la replicación.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsNullConcat|La concatenación con un operando NULL da como resultado NULL.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsNumericRoundAbortEnabled|Se generan errores cuando se produce una pérdida de precisión en expresiones.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsParameterizationForced|La opción de base de datos PARAMETERIZATION es FORCED por medio del comando SET.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida|  
|IsQuotedIdentifiersEnabled|Se pueden utilizar comillas dobles en identificadores.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsPublished|Las tablas de la base de datos se pueden publicar para la replicación de instantáneas o transaccional, si está instalada la replicación.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsRecursiveTriggersEnabled|Se habilita la activación recursiva de desencadenadores.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsSubscribed|La base de datos está suscrita a una publicación.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsSyncWithBackup|La base de datos es una base de datos publicada o de distribución, y puede restaurarse sin interrumpir la replicación transaccional.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**|  
|IsTornPageDetectionEnabled|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detecta operaciones de E/S incompletas debido a problemas con el suministro eléctrico u otros errores del sistema.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**| 
|IsVerifiedClone|La base de datos es una copia de solo estadísticas y esquema de una base de datos de usuario creada con la opción WITH VERIFY_CLONEDB de DBCC CLONEDATABASE. Para obtener más información, vea este [artículo de Soporte técnico de Microsoft](http://support.microsoft.com/help/3177838).|**Se aplica a**: a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2.<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **int**| 
|IsXTPSupported|Indica si la base de datos es compatible con OLTP en memoria, es decir, permite crear y usar tablas optimizadas para memoria y módulos compilados de forma nativa.<br /><br /> Específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> IsXTPSupported es independiente de la existencia de algún grupo de archivos MEMORY_OPTIMIZED_DATA, necesario para crear objetos de OLTP en memoria.|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida, es un error o no es aplicable<br /><br /> Tipo de datos base: **int**|  
|LastGoodCheckDbTime|La fecha y hora de la última operación DBCC CHECKDB correcta que se ejecutó en la base de datos especificada.|**Se aplica a**: a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2.<br /><br /> NULL = Entrada no válida<br /><br /> Tipo de datos base: **datetime**| 
|LCID|Identificador de configuración regional (LCID) de Windows de la intercalación.|Valor de LCID (en formato decimal).<br /><br /> Tipo de datos base: **int**|  
|MaxSizeInBytes|Tamaño máximo de la base de datos en bytes.|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL = La base de datos no se ha iniciado<br /><br /> Tipo de base de datos: **bigint**|  
|Recuperación|Modelo de recuperación de la base de datos.|FULL = Modelo de recuperación completa<br /><br /> BULK_LOGGED = Modelo de registro masivo<br /><br /> SIMPLE = Modelo de recuperación simple<br /><br /> Tipo de datos base: **nvarchar(128)**|  
|ServiceObjective|Describe el nivel de rendimiento de la base de datos en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|Puede ser uno de los valores siguientes:<br /><br /> NULL = La base de datos no se ha iniciado<br /><br /> Compartido (para las ediciones Web o Business)<br /><br /> Básico<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> Sistema (para la base de datos maestra)<br /><br /> Tipo de datos base: **nvarchar(32)**|  
|ServiceObjectiveId|El identificador del objetivo del servicio en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|**uniqueidentifier** que identifica el objetivo del servicio.|  
|SQLSortOrder|Id. de orden de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compatible con versiones anteriores de SQL Server.|0 = La base de datos utiliza la intercalación de Windows<br /><br /> >0 = Identificador de criterio de ordenación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> NULL = La entrada no es válida o no se ha iniciado la base de datos.<br /><br /> Tipo de datos base: **tinyint**|  
|Estado|Estado de la base de datos.|ONLINE = La base de datos está disponible para consultas.<br /><br /> **Nota:** El estado ONLINE se puede devolver mientras la base de datos se esté abriendo y no se haya recuperado todavía. Para saber cuándo puede aceptar conexiones una base de datos, consulte la propiedad Collation de **DATABASEPROPERTYEX**. La base de datos puede aceptar conexiones cuando la intercalación de base de datos devuelve un valor distinto de NULL. En el caso de las bases de datos siempre visibles, consulte las columnas database_state o database_state_desc de sys.dm_hadr_database_replica_states.<br /><br /> OFFLINE = La base de datos está explícitamente sin conexión.<br /><br /> RESTORING = La base de datos se está restaurando.<br /><br /> RECOVERING = La base de datos se está recuperando y aún no está lista para consultas.<br /><br /> SUSPECT = La base de datos no se recuperó.<br /><br /> EMERGENCY = La base de datos está en un estado de emergencia de solo lectura. El acceso se restringe a los miembros del rol sysadmin<br /><br /> Tipo de datos base: **nvarchar(128)**|  
|Updateability|Indica si los datos se pueden modificar.|READ_ONLY = Los datos se pueden leer pero no modificar.<br /><br /> READ_WRITE = Los datos se pueden leer y modificar.<br /><br /> Tipo de datos base: **nvarchar(128)**|  
|UserAccess|Indica qué usuarios pueden tener acceso a la base de datos.|SINGLE_USER = Solo un usuario db_owner, dbcreator o sysadmin a la vez<br /><br /> RESTRICTED_USER = Solo los miembros de los roles db_owner, dbcreator y sysadmin<br /><br /> MULTI_USER = Todos los usuarios<br /><br /> Tipo de datos base: **nvarchar(128)**|  
|Versión|Número interno de versión del código de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el que se creó la base de datos. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|Número de versión = La base de datos está abierta.<br /><br /> NULL = La base de datos no se ha iniciado.<br /><br /> Tipo de datos base: **int**|  
  
## <a name="return-types"></a>Tipos de valores devueltos
**sql_variant**
  
## <a name="exceptions"></a>Excepciones  
Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECT_ID, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Notas  
DATABASEPROPERTYEX devuelve un único valor de propiedad cada vez. Para ver varios valores de propiedad, use la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-status-of-the-autoshrink-database-option"></a>A. Recuperar el estado de la opción de base de datos AUTO_SHRINK  
El ejemplo siguiente devuelve el estado de la opción de base de datos AUTO_SHRINK para la base de datos `AdventureWorks`.
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] Esto indica que AUTO_SHRINK está desactivado.
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. Recuperar la intercalación predeterminada de una base de datos  
En el siguiente ejemplo se devuelven varios atributos de la base de datos `AdventureWorks`.
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>Vea también
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[Estados de base de datos](../../relational-databases/databases/database-states.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
