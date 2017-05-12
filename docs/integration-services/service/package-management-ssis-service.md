---
title: "Управление пакетами (службы SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "пакеты служб SQL Server Integration Services, управление"
  - "пакеты [службы Integration Services], управление"
  - "пакеты служб Integration Services, управление"
  - "хранение пакетов"
  - "папка «Хранимые пакеты»"
  - "текущие пакеты"
  - "папка «Выполняющиеся пакеты»"
  - "сведения о состоянии [службы Integration Services]"
  - "пакеты служб SSIS, управление"
  - "хранилище [службы Integration Services]"
  - "мониторинг [службы Integration Services], пакеты"
  - "службы Integration Services, управление пакетами"
  - "службы [службы Integration Services], управление пакетами"
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Управление пакетами (службы SSIS)
  Управление пакетов требует выполнения следующих задач.  
  
-   наблюдение за выполнением пакетов;  
  
-   управление хранилищем пакетов;  
  
-   импорт и экспорт пакетов;  
  
> [!IMPORTANT]  
>  В данном разделе описывается компонент [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] — служба Windows для управления пакетами служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] поддерживает эту службу для обеспечения обратной совместимости с более ранними версиями служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], на сервере служб Integration Services можно управлять пакетами.  
  
## Хранилище пакетов  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предоставляют две папки верхнего уровня для доступа к пакетам служб[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: **Выполняемые пакеты** и **Сохраненные пакеты**. В папке **Выполняемые пакеты** отображаются пакеты, которые в данный момент выполняются на сервере. В папке **Сохраненные пакеты** перечислены пакеты, которые сохранены в хранилище пакетов. Это только те пакеты, которыми управляет служба [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Хранилище пакетов может состоять либо из базы данных msdb, либо из папок файловой системы, перечисленных в файле конфигурации службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], либо как из базы данных, так и из файловой системы. В файле конфигурации указываются база данных msdb и папки файловой системы, над которыми требуется осуществлять управление. Где-либо в файловой системе могут также иметься пакеты, не управляемые службами [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Пакеты, сохраняемые в базе данных msdb, хранятся в таблице с именем sysssispackages. При сохранении пакетов в базе данных msdb их можно также сгруппировать в логические папки. Использование логических папок помогает организовывать пакеты по назначению или отфильтровывать пакеты в таблице sysssispackages. Логические папки можно создавать с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. По умолчанию все логические папки, добавляемые в базу данных msdb, автоматически включаются в хранилище пакетов.  
  
 Логические папки, создаваемые для группирования пакетов в базе данных msdb, представлены как строки в таблице sysssispackagefolders базы данных msdb. Столбцы folderid и parentfolderid в таблице sysssispackagefolders определяют иерархию папок. Корневые логические папки в базе данных msdb представлены строками таблицы sysssispackagefolders, которые содержат значение NULL в столбце parentfolderid. Дополнительные сведения см. в разделах [sysssispackages (Transact-SQL)](../../relational-databases/system-tables/sysssispackages-transact-sql.md) и [sysssispackagefolders (Transact-SQL)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 При открытии среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и подключении к службам [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] папки базы данных msdb, управляемые службой [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], перечислены внутри папки "Хранимые пакеты". Если файл конфигурации задает корневые папки файловой системы, то папка «Хранимые пакеты» также перечисляет пакеты, сохраненные в файловой системе в этих папках и всех ее вложенных папках.  
  
 Пакеты можно сохранить в любой папке файловой системы, но они не будут перечислены во вложенных папках папки **Сохраненные пакеты** , если соответствующую папку не добавить в список папок в файле конфигурации хранилища пакетов. Дополнительные сведения о файле конфигурации см. в статье [Настройка служб Integration Services (SSIS)](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 В папке **Выполняемые пакеты** нет вложенных папок, и она не может быть расширена.  
  
 По умолчанию папка **Сохраненные пакеты** содержит две вложенные папки: **Файловая система** and **MSDB**. В папке **Файловая система** перечислены пакеты, которые сохранены в файловой системе. Расположение этих файлов указано в файле конфигурации службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . По умолчанию это папка «Пакеты», расположенная в папке %Program Files%\Microsoft SQL Server\100\DTS. В папке **MSDB** находятся пакеты служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], которые были сохранены на сервере в базе данных msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сервера. Таблица sysssispackages содержит пакеты, сохраненные в базе данных msdb.  
  
 Для просмотра списка пакетов в хранилище пакетов следует открыть среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и подключиться к службам [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Дополнительные сведения см. в разделе [Просмотр пакетов служб Integration Services в среде SQL Server Management Studio (службы SSIS)](../../integration-services/service/view-integration-services-packages-in-sql-server-management-studio-ssis-service.md).  
  
## наблюдение за выполнением пакетов;  
 В папке **Выполняемые пакеты** находятся выполняемые в данный момент пакеты. Для просмотра сведений о текущих пакетах на странице **Сводка** в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]щелкните папку **Выполняемые пакеты** . На странице **Сводка** приведены такие сведения, как время выполнения пакетов. При необходимости обновите содержимое папки для просмотра более свежих данных.  
  
 Чтобы просмотреть сведения о выполняющемся пакете на странице **Сводка** , щелкните пакет. На странице **Сводка** представлены такие сведения, как версия и описание пакета.  
  
 Можно остановить выполнение пакета в папке **Выполняемые пакеты**, щелкнув правой кнопкой мыши пакет и выбрав **Остановить**.  
  
## управление хранилищем пакетов;  
 Чтобы упорядочить пакеты, можно добавлять пользовательские папки в корневую папку для хранения пакетов, определенную в файле конфигурации служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . По умолчанию корневыми папками являются папки **Файловая система** и **MSDB** . Например, можно создать в папке **Файловая система** вложенную папку **Очистка данных** , которая будет содержать все пакеты, очищающие данные. Можно вкладывать одни пользовательские папки в другие, создавая необходимую пользователю иерархию папок. Пользовательские папки можно удалять и переименовывать, но нельзя переименовывать или удалять корневые папки, определенные в файле конфигурации. Чтобы обновить корневые папки, перечисленные в службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , необходимо обновить файл конфигурации.  
  
 Дополнительные сведения см. в разделе [Настройка служб Integration Services (SSIS)](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
## импорт и экспорт пакетов;  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] пакеты служб можно сохранять либо в базе данных msdb, либо в файловой системе. Пакет можно скопировать из одного места хранения в другое при помощи функций импорта или экспорта, которые предоставляют службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Для создания копии пакета можно импортировать пакет в то же хранилище, дав ему другое название. Для импорта и экспорта пакетов можно также использовать программу командной строки **dtutil** (dtutil.exe).  
  
 Дополнительные сведения см. в статье [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## Связанные задачи  
  
-   [Импорт и экспорт пакетов (службы SSIS)](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
-   [Просмотр пакетов служб Integration Services в среде SQL Server Management Studio (службы SSIS)](../../integration-services/service/view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## См. также раздел  
 [Службы Integration Services (службы SSIS)](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  