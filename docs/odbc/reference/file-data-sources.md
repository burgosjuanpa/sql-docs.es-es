---
title: Orígenes de datos de archivos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25be6ea116b5449de55aeb8a16ed1cf12e1ce418
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="file-data-sources"></a>Orígenes de datos de archivo
*Orígenes de datos de archivos* se almacenan en un archivo y permitir que la información de conexión para utilizarse varias veces por un único usuario o compartir entre varios usuarios. Cuando se utiliza un origen de datos de archivo, el Administrador de controladores realiza la conexión al origen de datos con la información de un archivo de DSN. Este archivo se puede manipular como cualquier otro archivo. Un origen de datos de archivo no tiene un nombre de origen de datos, tal y como hace un origen de datos de la máquina y no está registrado en cualquier máquina o un usuario.  
  
 Un origen de datos de archivos simplifica el proceso de conexión, porque el archivo .dsn contiene la cadena de conexión que lo contrario, tendría que se crea para una llamada a la **SQLDriverConnect** función. Otra ventaja del archivo .dsn es que se puede copiar a cualquier máquina, por lo que los orígenes de datos idénticos pueden usa muchas máquinas siempre que tienen instalado el controlador apropiado. Un origen de datos de archivo también puede compartirse entre aplicaciones. Un origen de datos de archivo que se pueda compartir puede colocarse en una red y utilizar simultáneamente varias aplicaciones.  
  
 También se pueden compartir un archivo de DSN. Un archivo no se puede compartir .dsn reside en un único equipo y apunta a un origen de datos de la máquina. Orígenes de datos de archivo no se puede compartir existen principalmente para permitir la conversión sencilla de orígenes de datos de máquina a orígenes de datos de archivo para que una aplicación puede estar diseñada para que funcione únicamente con orígenes de datos de archivo. Cuando el Administrador de controladores se envía la información en un origen de datos de archivo no se puede compartir, conecta según sea necesario para el origen de datos de máquina que el archivo .dsn apunta a.  
  
 Para obtener más información acerca de los orígenes de datos de archivo, consulte [conectar orígenes de datos de archivo utilizando](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), o la [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.
