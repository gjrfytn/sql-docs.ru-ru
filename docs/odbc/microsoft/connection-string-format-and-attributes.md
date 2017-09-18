---
title: "Формат строки соединения и атрибуты | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79d5cabb884262b052429da53cf19c360048dd21
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-format-and-attributes"></a>Формат строки соединения и атрибуты
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Вместо этого используйте драйвер ODBC, предоставляемого корпорацией Oracle.  
  
 Вместо того чтобы использовать диалоговое окно, некоторых приложений может потребоваться строка подключения, указывающая о соединении с источником данных. Строка подключения состоит из ряд атрибутов, которые определяют, как драйвер подключается к источнику данных. Атрибут определяет некоторой части сведений, которые необходимо знать, чтобы сделать подключение к источнику данных соответствующий драйвер. Каждый драйвер может иметь разный набор атрибутов, но формат строки соединения не изменяется. Строка подключения имеет следующий формат:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Драйвер Microsoft ODBC для Oracle поддерживает формат строки подключения первой версии драйвера, который используется `CONNECTSTRING`= вместо `SERVER=`.  
  
 Если вы подключаетесь к поставщик источника данных, который поддерживает проверку подлинности Windows, следует указать `Trusted_Connection=yes` вместо идентификатора и пароля пользователя в строке подключения.  
  
 Необходимо указать источник данных именем, если вы не укажете UID, PWD, сервер (или CONNECTSTRING) и атрибутов ДРАЙВЕРА. Тем не менее все остальные атрибуты являются необязательными. Если атрибут не задан, этот атрибут по умолчанию в соответствии с указанной на вкладке соответствующие DSN **администратор источников данных ODBC** диалоговое окно. Значение атрибута может быть с учетом регистра.  
  
 Атрибуты для строки подключения будет следующим:  
  
|Attribute|Description|Значение по умолчанию|  
|---------------|-----------------|-------------------|  
|DSN|Имя источника данных, указанных на вкладке драйверов из **администратор источников данных ODBC** диалоговое окно.|""|  
|PWD|Пароль для сервера Oracle, необходимо получить доступ. Этот драйвер поддерживает ограничения, которые Oracle помещает пароли.|""|  
|SERVER|Строка соединения для сервера Oracle, необходимо получить доступ.|""|  
|UID|Имя пользователя сервера Oracle. В зависимости от вашей системе, этот атрибут может быть необязательным — то есть некоторые базы данных и таблицы этого атрибута требуется в целях безопасности.<br /><br /> Используйте «/» для использования Oracle операционной системы проверки подлинности.|""|  
|BUFFERSIZE|Оптимальный размер буфера при получении столбцов.<br /><br /> Процесс загрузки настраивается таким образом, одну загрузку сервер Oracle возвращал достаточно строк, чтобы заполнить буфер такого размера. Как правило, большие значения для повышения производительности при загрузке большого объема данных.|65535|  
|SYNONYMCOLUMNS|Если это значение равно true (1) вызов SQLColumn API () возвращает сведения о столбце. В противном случае SQLColumn () возвращает только те столбцы для таблиц и представлений. Если этот флажок не установлен, драйвер ODBC для Oracle обеспечивает более быстрый доступ.|1|  
|REMARKS|Если это значение равно true (1), драйвер возвращает столбцы примечания для [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) результирующего набора. Если этот флажок не установлен, драйвер ODBC для Oracle обеспечивает более быстрый доступ.|0|  
|StdDayOfWeek|Обеспечивает стандарт ODBC для скалярных DAYOFWEEK. По умолчанию это включена, но пользователям необходимо локализованной версии можно изменить поведение, используемое возвращаемого Oracle.|1|  
|GuessTheColDef|Указывает, возвращать ли драйвер ненулевое значение для *cbColDef* аргумент **SQLDescribeCol**. Применяется только к столбцам, где есть нет Oracle масштаба, например вычисляемые числовые столбцы и столбцы, определенные в виде ЧИСЛА без указания точности или масштаба. Объект **SQLDescribeCol** вызов возвращает 130 для точности при Oracle не предоставляет эту информацию.|0|  
  
 Например строки подключения, которая подключается к источнику данных MyDataSource, с помощью сервера MyOracleServerOracle и MyUserID пользователя Oracle будет:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Строки подключения, которая подключается к источнику данных MyOtherDataSource, используя проверку подлинности операционной системы и сервера MyOtherOracleServerOracle будет:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```