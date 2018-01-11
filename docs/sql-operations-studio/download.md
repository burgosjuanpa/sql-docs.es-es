---
title: "Descargue e instale Microsoft SQL operaciones Studio (versión preliminar) | Documentos de Microsoft"
description: "Descargue e instale Microsoft SQL operaciones Studio (versión preliminar) para Windows, Mac OS o Linux"
ms.custom: tools|sos
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a34a03b447e26f072b6c8064cd115333600fef4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="download-and-install-sql-operations-studio-preview"></a>Descargue e instale las operaciones de SQL Studio (versión preliminar)

[!INCLUDE[name-sos](../includes/name-sos.md)]se ejecuta en Windows, Mac OS y Linux.

Descargue e instale la versión más reciente, la *diciembre Public Preview*:

|Plataforma|Descargar|Fecha de lanzamiento|
|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=865305)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=865304)|19 de diciembre de 2017 |
|MacOS|[.zip](https://go.microsoft.com/fwlink/?linkid=865306)|19 de diciembre de 2017 |
|Linux|[.DEB](https://go.microsoft.com/fwlink/?linkid=865308)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=865309)<br>[. tar.gz](https://go.microsoft.com/fwlink/?linkid=865307)|19 de diciembre de 2017|

Para obtener más información acerca de la versión más reciente, consulte el [notas de la versión](release-notes.md).

## <a name="get-sql-operations-studio-preview-for-windows"></a>Obtener operaciones de SQL Studio (versión preliminar) para Windows

Esta versión de [!INCLUDE[name-sos](../includes/name-sos-short.md)] incluye una experiencia de instalador de Windows estándar y .zip: 

**Instalador**

1. Descargue y ejecute la [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] instalador para Windows](https://go.microsoft.com/fwlink/?linkid=865305).
1. Iniciar el [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] aplicación.


**archivo .zip**

1. Descargar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip para Windows](https://go.microsoft.com/fwlink/?linkid=865304).
2. Busque el archivo descargado y extráigalo.
3. Ejecutar`\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>Obtener operaciones de SQL Studio (versión preliminar) para macOS

1. Descargar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=865306).
2. Para expandir el contenido del archivo zip, haga doble clic en él.
3. Para realizar [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponibles en la *Launchpad*, arrastre *sqlops.app* a la *aplicaciones* carpeta.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Obtener operaciones de SQL Studio (versión preliminar) para Linux

1. Descargar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux](https://go.microsoft.com/fwlink/?linkid=865307).
1. Para extraer el archivo e inicie [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra una nueva ventana de Terminal y escriba los siguientes comandos:

   ```bash
   cd ~
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~
   tar -xvf ~/sqlops-linux-<version string>.tar.gz
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   sqlops
   ```

   > [!NOTE]
   > En Ubuntu y Redhat, puede tener dependencias que faltan. Use los comandos siguientes para instalar estas dependencias según su versión de Linux:
   
   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

   **RedHat:** 
   ```bash
   yum install libXScrnSaver
   ```

## <a name="uninstall-sql-operations-studio-preview"></a>Desinstalar Studio de operaciones de SQL (vista previa)

Si instaló [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] mediante el instalador de Windows, a continuación, desinstale la misma manera que quite cualquier aplicación de Windows.

Si instaló [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] con .zip o en otro archivo, a continuación, elimine los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

[!INCLUDE[name-sos](../includes/name-sos-short.md)]se ejecuta en Windows, Mac OS y Linux y es compatible con las siguientes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requiere Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>MacOS
- macOS 10.13 Sierra alta
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04



## <a name="next-steps"></a>Next Steps

Vea uno de los tutoriales siguientes para empezar a trabajar:
- [Conectar & consultas SQL Server](quickstart-sql-server.md)
- [Conectarse y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectarse y consultar el almacenamiento de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) y [la recopilación de datos de uso](usage-data-collection.md).