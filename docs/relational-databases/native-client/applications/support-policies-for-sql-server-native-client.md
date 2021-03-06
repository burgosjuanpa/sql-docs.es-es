---
title: Directivas de soporte técnico para SQL Server Native Client | Documentos de Microsoft
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fcf6d00af82ce8a67fd3259d39118907713f97b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="support-policies-for-sql-server-native-client"></a>Directivas de soporte con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se describe la forma de usar diversos componentes de acceso a datos con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="server-support"></a>Compatibilidad de servidor  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 admite conexiones, [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
## <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos admitidos  
 En la tabla siguiente se enumeran los sistemas operativos admitidos por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
|Versión de SQL Server Native Client|Sistemas operativos compatibles|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client (SQL Server 2005)|Microsoft Windows 2000 Service Pack 4 o posterior<br /><br /> Microsoft Windows Server 2003 o posterior<br /><br /> Microsoft Windows XP Service Pack 1 o posterior<br /><br /> Microsoft Windows Vista (requiere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 o posterior)<br /><br /> Microsoft Windows Server 2008 R2 (requiere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 o posterior)|  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|Microsoft Windows Server 2003 Service Pack 2 o posterior<br /><br /> Microsoft Windows XP Service Pack 2 o posterior<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2|  
|SQL Server Native Client 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|Microsoft Windows Server 2003 Service Pack 2 o posterior<br /><br /> Microsoft Windows XP Service Pack 2 o posterior<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7|  
|SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7<br /><br /> Microsoft Windows 8<br /><br /> Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>Directivas de compatibilidad de ADO  
 Las aplicaciones ADO pueden usar el proveedor OLE DB SQLOLEDB que se incluye con Windows si no requieren ninguna de las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  
  
 Las aplicaciones ADO pueden usar la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client incluido en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Las aplicaciones ADO también pueden usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 (que se incluye en [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]) pero, si lo hacen, deben especificar `DataTypeCompatibility=80` en las cadenas de conexión. Solo estarán disponibles las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] cuando `DataTypeCompatibility=80` esté presente en las cadenas de conexión.  
  
## <a name="bcp-support-policies"></a>Directivas de soporte de BCP  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], bcp.exe admite archivos de datos que no sean más de tres versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores que la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que se incluía bcp.exe.  
  
## <a name="odbc-support-policies"></a>Directivas de compatibilidad de ODBC  
 Las aplicaciones deben usar el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se incluye con el sistema operativo Windows. Puede usar el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si la aplicación está certificada para usarse con una versión específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="ole-db-support-policies"></a>Directivas de soporte de OLE DB  
 Las aplicaciones deberían usar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se incluye con el sistema operativo Windows. Puede usar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si la aplicación está certificada para usarse con una versión específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 Las aplicaciones OLE DB que no estén certificadas para usarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client podrán usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si especifican `DataTypeCompatibility=80` en sus cadenas de conexión.  
  
 Las aplicaciones OLE DB que usan OLE DB Service Components solo pueden usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client si especifican `DataTypeCompatibility=80` en sus cadenas de conexión. Sin embargo, ninguna característica agregadas después [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] estará disponible en este caso.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
