---
title: "Instalar SQL Server desde el símbolo del sistema | Microsoft Docs"
ms.custom: 
ms.date: 09/07/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing SQL Server, command prompt
- installation scripts [SQL Server]
- maintenance scripts [SQL Server]
- REMOVENODE property
- components [SQL Server], removing
- command prompt [SQL Server], SQL Server installations
- ASACCOUNT parameter
- failover clustering [SQL Server], installing
- master database [SQL Server], rebuilding
- SQLCOLLATION parameter
- clusters [SQL Server], installing
- unattended installations [SQL Server]
- modifying collations
- AGTPASSWORD parameter
- USESYSDB parameter
- RSPASSWORD parameter
- AUTOSTART parameter
- ASPASSWORD parameter
- stand-alone installations [SQL Server]
- SAMPLEDATABASESERVER parameter
- adding components
- SAPWD parameter
- scripts [SQL Server], uninstallations
- remote installations [SQL Server]
- components [SQL Server], installing
- TARGETCOMPUTER parameter
- REMOVENODE parameter
- REINSTALLMODE parameter
- scripts [SQL Server], maintenance
- rebuilding registry
- SQLPASSWORD parameter
- rebuilding databases
- IP property
- PIDKEY parameter
- RSCONFIGURATION parameter
- ADDLOCAL parameter
- Setup [SQL Server], command prompt
- REBUILDDATABASE parameter
- SECURITYMODE parameter
- REMOVE property
- DISABLENETWORKPROTOCOLS parameter
- INSTALLDATADIR parameter
- REMOVE parameter
- removing components
- SQLACCOUNT parameter
- parameters [SQL Server], SQL Server installations
- UPGRADE parameter
- shortcuts [SQL Server]
- updating components
- removing SQL Server
- clustered instance of SQL Server
- INSTALLSQLDATADIR parameter
- RSACCOUNT parameter
- ADMINPASSWORD parameter
- GROUP property
- ERRORREPORTING property
- uninstallation scripts [SQL Server]
- AGTACCOUNT parameter
- SAVESYSDB parameter
- INSTALLVS parameter
- INSTANCENAME parameter
- scripts [SQL Server], installations
- rebuilding database, master
- uninstalling SQL Server
- ASCOLLATION parameter
- .ini files
- ADDNODE parameter
- command line installations [SQL Server]
- VS parameter
- INSTALLASDATADIR parameter
- INSTALLSQLDIR parameter
- nodes [Faillover Clustering], command prompt
- INSTALLSQLSHAREDDIR parameter
ms.assetid: df40c888-691c-4962-a420-78a57852364d
caps.latest.revision: 255
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: 0015d57b64757afb886fb6ded1d5803d93ed13e3
ms.contentlocale: es-es
ms.lasthandoff: 09/12/2017

---
# <a name="install-sql-server-from-the-command-prompt"></a>Instalar SQL Server desde el símbolo del sistema
  Antes de ejecutar el programa de instalación de SQL Server, consulte [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
 Instalar una nueva instancia de SQL Server en el símbolo del sistema le permite especificar las características que se instalarán y cómo se deben configurar. También puede especificar la interacción silenciosa, básica o completa con la interfaz de usuario del programa de instalación.  
  
> **NOTA:** Al realizar la instalación a través del símbolo del sistema, SQL Server admite el modo totalmente silencioso mediante el uso del parámetro /Q o el modo silencioso sencillo mediante el parámetro /QS. El modificador /QS solamente muestra el progreso, pero no acepta ninguna entrada ni muestra mensajes de error si los encuentra. El parámetro /QS solamente se admite cuando se ha especificado /Action=install.  
  
 Con independencia del método de instalación, es necesario confirmar la aceptación de los términos de la licencia de software como usuario individual o en nombre de una entidad, a menos que el uso del software en su caso se rija por un acuerdo independiente, como un acuerdo de licencia por volumen de Microsoft o un acuerdo suscrito con un ISV u OEM.  
  
 Los términos de la licencia se muestran para revisarlos y aceptarlos en la interfaz de usuario del programa de instalación. Las instalaciones desatendidas (mediante los parámetros /Q o /QS) deben incluir el parámetro /IACCEPTSQLSERVERLICENSETERMS. Puede revisar separadamente los términos de licencia en [Términos de licencia de software de Microsoft](http://go.microsoft.com/fwlink/?LinkId=148209).  
  
> **NOTA:** Dependiendo de cómo haya recibido el software (por ejemplo, a través de un contrato de licencias por volumen de Microsoft), su uso del software puede estar sujeto a términos y condiciones adicionales.  
  
 La instalación desde el símbolo del sistema se admite en los escenarios siguientes:  
  
-   Al instalar, actualizar o quitar una instancia y los componentes compartidos de SQL Server en un equipo local usando la sintaxis y los parámetros que se especifiquen en el símbolo del sistema.  
  
-   Al instalar, actualizar o quitar una instancia del clúster de conmutación por error.  
  
-   Actualizar de una edición de SQL Server a otra edición de SQL Server.  
  
-   Instalar una instancia de SQL Server en un equipo local mediante el uso de la sintaxis y los parámetros especificados en un archivo de configuración. Puede usar este método para copiar una configuración de instalación en varios equipos o para instalar varios nodos de una instalación de clúster de conmutación por error.  
  
 Al instalar SQL Server en el símbolo del sistema, especifique los parámetros para su instalación en el símbolo del sistema como parte de la sintaxis de la instalación.  
  
> **NOTA:** En las instalaciones locales debe ejecutar el programa de instalación como administrador. Si instala SQL Server desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso. Para las instalaciones de clúster de conmutación por error, debe ser un administrador local con permisos para iniciar sesión como servicio y para actuar como parte del sistema operativo en todos los nodos de clúster de conmutación por error.  
  
##  <a name="ProperUse"></a> Uso correcto de los parámetros de instalación  
 Use las instrucciones siguientes para desarrollar comandos de instalación que tengan la sintaxis correcta:  
  
-   /PARAMETER  
  
-   /PARAMETER=true/false  
  
-   /PARAMETER=1/0 para tipos booleanos  
  
-   /PARAMETER="value" para todos los parámetros de un solo valor. Se recomienda el uso de comillas dobles, pero es necesario si el valor contiene un espacio  
  
-   /PARAMETER="value1" "value2" "value3" para todos los parámetros con varios valores. Se recomienda el uso de comillas dobles, pero es necesario si el valor contiene un espacio  
  
 **Excepciones:**  
  
-   /FEATURES, que es un parámetro de varios valores, pero su formato es /FEATURES=AS,RS,IS sin un espacio, delimitado por comas  
  
 **Ejemplos:**  
  
-   /INSTANCEDIR=c:\Ruta de acceso admitida.  
  
-   /INSTANCEDIR=”c:\Ruta de acceso” admitida  
  
> [!NOTE]  
>  -   Si, al instalar SQL Server, se especifica la misma ruta de directorio para INSTANCEDIR y para SQLUSERDBDIR, el Agente SQL Server y la búsqueda de texto completo no se inician debido a que faltan permisos.  
>   
>      Los valores de servidores relacionales admiten formatos adicionales que finalicen con una barra diagonal inversa (barra diagonal inversa o dos caracteres de barra diagonal inversa) en la ruta de acceso.  
> -   /PID, el valor de este parámetro se debe incluir entre comillas dobles.  
  
## <a name="sql-server-parameters"></a>Parámetros de SQL Server  
 En las secciones siguientes se proporcionan parámetros para desarrollar scripts de instalación de la línea de comandos en escenarios de instalación, actualización y reparación.  
  
 Los parámetros que se enumeran para un componente de SQL Server son específicos de ese componente. Los parámetros del Agente SQL Server y SQL Server Browser son aplicables cuando instala [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   [Parámetros de instalación](#Install)  
  
-   [Parámetros de SysPrep](#SysPrep)  
  
-   [Parámetros de actualización](#Upgrade)  
  
-   [Parámetros de reparación](#Repair)  
  
-   [Parámetros de regeneración de bases de datos del sistema](#Rebuild)  
  
-   [Parámetros de desinstalación](#Uninstall)  
  
-   [Parámetros de clúster de conmutación por error](#ClusterInstall)  
  
-   [Parámetros de cuentas de servicio](#Accounts)  
  
-   [Parámetros de características](#Feature)  
  
-   [Parámetros de rol](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RoleParameters)  
  
-   [Controlar el comportamiento de la conmutación por error con el parámetro /FAILOVERCLUSTERROLLOWNERSHIP](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RollOwnership)  
  
-   [Configuración de identificador de instancia o InstanceID](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#InstanceID) 
  
##  <a name="Install"></a> Parámetros de instalación  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la instalación.  
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación.<br /><br /> Valores admitidos: **Install**.|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/IACCEPTROPENLICENSETERMS <br /><br /> **Obligatorio únicamente cuando se especifican los parámetros /Q o/QS para instalaciones desatendidas que incluyen R Services (En base de datos) o Microsoft R Server.**|Obligatorio para confirmar la aceptación de los términos de licencia.| 
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/UpdateEnabled<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/UpdateSource<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/> Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173).<br /><br /> Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> O bien<br /><br /> /ROLE<br /><br /> **Obligatorio**|Especifica los componentes que se van a instalar.<br /><br /> Elija **/FEATURES** para especificar los componentes de SQL Server individuales que se van a instalar. Para obtener más información, vea [Parámetros de características](#Feature) a continuación.<br /><br /> Elija **/ROLE** para especificar un rol de instalación. Los roles de instalación instalan SQL Server en una configuración predeterminada.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros de instalación.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalice a la consola.|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 32 bits. Se admite únicamente en un sistema de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes específicos de la instancia.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> **Opcional**|Especifica un valor no predeterminado para un [InstanceID](#InstanceID).|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/UIMODE<br /><br /> **Opcional**|Especifica si se va a presentar solo el número mínimo de cuadros de diálogo durante la instalación.<br /><br /> **/UIMode** solo se puede usar con los parámetros **/ACTION=INSTALL** y **UPGRADE** . Valores admitidos:<br /><br /> **/UIMODE=Normal** es el valor predeterminado para las ediciones distintas de Express y presenta todos los cuadros de diálogo de instalación para las características seleccionadas.<br /><br /> **/UIMODE=AutoAdvance** es el valor predeterminado para las ediciones distintas de Express y omite los cuadros de diálogo no esenciales.<br /><br /> <br /><br /> Cabe decir que, cuando se combina con otros parámetros, se invalida **UIMODE** . Por ejemplo, cuando se proporciona tanto **/UIMODE=AutoAdvance** como **/ADDCURRENTUSERASSQLADMIN=FALSE** , el cuadro de diálogo de aprovisionamiento no se rellena automáticamente con el usuario actual.<br /><br /> La configuración **UIMode** no se puede usar con los parámetros **/Q** ni **/QS** .|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Agente SQL Server|/AGTSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta para el servicio Agente SQL Server.|  
|Agente SQL Server|/AGTSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta del servicio del Agente SQL Server.|  
|Agente SQL Server|/AGTSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) para el servicio del Agente SQL Server.<br /><br /> Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Valor predeterminado: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica el modo de servidor de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Los valores válidos son MULTIDIMENSIONAL, POWERPIVOT o TABULAR. **ASSERVERMODE** distingue entre mayúsculas y minúsculas. Todos los valores se deben expresar en mayúsculas. Para obtener más información sobre los valores válidos, vea [Instalar Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Especifica las credenciales de administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos temporales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica si el proveedor MSOLAP se puede ejecutar en proceso.<br /><br /> Valor predeterminado: 1=habilitado|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMACCOUNT<br /><br /> **Obligatorio para SPI_AS_NewFarm**|Especifica una cuenta de usuario de dominio para ejecutar los servicios de Administración central de SharePoint y otros servicios esenciales en una granja.<br /><br /> Este parámetro solo se usa para instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas a través de /ROLE = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMPASSWORD<br /><br /> **Obligatorio para SPI_AS_NewFarm**|Especifica una contraseña para la cuenta de la granja.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/PASSPHRASE<br /><br /> **Obligatorio para SPI_AS_NewFarm**|Especifica una frase de contraseña que se utiliza para agregar servidores de aplicación adicionales o servidores front-end web a una granja de SharePoint.<br /><br /> Este parámetro solo se usa para instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas a través de /ROLE = SPI_AS_NEWFARM.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMADMINIPORT<br /><br /> **Obligatorio para SPI_AS_NewFarm**|Especifica un puerto para conectar con la aplicación web de Administración central de SharePoint.<br /><br /> Este parámetro solo se usa para instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instaladas a través de /ROLE = SPI_AS_NEWFARM.|  
|SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio SQL Server Browser. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Opcional**|Habilita las credenciales del comando run-as para las instalaciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Opcional**|Especifica el directorio de datos de los archivos de datos de SQL Server. Valores predeterminados:<br /><br /> En el modo WOW en 64 bits:%Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> En todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Obligatorio cuando /SECURITYMODE=SQL**|Especifica la contraseña de la cuenta de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica el modo de seguridad de SQL Server.<br /><br /> Si no se proporciona este parámetro, se admite el modo de autenticación solamente de Windows.<br /><br /> Valor admitido: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para SQL Server.<br /><br /> El valor predeterminado se basa en la configuración regional del sistema operativo Windows. Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ADDCURRENTUSERASSQLADMIN<br /><br /> **Opcional**|Agrega el usuario actual al rol fijo de servidor**sysadmin** de SQL Server. El parámetro /ADDCURRENTUSERASSQLADMIN se puede usar al instalar las ediciones Express o cuando se usa /Role=ALLFeatures_WithDefaults. Para obtener más información, vea /ROLE a continuación.<br /><br /> El uso de /ADDCURRENTUSERASSQLADMIN es opcional, pero /ADDCURRENTUSERASSQLADMIN o /SQLSYSADMINACCOUNTS es obligatorio. Valores predeterminados:<br /><br /> **Verdadero** para las ediciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> **False** en todas las demás|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio del servicio de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de SQL Server. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Use este parámetro para proporcionar inicios de sesión que sean miembros del rol sysadmin.<br /><br /> Para las ediciones SQL Server distintas de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], es obligatorio /SQLSYSADMINACCOUNTS. Para las ediciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], el uso de /SQLSYSADMINACCOUNTS es opcional, pero es obligatorio /SQLSYSADMINACCOUNTS o /ADDCURRENTUSERASSQLADMIN.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica los directorios de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Opcional**|Especifica el número de archivos de datos de tempdb que va a agregar el programa de instalación. Este valor se puede aumentar hasta el número de núcleos existente. Valor predeterminado:<br /><br /> 1 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 o el número de núcleos, lo que sea menor en todas las demás ediciones<br /><br /> **\*\* Importante \*\*** El archivo de base de datos principal para tempdb seguirá siendo tempdb.mdf. Los archivos de tempdb adicionales se denominarán tempdb_mssql_#.ndf, donde # es un número único para cada archivo de base de datos de tempdb extra creado durante la instalación. Lo que se persigue con esta convención de nomenclatura es que estos archivos sean únicos. Si se desinstala una instancia de SQL Server, se eliminan los archivos con la convención de nomenclatura tempdb_mssql_#.ndf. No use la convención de nomenclatura tempdb_mssql_*.ndf con archivos de base de datos de usuario.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de datos de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64. Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de registro de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64. Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCINSTANTFILEINIT<br /><br /> **Opcional**|Habilita la inicialización instantánea de archivos de la cuenta de servicio de SQL Server. Vea [Inicialización instantánea de archivos de la base de datos](../../relational-databases/databases/database-instant-file-initialization.md)para conocer las consideraciones sobre seguridad y rendimiento.<br /><br /> Valor predeterminado: "False"<br /><br /> Valor opcional: "True"|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica el nivel de acceso de la característica FILESTREAM. Valores admitidos:<br /><br /> 0=Deshabilitar la compatibilidad de FILESTREAM con esta instancia. (Valor predeterminado)<br /><br /> 1=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] y a la transmisión por secuencias de E/S de archivos. (No es válido en escenarios de clúster)<br /><br /> 3=Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Obligatorio cuando FILESTREAMLEVEL es mayor que 1.**|Especifica el nombre del recurso compartido de Windows en el que se almacenarán los datos de FILESTREAM.|  
|Texto completo de SQL Server|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta para el servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. Se usa ServiceSID para asegurar la comunicación entre SQL Server y el demonio de filtro de texto completo. Si no se proporcionan los valores, se deshabilita el servicio iniciador de filtro de texto completo. Tiene que usar el Administrador de control de SQL Server para cambiar la cuenta del servicio y habilitar la funcionalidad de texto completo.<br /><br /> Valor predeterminado: cuenta de servicio local|  
|Texto completo de SQL Server|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña del servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Valor predeterminado: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Configuración de red de SQL Server|/NPENABLED<br /><br /> **Opcional**|Especifica el estado del protocolo Canalizaciones con nombre del servicio de SQL Server. Valores admitidos:<br /><br /> 0=deshabilitar el protocolo Canalizaciones con nombre<br /><br /> 1=habilitar el protocolo Canalizaciones con nombre|  
|Configuración de red de SQL Server|/TCPENABLED<br /><br /> **Opcional**|Especifica el estado del protocolo TCP para el servicio de SQL Server. Valores admitidos:<br /><br /> 0=Deshabilitar el protocolo TCP<br /><br /> 1= Habilitar el protocolo TCP|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Valores admitidos:<br /><br /> **SharePointFilesOnlyMode**<br /><br /> **DefaultNativeMode**<br /><br /> **FilesOnlyMode**<br /><br /> <br /><br /> Nota: Si la instalación incluye SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], el valor predeterminado de RSINSTALLMODE es DefaultNativeMode.<br /><br /> Si la instalación no incluye SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], el valor predeterminado de RSINSTALLMODE es FilesOnlyMode.<br /><br /> Si elige DefaultNativeMode pero la instalación no incluye SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)], la instalación cambiará automáticamente RSINSTALLMODE a FilesOnlyMode.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta de inicio del servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|R Services (en bases de datos)|MRCACHEDIRECTORY|Use este parámetro para especificar el directorio de caché de componentes de Microsoft R Open y Microsoft R Server como se describe en [esta sección](https://msdn.microsoft.com/library/mt695942.aspx). Esta opción se usa normalmente cuando se instala SQL Server R Services desde la línea de comandos en un equipo sin acceso a Internet.|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para instalar una instancia nueva e independiente con los componentes de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], replicación y búsqueda de texto completo y habilitar la inicialización instantánea de archivos para [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. 
  
```  
  
Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSVCINSTANTFILEINIT="True" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="SysPrep"></a> Parámetros de SysPrep  
 Para obtener más información sobre SQL Server SysPrep, vea  
  
 [Instalar SQL Server 2016 mediante SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md). 
  
#### <a name="prepare-image-parameters"></a>Preparar los parámetros de imagen  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para preparar una instancia de SQL Server sin configurarla. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación.<br /><br /> Valores admitidos: **PrepareImage**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/UpdateEnabled<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/UpdateSource<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> **Obligatorio**|Especifica los [componentes](#Feature) que se van a instalar.<br /><br /> Los valores admitidos son SQLEngine, Replication, FullText, DQ, AS, AS_SPI, RS, RS_SHP, RS_SHPWFE, DQC, Conn, IS, BC, SDK, DREPLAY_CTLR, DREPLAY_CLT, SNAC_SDK, SQLODBC, SQLODBC_SDK, LocalDB, MDS, POLYBASE.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros de instalación.|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalice a la consola.|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes específicos de la instancia.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> Antes de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (enero de 2013) **Necesario**<br /><br /> A partir de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 se **requiere** para características de instancia.|Especifica InstanceID para la instancia que se prepara.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para preparar una nueva instancia independiente con los componentes [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replicación y Búsqueda de texto completo y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. 
  
```  
Setup.exe /q /ACTION=PrepareImage /FEATURES=SQL,RS /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-image-parameters"></a>Parámetros de imagen completos  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para completar y configurar una instancia preparada de SQL Server. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación.<br /><br /> Valores admitidos: **CompleteImage**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros de instalación.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalice a la consola.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> Antes de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (enero de 2013) **Necesario**<br /><br /> A partir de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Opcional**|Use el identificador de instancia durante el paso para preparar la imagen.<br /><br /> Valores admitidos: InstanceID de una instancia preparada.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> Antes de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (enero de 2013) **Necesario**<br /><br /> A partir de la actualización acumulativa 2 de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Opcional**|Especifica un nombre de instancia de SQL Server para la instancia que se ha completado.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.<br /><br /> Nota: Si está instalando SQL Server Express, SQL Server Express with Tools o SQL Server Express con Advanced Services, el PID está predefinido.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Agente SQL Server|/AGTSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta para el servicio Agente SQL Server.|  
|Agente SQL Server|/AGTSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta del servicio del Agente SQL Server.|  
|Agente SQL Server|/AGTSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) para el servicio del Agente SQL Server. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio SQL Server Browser. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Opcional**|Habilita las credenciales del comando run-as para las instalaciones de SQL Server Express.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Opcional**|Especifica el directorio de datos de los archivos de datos de SQL Server. Valores predeterminados:<br /><br /> En el modo WOW en 64 bits:%Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> En todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Obligatorio cuando /SECURITYMODE=SQL**|Especifica la contraseña de la cuenta de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica el modo de seguridad de SQL Server.<br /><br /> Si no se proporciona este parámetro, se admite el modo de autenticación solamente de Windows.<br /><br /> Valor admitido: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad.<br /><br /> Valor predeterminado:<br /><br /> \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para SQL Server.<br /><br /> El valor predeterminado se basa en la configuración regional del sistema operativo Windows. Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio del servicio de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de SQL Server. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Use este parámetro para proporcionar inicios de sesión que sean miembros del rol sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica los directorios de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de datos de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64<br /><br /> Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Opcional**|Especifica el tamaño inicial en MB del archivo de registro de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado:<br /><br /> 4 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 en todas las demás ediciones<br /><br /> Intervalo permitido: Mín. = valor predeterminado (4 u 8); Máx. = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de registro de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Opcional**|Especifica el número de archivos de datos de tempdb que va a agregar el programa de instalación. Este valor se puede aumentar hasta el número de núcleos existente. Valor predeterminado:<br /><br /> 1 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 o el número de núcleos, lo que sea menor en todas las demás ediciones<br /><br /> **\*\* Importante \*\*** El archivo de base de datos principal para tempdb seguirá siendo tempdb.mdf. Los archivos de tempdb adicionales se denominarán tempdb_mssql_#.ndf, donde # es un número único para cada archivo de base de datos de tempdb extra creado durante la instalación. Lo que se persigue con esta convención de nomenclatura es que estos archivos sean únicos. Si se desinstala una instancia de SQL Server, se eliminan los archivos con la convención de nomenclatura tempdb_mssql_#.ndf. No use la convención de nomenclatura tempdb_mssql_\*.ndf con archivos de base de datos de usuario.<br /><br /> **\*\* Advertencia \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]no se puede usar para configurar este parámetro. El programa de instalación solamente instala un único archivo de datos de tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica el nivel de acceso de la característica FILESTREAM. Valores admitidos:<br /><br /> 0=Deshabilitar la compatibilidad de FILESTREAM con esta instancia. (Valor predeterminado)<br /><br /> 1=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] y a la transmisión por secuencias de E/S de archivos. (No es válido en escenarios de clúster)<br /><br /> 3=Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Obligatorio cuando FILESTREAMLEVEL es mayor que 1.**|Especifica el nombre del recurso compartido de Windows en el que se almacenarán los datos de FILESTREAM.|  
|Texto completo de SQL Server|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta para el servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. Se usa ServiceSID para asegurar la comunicación entre SQL Server y el demonio de filtro de texto completo. Si no se proporcionan los valores, se deshabilita el servicio iniciador de filtro de texto completo. Tiene que usar el Administrador de control de SQL Server para cambiar la cuenta del servicio y habilitar la funcionalidad de texto completo.<br /><br /> Valor predeterminado: cuenta de servicio local|  
|Texto completo de SQL Server|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña del servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|Configuración de red de SQL Server|/NPENABLED<br /><br /> **Opcional**|Especifica el estado del protocolo Canalizaciones con nombre del servicio de SQL Server. Valores admitidos:<br /><br /> 0=deshabilitar el protocolo Canalizaciones con nombre<br /><br /> 1=habilitar el protocolo Canalizaciones con nombre|  
|Configuración de red de SQL Server|/TCPENABLED<br /><br /> **Opcional**|Especifica el estado del protocolo TCP para el servicio de SQL Server. Valores admitidos:<br /><br /> 0=Deshabilitar el protocolo TCP<br /><br /> 1= Habilitar el protocolo TCP|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta de inicio del servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para completar una instancia preparada e independiente que incluye los componentes [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replicación y Búsqueda de texto completo. 
  
```  
  
setup.exe /q /ACTION=CompleteImage /INSTANCENAME=MYNEWINST /INSTANCEID=<MYINST> /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="Upgrade"></a> Parámetros de actualización  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la actualización. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación. Valores admitidos:<br /><br /> **Actualización**<br /><br /> **EditionUpgrade**<br /><br /> <br /><br /> El valor **EditionUpgrade** se usa para actualizar una edición existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una edición diferente. Para obtener más información acerca de las actualizaciones de edición y versión compatibles, vea [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/*/UpdateEnabled*<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/*UpdateSource*<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/ INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> **Obligatorio cuando se actualiza desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]** o posterior.<br /><br /> **Opcional cuando se actualiza desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Especifica un valor no predeterminado para un [InstanceID](#InstanceID).|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/UIMODE<br /><br /> **Opcional**|Especifica si se va a presentar solo el número mínimo de cuadros de diálogo durante la instalación. <br />                **/UIMode** solo se puede usar con los parámetros **/ACTION=INSTALL** y **UPGRADE** . Valores admitidos:<br /><br /> **/UIMODE=Normal** es el valor predeterminado para las ediciones distintas de Express y presenta todos los cuadros de diálogo de instalación para las características seleccionadas.<br /><br /> **/UIMODE=AutoAdvance** es el valor predeterminado para las ediciones distintas de Express y omite los cuadros de diálogo no esenciales.<br /><br /> Tenga en cuenta que la opción **UIMode** no se puede usar con los parámetros **/Q** ni **/QS** .|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola estaría oculta o cerrada.|  
|Servicio SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio SQL Server Browser. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|Texto completo de SQL Server|/FTUPGRADEOPTION<br /><br /> **Opcional**|Especifica la opción de actualización del catálogo de texto completo. Valores admitidos:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Valor predeterminado: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Opcional**|La propiedad solo se utiliza al actualizar un servidor de informes en modo de SharePoint que sea de la versión 2008 R2 o anterior. Las operaciones adicionales de actualización se realizan en los servidores de informes que utilizan la arquitectura en modo de SharePoint más antigua, que se cambió en SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si esta opción no se incluye con la instalación de línea de comandos, la cuenta de servicio predeterminada se utiliza para la antigua instancia del servidor de informes. Si se usa esta propiedad, proporcione la contraseña de la cuenta mediante la propiedad **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Opcional**|Contraseña de la cuenta de servicio del Servidor de informes existente.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/ALLOWUPGRADEFORSSRSSHAREPOINTMODE|Se requiere el modificador al actualizar una instalación en modo de SharePoint que se basa en la arquitectura de servicio compartido de SharePoint. El modificador no es necesario para actualizar versiones de servicios no compartidos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para actualizar una instancia o un nodo de clúster de conmutación por error existente de una versión de SQL Server anterior,  
  
```  
Setup.exe /q /ACTION=upgrade /INSTANCEID = <INSTANCEID>/INSTANCENAME=MSSQLSERVER /RSUPGRADEDATABASEACCOUNT="<Provide a SQL Server logon account that can connect to the report server during upgrade>" /RSUPGRADEPASSWORD="<Provide a password for the report server upgrade account>" /ISSVCAccount="NT Authority\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="Repair"></a> Parámetros de reparación  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la reparación. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la reparación.<br /><br /> Valores admitidos: **Repair**|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> **Obligatorio**|Especifica los [componentes](#Feature) que se van a reparar.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Reparar una instancia y componentes compartidos. 
  
```  
Setup.exe /q /ACTION=Repair /INSTANCENAME=<instancename>  
```  
  
##  <a name="Rebuild"></a> Parámetros de regeneración de bases de datos del sistema  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para volver a generar las bases de datos del sistema maestra, modelo, msdb y tempdb. Para obtener más información, vea [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md). 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la base de datos de regeneración.<br /><br /> Valores admitidos: **Rebuilddatabase**|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica una nueva intercalación de nivel de servidor.<br /><br /> El valor predeterminado se basa en la configuración regional del sistema operativo Windows. Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Obligatorio si se ha especificado /SECURITYMODE=SQL durante la instalación de la instancia.**|Especifica la contraseña de la cuenta SA de SQL.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Use este parámetro para proporcionar inicios de sesión que sean miembros del rol sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica los directorios de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Opcional**|Especifica el número de archivos de datos de tempdb que va a agregar el programa de instalación. Este valor se puede aumentar hasta el número de núcleos existente. Valor predeterminado:<br /><br /> 1 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 o el número de núcleos, lo que sea menor en todas las demás ediciones<br /><br /> **\*\* Importante \*\*** El archivo de base de datos principal para tempdb seguirá siendo tempdb.mdf. Los archivos de tempdb adicionales se denominarán tempdb_mssql_#.ndf, donde # es un número único para cada archivo de base de datos de tempdb extra creado durante la instalación. Lo que se persigue con esta convención de nomenclatura es que estos archivos sean únicos. Si se desinstala una instancia de SQL Server, se eliminan los archivos con la convención de nomenclatura tempdb_mssql_#.ndf. No use la convención de nomenclatura tempdb_mssql_\*.ndf con archivos de base de datos de usuario.<br /><br /> **\*\* Advertencia \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]no se puede usar para configurar este parámetro. El programa de instalación solamente instala un único archivo de datos de tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de datos de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64<br /><br /> Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Opcional**|Especifica el tamaño inicial en MB del archivo de registro de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB. Valor predeterminado:<br /><br /> 4 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 en todas las demás ediciones<br /><br /> Intervalo permitido: Mín. = valor predeterminado (4 u 8); Máx. = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de registro de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
##  <a name="Uninstall"></a> Parámetros de desinstalación  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la desinstalación. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la desinstalación.<br /><br /> Valores admitidos: **Uninstall**|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> **Obligatorio**|Especifica los [componentes](#Feature) que se van a desinstalar.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para desinstalar una instancia existente de SQL Server. 
  
```  
Setup.exe /Action=Uninstall /FEATURES=SQL,AS,RS,IS,Tools /INSTANCENAME=MSSQLSERVER  
```  
  
 Para quitar una instancia con nombre, especifique el nombre de la instancia en lugar de "MSSQLSERVER" en el ejemplo que se mencionó anteriormente en este tema. 
  
##  <a name="ClusterInstall"></a> Parámetros de clúster de conmutación por error  
 Antes de instalar una instancia en clúster de conmutación por error de SQL Server, revise los temas siguientes:  
  
-   [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [[Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)]
  
-   [Antes de instalar los clústeres de conmutación por error](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Todos los comandos de la instalación de un clúster de conmutación por error requieren un clúster de Windows subyacente. Todos los nodos que formarán parte de un clúster de conmutación por error de SQL Server deben formar parte del mismo clúster de Windows. 
  
 Pruebe y modifique los siguientes ejemplos de scripts de instalación de un clúster de conmutación por error para adaptarlos a las necesidades de su organización. 
  
#### <a name="integrated-install-failover-cluster-parameters"></a>Parámetros de clúster de conmutación por error de una instalación integrada  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la instalación de clúster de conmutación por error. 
  
 Para obtener más información sobre la instalación integrada, vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
> **NOTA:** Para agregar más nodos después de la instalación, use la acción [Agregar nodo](#AddNode). 
  
|Componente de SQL Server|Parámetro|Detalles|  
|-----------------------------------------|---------------|-------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación de clústeres de conmutación por error.<br /><br /> Valor admitido: **InstallFailoverCluster**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERGROUP<br /><br /> **Opcional**|Especifica el nombre del grupo de recursos que se va a usar para el clúster de conmutación por error de SQL Server. Puede ser el nombre de un grupo de clústeres existente o de uno nuevo.<br /><br /> Valor predeterminado:<br /><br /> SQL Server (\<NombreDeInstancia>)|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/*/UpdateEnabled*<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/*UpdateSource*<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> **Obligatorio**|Especifica los [componentes](#Feature) que se van a instalar.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 32 bits. Se admite únicamente en un sistema de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes específicos de la instancia.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> **Opcional**|Especifica un valor no predeterminado para un [InstanceID](#InstanceID).|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola estaría oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERDISKS<br /><br /> **Opcional**|Especifica la lista de discos compartidos que se van a incluir en el grupo de recursos del clúster de conmutación por error de SQL Server.<br /><br /> Valor predeterminado: la primera unidad se usa como unidad predeterminada en todas las bases de datos.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Obligatorio**|Especifica una dirección IP codificada. Las codificaciones están delimitadas por punto y coma (;) y siguen el formato \<tipo de IP>;\<dirección>;\<nombre de red>;\<máscara de subred>. Los tipos de direcciones IP admitidos incluyen DHCP, IPv4 e IPv6.<br />Puede especificar varias direcciones IP del clúster de conmutación por error separadas por un espacio. Vea los ejemplos siguientes:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Obligatorio**|Especifica el nombre de red del nuevo clúster de conmutación por error de SQL Server. El nombre se usa para identificar la nueva instancia del clúster de conmutación por error de SQL Server en la red.|  
|Agente SQL Server|/AGTSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta para el servicio Agente SQL Server.|  
|Agente SQL Server|/AGTSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta del servicio del Agente SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Valor predeterminado: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Especifica las credenciales de administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos temporales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\\ <INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica si el proveedor MSOLAP se puede ejecutar en proceso.<br /><br /> Valor predeterminado: 1=habilitado|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica el modo de servidor de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Los valores válidos en un escenario de clúster son MULTIDIMENSIONAL o TABULAR. **ASSERVERMODE** distingue entre mayúsculas y minúsculas. Todos los valores se deben expresar en mayúsculas. Para obtener más información acerca de los valores válidos, vea Instalar Analysis Services en modo Tabular.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Obligatorio**|Especifica el directorio de datos de los archivos de datos de SQL Server.<br /><br /> El directorio de datos se debe especificar en un disco de clúster compartido.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Obligatorio cuando /SECURITYMODE=SQL**|Especifica la contraseña de la cuenta de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica el modo de seguridad de SQL Server.<br /><br /> Si no se proporciona este parámetro, se admite el modo de autenticación solamente de Windows.<br /><br /> Valor admitido: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para SQL Server.<br /><br /> El valor predeterminado se basa en la configuración regional del sistema operativo Windows. Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio del servicio de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de SQLSVCACCOUNT.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Use este parámetro para proporcionar inicios de sesión que sean miembros del rol sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica los directorios de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Opcional**|Especifica el número de archivos de datos de tempdb que va a agregar el programa de instalación. Este valor se puede aumentar hasta el número de núcleos existente. Valor predeterminado:<br /><br /> 1 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 o el número de núcleos, lo que sea menor en todas las demás ediciones<br /><br /> **\*\* Importante \*\*** El archivo de base de datos principal para tempdb seguirá siendo tempdb.mdf. Los archivos de tempdb adicionales se denominarán tempdb_mssql_#.ndf, donde # es un número único para cada archivo de base de datos de tempdb extra creado durante la instalación. Lo que se persigue con esta convención de nomenclatura es que estos archivos sean únicos. Si se desinstala una instancia de SQL Server, se eliminan los archivos con la convención de nomenclatura tempdb_mssql_#.ndf. No use la convención de nomenclatura tempdb_mssql_\*.ndf con archivos de base de datos de usuario.<br /><br /> **\*\* Advertencia \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]no se puede usar para configurar este parámetro. El programa de instalación solamente instala un único archivo de datos de tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de datos de tempdb.<br/><br/>Valor predeterminado = 8 MB.<br/><br/>Mín. = 8 MB.<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64<br /><br /> Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Opcional**|Especifica el tamaño inicial en MB del archivo de registro de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB. <br /> Valor predeterminado:<br /><br /> 4 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 en todas las demás ediciones<br /><br /> Intervalo permitido: Mín. = valor predeterminado (4 u 8); Máx. = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de registro de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica el nivel de acceso de la característica FILESTREAM. Valores admitidos:<br /><br /> 0=Deshabilitar la compatibilidad de FILESTREAM con esta instancia. (Valor predeterminado)<br /><br /> 1=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] y a la transmisión por secuencias de E/S de archivos. (No es válido en escenarios de clúster)<br /><br /> 3=Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Obligatorio cuando FILESTREAMLEVEL es mayor que 1.**|Especifica el nombre del recurso compartido de Windows en el que se almacenarán los datos de FILESTREAM.|  
|Texto completo de SQL Server|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta para el servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. Se usará ServiceSID para asegurar la comunicación entre SQL Server y el demonio de filtro de texto completo.<br /><br /> Si no se proporcionan los valores, se deshabilitará el servicio iniciador de filtro de texto completo. Tiene que usar el Administrador de control de SQL Server para cambiar la cuenta del servicio y habilitar la funcionalidad de texto completo.<br /><br /> Valor predeterminado: cuenta de servicio local|  
|Texto completo de SQL Server|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña del servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Valor predeterminado: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Opcional**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña para la cuenta de inicio del servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 Recomendamos usar el SID de servicio en lugar de grupos de dominios. 
  
##### <a name="additional-notes"></a>Notas adicionales:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son los únicos componentes que son conscientes del clúster. Otras características no son conscientes del clúster y no tienen una alta disponibilidad mediante la conmutación por error. 
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para instalar una instancia en clúster de conmutación por error de SQL Server de nodo único con [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la instancia predeterminada. 
  
```  
setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="prepare-failover-cluster-parameters"></a>Preparar parámetros de clúster de conmutación por error  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para preparar el clúster de conmutación por error. Este es el primer paso de la instalación de clúster avanzada, donde tiene que preparar las instancias con clúster de conmutación por error en todos los nodos del clúster de conmutación por error. Para obtener más información, vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la preparación de clústeres de conmutación por error.<br /><br /> Valor admitido: **PrepareFailoverCluster**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/*/UpdateEnabled*<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/*UpdateSource*<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/FEATURES<br /><br /> **Obligatorio**|Especifica los [componentes](#Feature) que se van a instalar.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTALLSHAREDWOWDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos de 32 bits. Se admite únicamente en un sistema de 64 bits.<br /><br /> El valor predeterminado es %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server<br /><br /> No se puede establecer en %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server|  
|Control del programa de instalación de SQL Server|/INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes específicos de la instancia.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> **Opcional**|Especifica un valor no predeterminado para un [InstanceID](#InstanceID).|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro.<br /><br /> Se utiliza la evaluación.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Agente SQL Server|/AGTSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta para el servicio Agente SQL Server.|  
|Agente SQL Server|/AGTSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta del servicio del Agente SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio del servicio de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de SQLSVCACCOUNT.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Opcional**|Especifica el nivel de acceso de la característica FILESTREAM. Valores admitidos:<br /><br /> 0=Deshabilitar la compatibilidad de FILESTREAM con esta instancia. (Valor predeterminado)<br /><br /> 1=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> 2=Habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] y a la transmisión por secuencias de E/S de archivos. (No es válido en escenarios de clúster)<br /><br /> 3=Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Opcional**<br /><br /> **Obligatorio** cuando FILESTREAMLEVEL es mayor que 1.|Especifica el nombre del recurso compartido de Windows en el que se almacenarán los datos de FILESTREAM.|  
|Texto completo de SQL Server|/FTSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta para el servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]. Se usará ServiceSID para asegurar la comunicación entre SQL Server y el demonio de filtro de texto completo.<br /><br /> Si no se proporcionan los valores, se deshabilitará el servicio iniciador de filtro de texto completo. Tiene que usar el Administrador de control de SQL Server para cambiar la cuenta del servicio y habilitar la funcionalidad de texto completo.<br /><br /> Valor predeterminado: cuenta de servicio local|  
|Texto completo de SQL Server|/FTSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña del servicio de selector del filtro de texto completo.<br /><br /> Este parámetro se pasa por alto en [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)].|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Valor predeterminado: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponible únicamente en modo de solo archivos.**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña para la cuenta de inicio del servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
 Recomendamos usar el SID de servicio en lugar de grupos de dominios. 
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para realizar el paso de "preparación" del escenario de instalación avanzada de un clúster de conmutación por error para [!INCLUDE[ssDE](../../includes/ssde-md.md)] y para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
 Ejecute el comando siguiente en el símbolo del sistema para preparar una instancia predeterminada:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=MSSQLSERVER /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
 Ejecute el comando siguiente en el símbolo del sistema para preparar una instancia con nombre:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName="<Insert Instance name>" /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-failover-cluster-parameters"></a>Completar parámetros de clúster de conmutación por error  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para completar el clúster de conmutación por error. Se trata del segundo paso de la opción de instalación del clúster de conmutación por error. Cuando haya llevado a cabo la preparación en todos los nodos de clúster de conmutación por error, ejecute este comando en el nodo que posea los discos compartidos. Para obtener más información, vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo para completar los clústeres de conmutación por error.<br /><br /> Valor admitido: **CompleteFailoverCluster**|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERGROUP<br /><br /> **Opcional**|Especifica el nombre del grupo de recursos que se va a usar para el clúster de conmutación por error de SQL Server. Puede ser el nombre de un grupo de clústeres existente o de uno nuevo.<br /><br /> Valor predeterminado:<br /><br /> SQL Server (\<NombreDeInstancia>)|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 1=habilitado<br /><br /> 0=deshabilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERDISKS<br /><br /> **Opcional**|Especifica la lista de discos compartidos que se van a incluir en el grupo de recursos del clúster de conmutación por error de SQL Server.<br /><br /> Valor predeterminado:<br /><br /> La primera unidad se usa como la predeterminada para todas las bases de datos.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Obligatorio**|Especifica una dirección IP codificada. Las codificaciones están delimitadas por punto y coma (;) y siguen el formato \<tipo de IP>;\<dirección>;\<nombre de red>;\<máscara de subred>. Los tipos de direcciones IP admitidos incluyen DHCP, IPv4 e IPv6.<br />Puede especificar varias direcciones IP del clúster de conmutación por error separadas por un espacio. Vea los ejemplos siguientes:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Obligatorio**|Especifica el nombre de red del nuevo clúster de conmutación por error de SQL Server. El nombre se usa para identificar la nueva instancia del clúster de conmutación por error de SQL Server en la red.|  
|Control del programa de instalación de SQL Server|/CONFIRMIPDEPENDENCYCHANGE|Indica el consentimiento para establecer la dependencia de recurso de dirección IP de los clústeres de conmutación por error de varias subredes. Para obtener más información, vea [Crear un nuevo clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md). Valores admitidos:<br /><br /> 0 = False (predeterminado)<br /><br /> 1 = True|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Valor predeterminado: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Archivos de programa(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.<br /><br /> Para todas las demás instalaciones: %Archivos de programa%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log.<br /><br /> Para todas las demás instalaciones: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Opcional**|Especifica el modo de servidor de la instancia de Analysis Services. Los valores válidos en un escenario de clúster son MULTIDIMENSIONAL o TABULAR. **ASSERVERMODE** distingue entre mayúsculas y minúsculas. Todos los valores se deben expresar en mayúsculas. Para obtener más información acerca de los valores válidos, vea Instalar Analysis Services en modo Tabular.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Especifica las credenciales de administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos temporales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Valores predeterminados:<br /><br /> Para el modo WOW en 64 bits: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp.<br /><br /> Para todas las demás instalaciones: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Opcional**|Especifica si el proveedor MSOLAP se puede ejecutar en proceso.<br /><br /> Valor predeterminado: 1=habilitado|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Obligatorio**|Especifica el directorio de datos de los archivos de datos de SQL Server.<br /><br /> El directorio de datos se debe especificar en un disco de clúster compartido.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Obligatorio cuando /SECURITYMODE=SQL**|Especifica la contraseña de la cuenta de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Opcional**|Especifica el modo de seguridad de SQL Server.<br /><br /> Si no se proporciona este parámetro, se admite el modo de autenticación solamente de Windows.<br /><br /> Valor admitido: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de copia de seguridad.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Backup.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Opcional**|Especifica la configuración de la intercalación para SQL Server.<br /><br /> El valor predeterminado se basa en la configuración regional del sistema operativo Windows. Para obtener más información, vea [Configuración de intercalación en el programa de instalación](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Obligatorio**|Use este parámetro para proporcionar inicios de sesión que sean miembros del rol sysadmin.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de datos de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de las bases de datos de usuario.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponible en modo de solo archivos.**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Opcional**|Especifica los directorios de los archivos de datos de tempdb. Si especifica varios directorios, sepárelos con un espacio en blanco. Si se especifican varios directorios, los archivos de datos de tempdb se distribuirán por turnos entre los directorios.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Opcional**|Especifica el directorio de los archivos de registro de tempdb.<br /><br /> Valor predeterminado: \<directorioDatosSQLInstalación>\ \<IdInstanciaSQL>\MSSQL\Data(System Data Directory)<br /><br /> Nota: este parámetro también se agrega al escenario de RebuildDatabase.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Opcional**|Especifica el número de archivos de datos de tempdb que va a agregar el programa de instalación. Este valor se puede aumentar hasta el número de núcleos existente. Valor predeterminado:<br /><br /> 1 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 o el número de núcleos, lo que sea menor en todas las demás ediciones.<br /><br /> **\*\* Importante \*\*** El archivo de base de datos principal para tempdb seguirá siendo tempdb.mdf. Los archivos de tempdb adicionales se denominarán tempdb_mssql_#.ndf, donde # es un número único para cada archivo de base de datos de tempdb extra creado durante la instalación. Lo que se persigue con esta convención de nomenclatura es que estos archivos sean únicos. Si se desinstala una instancia de SQL Server, se eliminan los archivos con la convención de nomenclatura tempdb_mssql_#.ndf. No use la convención de nomenclatura tempdb_mssql_\*.ndf con archivos de base de datos de usuario.<br /><br /> **\*\* Advertencia \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]no se puede usar para configurar este parámetro. El programa de instalación solamente instala un único archivo de datos de tempdb.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de datos de tempdb.<br/><br/>Valor predeterminado = 8 MB.<br/><br/>Mín. = 8 MB.<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)]).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Opcional**|Especifica el incremento de crecimiento de archivo en MB de cada archivo de datos de tempdb. El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio. El programa de instalación permite que el tamaño alcance los 1024 MB.<br /><br /> Valor predeterminado: 64<br /><br /> Rango permitido: Mín. = 0, Máx. = 1024.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Opcional**|Especifica el tamaño inicial en MB del archivo de registro de tempdb. El programa de instalación permite que el tamaño alcance los 1024 MB. <br /> Valor predeterminado:<br /><br /> 4 en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 en todas las demás ediciones<br /><br /> Intervalo permitido: Mín. = valor predeterminado (4 u 8); Máx. = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Opcional**|Incluido en [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)]. Especifica el tamaño inicial de cada archivo de registro de tempdb.<br/><br/>Valor predeterminado = 4 MB en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; 8 MB en el resto de ediciones.<br/><br/>Mín. = (4 u 8 MB).<br/><br/>Máx. = 1024 MB (262 144 MB en [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para realizar el paso de "conclusión" del escenario de instalación avanzada de un clúster de conmutación por error para [!INCLUDE[ssDE](../../includes/ssde-md.md)] y para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Ejecute el comando siguiente en el equipo que será el nodo activo del clúster de conmutación por error para que pueda usarse. Debe ejecutar la acción "CompleteFailoverCluster" en el nodo que posee el disco compartido en el clúster de conmutación por error de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . 
  
 Ejecute el comando siguiente en el símbolo del sistema para completar la instalación del clúster de conmutación por error para una instancia predeterminada:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\Username>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
```  
  
 Ejecute el comando siguiente en el símbolo del sistema para completar la instalación del clúster de conmutación por error para una instancia con nombre:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName="<Insert Instance Name>" /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\KATMAI\Data /ASLOGDIR=<drive>:\KATMAI\Log /ASBACKUPDIR=<Drive>:\KATMAI\Backup /ASCONFIGDIR=<Drive>:\KATMAI\Config /ASTEMPDIR=<Drive>:\KATMAI\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>" /FAILOVERCLUSTERNETWORKNAME="CompNamedFOI" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="<Insert New Group Name>" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER_KATMAI" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\Username>"  
```  
  
#### <a name="upgrade-failover-cluster-parameters"></a>Actualizar parámetros de clúster de conmutación por error  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para la actualización del clúster de conmutación por error. Para obtener más información, vea [Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de la instalación.<br /><br /> Valor admitido: **Upgrade**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/*/UpdateEnabled*<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/*UpdateSource*<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/ERRORREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. <br/><br/>Para administrar cómo se envían los comentarios sobre errores a Microsoft, consulte [Cómo configurar SQL Server 2016 para enviar comentarios a Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>En versiones anteriores, especifica el informe de errores de SQL Server.<br /><br /> Para obtener más información, vea [Declaración de privacidad de Microsoft Error Reporting Service](http://go.microsoft.com/fwlink/?LinkID=72173). Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/ INSTANCEDIR<br /><br /> **Opcional**|Especifica un directorio de instalación no predeterminado para los componentes compartidos.|  
|Control del programa de instalación de SQL Server|/INSTANCEID<br /><br /> **Obligatorio cuando se actualiza desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores.**<br /><br /> **Opcional cuando se actualiza desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Especifica un valor no predeterminado para un [InstanceID](#InstanceID).|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/SQMREPORTING<br /><br /> **Opcional**|No tiene ningún efecto en SQL Server 2016. En versiones anteriores, especifica la notificación del uso de características para SQL Server.<br /><br />Valores admitidos:<br /><br /> 0=deshabilitado<br /><br /> 1=habilitado|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERROLLOWNERSHIP|Especifica el [comportamiento de conmutación por error](#RollOwnership) durante la actualización.|  
|Servicio SQL Server Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio SQL Server Browser. Valores admitidos:<br /><br /> **Automático**<br /><br /> **Deshabilitado**<br /><br /> **Manual**|  
|Texto completo de SQL Server|/FTUPGRADEOPTION<br /><br /> **Opcional**|Especifica la opción de actualización del catálogo de texto completo. Valores admitidos:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].<br /><br /> Valor predeterminado: NT AUTHORITY\NETWORK SERVICE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Opcional**|Especifica el modo de [inicio](#Accounts) del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Opcional**|La propiedad solo se utiliza al actualizar un servidor de informes en modo de SharePoint que sea de la versión 2008 R2 o anterior. Las operaciones adicionales de actualización se realizan en los servidores de informes que utilizan la arquitectura en modo de SharePoint más antigua, que se cambió en SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si esta opción no se incluye con la instalación de línea de comandos, la cuenta de servicio predeterminada se utiliza para la antigua instancia del servidor de informes. Si se usa esta propiedad, proporcione la contraseña de la cuenta mediante la propiedad **/RSUPGRADEPASSWORD** .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Opcional**|Contraseña de la cuenta de servicio del Servidor de informes existente.|  
  
####  <a name="AddNode"></a> Parámetros de Add Node  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para AddNode. 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de AddNode.<br /><br /> Valor admitido: **AddNode**|  
|Control del programa de instalación de SQL Server|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.**|Obligatorio para confirmar la aceptación de los términos de licencia.|  
|Control del programa de instalación de SQL Server|/ENU<br /><br /> **Opcional**|Use este parámetro para instalar la versión en inglés de SQL Server en un sistema operativo localizado cuando el disco de instalación incluya paquetes de idioma tanto para inglés como para el idioma correspondiente al sistema operativo.|  
|Control del programa de instalación de SQL Server|/*/UpdateEnabled*<br /><br /> **Opcional**|Especifique si el programa de instalación de SQL Server debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de SQL Server incluirá las actualizaciones que encuentre.|  
|Control del programa de instalación de SQL Server|/*UpdateSource*<br /><br /> **Opcional**|Especifique la ubicación en que el programa de instalación de SQL Server obtendrá las actualizaciones del producto. Los valores válidos son "MU" para buscar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, una ruta de acceso de carpeta válida, una ruta relativa, como .\MyUpdates o un recurso compartido UNC. De manera predeterminada, el programa de instalación de SQL Server buscará en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update o en el Servicio Windows Update a través de Windows Server Update Services.|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Opcional**|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Opcional**|Especifica la contraseña de la cuenta del servicio de motor.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Opcional**|Especifica el modo de inicio del servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Opcional**|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Opcional**|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. Valores admitidos: **True**, **False**.|  
|Control del programa de instalación de SQL Server|/PID<br /><br /> **Opcional**|Especifica la clave del producto para la edición de SQL Server. Si no se especifica este parámetro, se utiliza Evaluation.|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Obligatorio**|Especifica una dirección IP codificada. Las codificaciones están delimitadas por punto y coma (;) y siguen el formato \<tipo de IP>;\<dirección>;\<nombre de red>;\<máscara de subred>. Los tipos de direcciones IP admitidos incluyen DHCP, IPv4 e IPv6.<br />Puede especificar varias direcciones IP del clúster de conmutación por error separadas por un espacio. Vea los ejemplos siguientes:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1<br /><br /> <br /><br /> Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).|  
|Control del programa de instalación de SQL Server|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Obligatorio**|Indica el consentimiento para establecer la dependencia de recurso de dirección IP de los clústeres de conmutación por error de varias subredes. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Valores admitidos:<br /><br /> 0 = False (predeterminado)<br /><br /> 1 = True|  
|Agente SQL Server|/AGTSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta para el servicio Agente SQL Server.|  
|Agente SQL Server|/AGTSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de la cuenta del servicio del Agente SQL Server.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Obligatorio**|Especifica la cuenta de inicio del servicio de SQL Server.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de SQLSVCACCOUNT.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Disponible en modo de solo archivos**|Especifica el modo de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Obligatorio](#Accounts)|Especifica la contraseña de cuenta de inicio para el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
##### <a name="additional-notes"></a>Notas adicionales:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son los únicos componentes que son conscientes del clúster. Otras características no son conscientes del clúster y no tienen una alta disponibilidad mediante la conmutación por error. 
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para agregar un nodo a una instancia en clúster de conmutación por error existente con [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
```  
setup.exe /q /ACTION=AddNode /INSTANCENAME="<Insert Instance Name>" /SQLSVCACCOUNT="<SQL account that is used on other nodes>" /SQLSVCPASSWORD="<password for SQL account>" /AGTSVCACCOUNT="<SQL Server Agent account that is used on other nodes>", /AGTSVCPASSWORD="<SQL Server Agent account password>" /ASSVCACCOUNT="<AS account that is used on other nodes>" /ASSVCPASSWORD=”<password for AS account>” /INDICATEPROGRESS /IACCEPTSQLSERVERLICENSETERMS /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
#### <a name="remove-node-parameters"></a>Parámetros de RemoveNode  
 Use los parámetros de la tabla siguiente para desarrollar scripts de la línea de comandos para RemoveNode. Para desinstalar un clúster de conmutación por error, debe ejecutar RemoveNode en cada nodo de clúster de conmutación por error. Para obtener más información, vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|Componente de SQL Server|Parámetro|Description|  
|-----------------------------------------|---------------|-----------------|  
|Control del programa de instalación de SQL Server|/ACTION<br /><br /> **Obligatorio**|Obligatorio para indicar el flujo de trabajo de RemoveNode.<br /><br /> Valor admitido: **RemoveNode**|  
|Control del programa de instalación de SQL Server|/CONFIGURATIONFILE<br /><br /> **Opcional**|Especifica el [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) que se va a usar.|  
|Control del programa de instalación de SQL Server|/HELP, H, ?<br /><br /> **Opcional**|Muestra las opciones de uso para los parámetros.|  
|Control del programa de instalación de SQL Server|/INDICATEPROGRESS<br /><br /> **Opcional**|Especifica que el archivo de registro detallado del programa de instalación se canalizará a la consola.|  
|Control del programa de instalación de SQL Server|/INSTANCENAME<br /><br /> **Obligatorio**|Especifica un nombre de instancia de SQL Server.<br /><br /> Para obtener más información, vea [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|Control del programa de instalación de SQL Server|/Q<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute en modo silencioso sin ninguna interfaz de usuario. Se usa en las instalaciones desatendidas.|  
|Control del programa de instalación de SQL Server|/QS<br /><br /> **Opcional**|Especifica que el programa de instalación se ejecute y muestre el progreso a través de la interfaz de usuario, pero no acepte ninguna entrada ni muestre ningún mensaje de error.|  
|Control del programa de instalación de SQL Server|/HIDECONSOLE<br /><br /> **Opcional**|Especifica que la ventana de la consola está oculta o cerrada.|  
|Control del programa de instalación de SQL Server|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Obligatorio**|Indica el consentimiento para establecer la dependencia de recurso de dirección IP de y para los clústeres de conmutación por error de varias subredes. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Valores admitidos:<br /><br /> 0 = False (predeterminado)<br /><br /> 1 = True|  
  
###### <a name="sample-syntax"></a>Sintaxis de ejemplo:  
 Para eliminar un nodo de una instancia en clúster de conmutación por error existente con [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 
  
```  
setup.exe /q /ACTION=RemoveNode /INSTANCENAME="<Insert Instance Name>" [/INDICATEPROGRESS] /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
##  <a name="Accounts"></a> Parámetros de cuenta de servicio  
 Puede configurar los servicios de SQL Server usando una cuenta integrada, una cuenta local o una cuenta de dominio. 
  
> **NOTA:** Si usa una cuenta de servicio administrada, una cuenta virtual o una cuenta integrada, no debe especificar los parámetros correspondientes de la contraseña. Para obtener más información sobre estas cuentas de servicio, vea la sección **Nuevos tipos de cuenta disponibles con [!INCLUDE[win7](../../includes/win7-md.md)] y [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]** en [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
 Para obtener más información sobre la configuración de la cuenta de servicio, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
|Componente de SQL Server|Parámetro de cuenta|Parámetro de contraseña|Tipo de inicio|  
|-----------------------------------------|-----------------------|------------------------|------------------|  
|Agente SQL Server|/AGTSVCACCOUNT|/AGTSVCPASSWORD|/AGTSVCSTARTUPTYPE|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT|/ASSVCPASSWORD|/ASSVCSTARTUPTYPE|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT|/SQLSVCPASSWORD|/SQLSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT|/ISSVCPASSWORD|/ISSVCStartupType|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT|/RSSVCPASSWORD|/RSSVCStartupType|  
  
##  <a name="Feature"></a> Parámetros de características  
 Para instalar características específicas, use el parámetro /FEATURES y especifique la característica principal o los valores de características principales de la tabla siguiente. Para obtener una lista de las características admitidas por las ediciones de SQL Server, vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). 
  
|Parámetro de característica principal|Parámetro de característica|Description|  
|:---|:---|:---|  
|SQL||Instala los componentes [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replicación, Texto completo y [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].|  
||SQLEngine|Instala solamente [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||Replicación|Instala el componente Replicación junto con [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||FullText|Instala el componente Texto completo junto con el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||DQ|Copia los archivos requeridos para completar la instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Tras finalizar la instalación de SQL Server, debe ejecutar el archivo DQSInstaller.exe para completar la instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Para obtener más información, vea [Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md). Esto también instala [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||PolyBase|Instala los componentes de PolyBase.|  
||AdvancedAnalytics|Instala R Services (en bases de datos).|  
|AS||Instala todos los componentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|RS||Instala todos los componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|RS_SHP||Instala componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint.|  
|RS_SHPWFE||Instala el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint. |  
|DQC||Instala [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].|  
|IS||Instala todos los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|MDS||Instala [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|  
|SQL_SHARED_MR||Instala Microsoft R Server.|  
|Herramientas*||Instala las herramientas de cliente y los componentes de los Libros en pantalla de SQL Server.|  
||BC|Instala los componentes de compatibilidad con versiones anteriores.|  
||Conn|Instala los componentes de conectividad.|
||DREPLAY_CTLR|Instala Distributed Replay Controller|  
||DREPLAY_CLT|Instala el cliente de Distributed Replay Client|  
||SNAC_SDK|Instala el SDK para [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server Native Client|  
||SDK|Instala el kit de desarrollo de software.|  
||LocalDB**|Instala LocalDB, un modo de ejecución de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a los desarrolladores de programas.|  

*Herramientas de administración de SQL Server (SSMS) está ahora en un instalador aparte que es independiente del instalador de SQL Server. Para obtener más información, vea la sección sobre cómo [instalar SQL Server Management Studio desde la línea de comandos](https://msdn.microsoft.com/library/bb500441.aspx#Anchor_1).

 **LocalDB es una opción al instalar cualquier SKU de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express. Para obtener más información, vea [SQL Server 2016 Express LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). 
  
### <a name="feature-parameter-examples"></a>Ejemplos de parámetros de características:  
  
|Parámetro y valores|Description|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Instala [!INCLUDE[ssDE](../../includes/ssde-md.md)] sin Replicación ni Texto completo.|  
|/FEATURES=SQLEngine, FullText|Instala [!INCLUDE[ssDE](../../includes/ssde-md.md)] y Texto completo.|  
|/FEATURES=SQL, Tools|Instala [!INCLUDE[ssDE](../../includes/ssde-md.md)] completo y todas las herramientas.|  
|/FEATURES=BOL|Instala los componentes de los Libros en pantalla de SQL Server para ver y administrar el contenido de la Ayuda.|  
|/FEATURES=SQLEngine, PolyBase|Instala el motor de PolyBase.|  
  
##  <a name="RoleParameters"></a> Parámetros de rol  
 El rol de instalación o el parámetro /Role se utiliza para instalar una selección preconfigurada de características. Los roles de [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] instalan una instancia de [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] en una granja de SharePoint existente o en una nueva granja sin configurar. Se proporcionan dos roles de instalación para ser compatibles con cada escenario. Puede elegir solo un rol de instalación que instalar a la vez. Si elige un rol de instalación, el programa de instalación instala las características y componentes que pertenecen al rol. No puede variar las características y los componentes que están designados para ese rol. Para obtener más información sobre cómo usar el parámetro de roles de características, vea [Instalar PowerPivot desde el símbolo del sistema](http://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328). 
  
 El rol AllFeatures_WithDefaults es el comportamiento predeterminado para las ediciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] y reduce el número de cuadros de diálogo que se presentan al usuario. Se puede especificar desde la línea de comandos al instalar una edición de SQL Server diferente de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. 
  
|Rol|Description|Instala...|  
|----------|-----------------|---------------|  
|SPI_AS_ExistingFarm|Instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como una instancia con nombre de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja de [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] existente o en un servidor independiente.|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] motor de cálculo preconfigurado para el procesamiento y el almacenamiento de datos en memoria.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] paquetes de solución<br /><br /> Programa de instalador para [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]<br /><br /> SQL Server, Libros en pantalla|  
|SPI_AS_NewFarm|Instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssDE](../../includes/ssde-md.md)] como una instancia con nombre de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una nueva granja de Office [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] sin configurar o en un servidor independiente. El programa de instalación de SQL Server configurará la granja durante la instalación de los roles de características.|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] motor de cálculo preconfigurado para el procesamiento y el almacenamiento de datos en memoria.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] paquetes de solución<br /><br /> SQL Server, Libros en pantalla<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> Herramientas de configuración<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|AllFeatures_WithDefaults|Instala todas las características que están disponibles con la edición actual.<br /><br /> Agrega el usuario actual al rol fijo de servidor **sysadmin** de SQL Server.<br /><br /> En [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] o versiones posteriores, y cuando el sistema operativo no sea un controlador de dominio, [!INCLUDE[ssDE](../../includes/ssde-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se establecen de forma predeterminada para utilizar la cuenta de servicio NTAUTHORITY\NETWORK, e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se establece de forma predeterminada para utilizar la cuenta de servicio NTAUTHORITY\NETWORK.<br /><br /> Este rol está habilitado de forma predeterminada en ediciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Para todas las demás ediciones, este rol no se habilita, pero se puede especificar a través de la interfaz de usuario o con parámetros de la línea de comandos.|Para las ediciones de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], solo instala las características disponibles en la edición. Para otras ediciones, instala todas las características de SQL Server.<br /><br /> El parámetro **AllFeatures_WithDefaults** se puede combinar con otros parámetros que invalidan la configuración del parámetro **AllFeatures_WithDefaults** . Por ejemplo, si se usa el parámetro **AllFeatures_WithDefaults** y el parámetro **/Features=RS** , se invalida el comando para instalar todas las características y solo se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], pero se sigue el parámetro **AllFeatures_WithDefaults** y se utiliza la cuenta de servicio predeterminada para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Al usar el parámetro **AllFeatures_WithDefaults** junto con **/ADDCURRENTUSERASSQLADMIN=FALSE** , el cuadro de diálogo de aprovisionamiento no se rellena automáticamente con el usuario actual. Agregue **/AGTSVCACCOUNT** y **/AGTSVCPASSWORD** para especificar una cuenta de servicio y una contraseña para el Agente SQL Server.|  
  
##  <a name="RollOwnership"></a> Controlar el comportamiento de la conmutación por error con el parámetro /FAILOVERCLUSTERROLLOWNERSHIP  
 Para actualizar un clúster de conmutación por error de SQL Server a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], debe ejecutar el programa de instalación en un nodo de clúster de conmutación por error cada vez, comenzando por los nodos pasivos. El programa de instalación muestra el comportamiento de conmutación por error, en función del número total de nodos de la instancia en clúster de conmutación por error y del número total de nodos que ya se han actualizado. Cuando se ha actualizado la mitad de los nodos o más, el programa de instalación realiza una conmutación por error a un nodo actualizado. 
  
 Para controlar el comportamiento de los nodos de clúster durante el proceso de actualización, ejecute la operación de actualización en el símbolo del sistema y use el parámetro /FAILOVERCLUSTERROLLOWNERSHIP para controlar el comportamiento de la conmutación por error antes de que la operación de actualización deje el nodo sin conexión. Este parámetro se usa como se indica a continuación:  
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=0 no transmitirá la propiedad del clúster (moverá el grupo) a los nodos actualizados y no agregará este nodo a la lista de posibles propietarios del clúster de SQL Server al final de la actualización. 
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=1 transmitirá la propiedad del clúster (moverá el grupo) a los nodos actualizados y agregará este nodo a la lista de posibles propietarios del clúster de SQL Server al final de la actualización. 
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=2 es la configuración predeterminada. Se usará si no se especifica este parámetro. Este valor indica que el programa de instalación de SQL Server administrará la propiedad del clúster (mueve el grupo) según sea necesario. 
  
##  <a name="InstanceID"></a> Configuración de identificador de instancia o InstanceID  
 El parámetro Instance ID o /InstanceID se usa para especificar dónde puede instalar los componentes de la instancia y la ruta de acceso del Registro de la instancia. El valor de "INSTANCEID" es una cadena y debe ser único. 
  
-   SQL Instance ID:MSSQL13.\<INSTANCEID>  
  
-   AS Instance ID:MSAS13.\<INSTANCEID>  
  
-   RS Instance ID:MSRS13.\<INSTANCEID>  
  
 Los componentes que tienen en cuenta la instancia se instalan en las ubicaciones siguientes:  
  
 %Archivos de programa%\\Microsoft SQL Server\\<SQLInstanceID\>  
  
 %Archivos de programa%\\Microsoft SQL Server\\<ASInstanceID\>  
  
 %Archivos de programa Microsoft SQL Server\\<RSInstanceID\>  
  
> **NOTA:** Si INSTANCEID no se especifica en la línea de comandos, el programa de instalación sustituye de forma predeterminada \<INSTANCEID> por \<INSTANCENAME>. 
  
## <a name="see-also"></a>Vea también  
 [Instalación de SQL Server 2016 desde el Asistente para la instalación](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [[Instalar las características de SQL Server 2016 Business Intelligence](../../sql-server/install/install-sql-server-business-intelligence-features.md)]  
  
