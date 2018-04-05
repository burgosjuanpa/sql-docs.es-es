---
title: 'Issasynchstatus:: GetStatus (OLE DB) | Documentos de Microsoft'
description: ISSAsynchStatus::GetStatus (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 394539d4788df395e64c96f76c55edf0465326e2
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Devuelve el estado de una operación de ejecución asincrónica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 Identificador de capítulo. Si el objeto de sondeo no es un objeto de conjunto de filas o la operación no se aplica a un capítulo, se debe establecer en DB_NULL_HCHAPTER, que se pasa por alto por el proveedor.  
  
 *eOperation*[in]  
 Operación para la que se solicita el estado asincrónico. Debe utilizarse el siguiente valor:  
  
 DBASYNCHOP_OPEN: el consumidor solicita información sobre la apertura asincrónica o rellenado asincrónico de un conjunto de filas o sobre la inicialización asincrónica de un objeto de origen de datos. Si el proveedor es un proveedor compatible con OLE DB 2.5 que admite el enlace URL directo, el consumidor solicita información sobre la inicialización asincrónica o el rellenado asincrónico de un origen de datos, conjunto de filas, fila u objeto de flujo.  
  
 *pulProgress*[out]  
 Puntero a memoria en el que se devuelve el progreso actual de la operación asincrónica con respecto al máximo esperado indicado en el parámetro *pulProgressMax* . Para obtener más información acerca del significado de *pulProgress*, vea la descripción de *peAsynchPhase*.  
  
 Si *pulProgress* es un puntero NULL, no se devuelve ningún progreso.  
  
 *pulProgressMax*[out]  
 Puntero a memoria en el que se devuelve el valor máximo esperado del parámetro *pulProgress* . Este valor puede cambiar entre las distintas llamadas a este método. Para obtener más información acerca del significado de *pulProgressMax*, vea la descripción de *peAsynchPhase*.  
  
 Si *pulProgressMax* es un puntero NULL, no se devuelve ningún valor máximo esperado.  
  
 *peAsynchPhase*[out]  
 Un puntero a la memoria en el que se va a devolver información adicional sobre el progreso de la operación asincrónica. Los valores válidos incluyen:  
  
 DBASYNCHPHASE_INITIALIZATION: el objeto se encuentra en fase de inicialización. Los argumentos *pulProgress* y *pulProgressMax* indican una proporción estimada de progreso. El objeto aún no se ha materializado por completo. Al intentar llamar a otras interfaces puede generarse un error y es posible que en el objeto no esté disponible el conjunto completo de interfaces. Si la operación asincrónica se realizó como resultado de llamar a **ICommand::Execute** en un comando que actualiza, elimina o inserta filas y si *cParamSets* es mayor que 1, *pulProgress* y *pulProgressMax* pueden indicar el progreso de un conjunto único de parámetros o de la matriz completa de conjuntos de parámetros.  
  
 DBASYNCHPHASE_POPULATION: el objeto se encuentra en fase de rellenado. Si bien el conjunto de filas está totalmente inicializado y en el objeto está disponible todo el conjunto de interfaces, es posible que el conjunto de filas cuente con filas adicionales aún sin rellenar. Aunque *pulProgress* y *pulProgressMax* pueden basarse en el número de filas rellenado, generalmente se basan en el tiempo o el esfuerzo exigidos para rellenar el conjunto de filas. Por lo tanto, el autor de la llamada debe usar esta información como un cálculo aproximado del tiempo que puede durar el proceso, y no del recuento de filas final. Esta fase solo se devuelve durante el rellenado de un conjunto de filas; nunca se devuelve durante la inicialización de un objeto de origen de datos ni debido a la ejecución de un comando que actualiza, elimina o inserta filas.  
  
 DBASYNCHPHASE_COMPLETE: se ha completado el procesamiento asincrónico del objeto. **Issasynchstatus:: GetStatus** método devuelve un HRESULT que indica el resultado de la operación. Normalmente, será el HRESULT que se habría devuelto si la operación se hubiese llamado de forma sincrónica. Si la operación asincrónica era el resultado de una llamada a **ICommand::Execute** en un comando que actualiza, elimina o inserta filas, el valor de los parámetros *pulProgress* y *pulProgressMax* será igual al número total de filas afectadas por el comando. Si el valor de *cParamSets* es mayor que 1, éste será el número total de filas afectadas por todos los conjuntos de parámetros especificados en la ejecución. Si *peAsynchPhase* es un puntero NULL, no se devuelve ningún código de estado.  
  
 DBASYNCHPHASE_CANCELED: se ha anulado el procesamiento asincrónico del objeto. **Issasynchstatus:: GetStatus** método devuelve DB_E_CANCELED. Si la operación asincrónica era el resultado de una llamada a **ICommand::Execute** de un comando que actualiza, elimina o inserta filas, el valor de *pulProgress* es igual al número total de filas, de todos los conjuntos de parámetros, afectadas por el comando antes de la cancelación.  
  
 *ppwszStatusText*[in/out]  
 Puntero a memoria que contiene información adicional sobre la operación. Un proveedor puede usar este valor para distinguir los diferentes elementos de una operación; por ejemplo, el acceso a diferentes recursos. Esta cadena se localiza según la propiedad DBPROP_INIT_LCID del objeto de origen de datos.  
  
 Si *ppwszStatusText* no es NULL en la entrada, el proveedor devuelve el estado asociado al elemento específico identificado por *ppwszStatusText*. Si *ppwszStatusText* no indica ningún elemento de *eOperation*, el proveedor devuelve S_OK con los parámetros *pulProgress* y *pulProgressMax* establecidos en el mismo valor. Si el proveedor no distingue entre elementos basados en un identificador textual, establece *ppwszStatusText* en NULL y devuelve información sobre la operación como un todo; de lo contrario, si *ppwszStatusText* no es NULL en la entrada, el proveedor deja *ppwszStatusText* intacto.  
  
 Si *ppwszStatusText* es null en la entrada, el proveedor establece *ppwszStatusText* en un valor que indica más información sobre la operación, o null si dicha información no está disponible o si  **Issasynchstatus:: GetStatus** método devuelve un error. Cuando *ppwszStatusText* es NULL en la entrada, el proveedor asigna memoria a la cadena de estado y devuelve la dirección a esta memoria. El consumidor libera esta memoria con **IMalloc::Free** cuando ya no necesita la cadena.  
  
 Si *ppwszStatusText* es NULL en la entrada, no se devuelve ninguna cadena de estado y el proveedor devuelve información sobre cualquier elemento de la operación o sobre la operación en general.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se devolvió correctamente.  
  
-   Si *peAsynchPhase* es igual a DBASYNCHPHASE_INITIALIZATION, el objeto aún no está completamente inicializado; los intentos de llamar a otras interfaces pueden generar errores y es posible que en el objeto no esté disponible el conjunto completo de interfaces.  
  
-   Si *peAsynchPhase* es igual a DBASYNCHPHASE_POPULATION, el conjunto de filas está completamente inicializado y en el objeto está disponible todo el conjunto de interfaces; sin embargo, es posible que haya filas adicionales aún sin rellenar en el conjunto de filas.  
  
-   Si *peAsynchPhase* es igual a DBASYNCHPHASE_COMPLETE, significa que se ha completado todo el procesamiento asincrónico del objeto. El objeto está totalmente inicializado y rellenado.  
  
 DB_E_CANCELED  
 El procesamiento asincrónico se canceló durante el rellenado del conjunto de filas. El rellenado se detiene, pero el conjunto de filas sigue siendo válido para las filas ya rellenadas.  
  
 El procesamiento asincrónico se canceló durante la inicialización del objeto de origen de datos. El objeto de origen de datos se encuentra en un estado no inicializado.  
  
 E_INVALIDARG  
 El parámetro *hChapter* no es correcto.  
  
 E_UNEXPECTED  
 **Issasynchstatus:: GetStatus** método se llamó en un objeto de origen de datos, y **IDBInitialize:: Initialize** no se ha llamado en el objeto de origen de datos.  
  
 **Issasynchstatus:: GetStatus** método se llamó en un conjunto de filas, **ITransaction:: Commit** o **ITransaction:: Abort** se llamó, y el objeto está en estado inerte.  
  
 **Issasynchstatus:: GetStatus** método se llamó en un conjunto de filas que se canceló de forma asincrónica en su fase de inicialización. El conjunto de filas se encuentra en estado inerte.  
  
 E_FAIL  
 Se produjo un error específico del proveedor.  
  
## <a name="remarks"></a>Comentarios  
 El **issasynchstatus:: GetStatus** método se comporta exactamente igual que el **idbasynchstatus:: GetStatus** método salvo que si el objeto de origen de la inicialización de los datos se anula, se devuelve E_UNEXPECTED en su lugar de DB_E_CANCELED (aunque [issasynchstatus:: Waitforasynchcompletion](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) devolverá DB_E_CANCELED). Es porque el objeto de origen de datos no se queda en el estado inerte habitual que sigue a una interrupción para que se puedan intentar otras operaciones de inicialización.  
  
 Si el conjunto de filas se inicializa o rellena de forma asincrónica, debe admitir este método.  
  
 Además de los valores de retorno indicados, **ISSAsynchStatus::GetStatus** puede devolver cualquier HRESULT que hubiera devuelto el método que inició la operación asincrónica, que indica si la operación se ha realizado correcta o incorrectamente.  
  
 Algunas operaciones asincrónicas no pueda devolver ningún estado distinto de "finalizado" y "no finalizado". Estas operaciones deben establecer el valor de *pulProgressMax* en 1, que indica la granularidad todo o nada de su estimación, de modo que sus respuestas serían 0/1 ó 1/1.  
  
 Un proveedor puede cambiar *pulProgressMax* en llamadas sucesivas e incluso devolver una proporción menor que en ocasiones anteriores, si esto refleja una estimación mejorada del progreso de la tarea.  
  
 El proveedor no está obligado a garantizar ninguna otra precisión, pero se le anima a que lo haga en casos donde son posibles estimaciones razonables de progreso. Tales esfuerzos mejorarán la calidad de la interfaz de usuario porque es probable que el uso principal de esta función sea proporcionar información sobre el progreso al usuario. La satisfacción del usuario aumenta con la calidad de la información relativa a una tarea no visible de ejecución prolongada.  
  
 Al llamar a **ISSAsynchStatus::GetStatus** en un objeto de origen de datos inicializado o en un conjunto de filas rellenado o al pasar un valor a *eOperation* distinto de DBASYNCHOP_OPEN, se devuelve S_OK con los parámetros *pulProgress* y *pulProgressMax* establecidos en el mismo valor. Si **issasynchstatus:: GetStatus** método se llama en un objeto creado a partir de la ejecución de un comando que actualiza, elimina o inserta filas, ambos *pulProgress* y *pulProgressMax*  indican el número total de filas afectadas por el comando.  
  
## <a name="see-also"></a>Vea también  
 [Realizar las operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  