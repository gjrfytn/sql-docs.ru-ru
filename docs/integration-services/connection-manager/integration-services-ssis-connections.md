---
title: "Соединения в службах Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.connectionmanager.f1"
  - "sql13.dts.designer.adddtsconnection.f1"
helpviewer_keywords: 
  - "Пакеты служб Integration Services, подключения"
  - "пакеты SSIS, подключения"
  - "источники [службы Integration Services], подключения"
  - "пакеты [службы Integration Services], подключения"
  - "назначения [службы Integration Services], подключения"
  - "задачи [службы Integration Services], подключения"
  - "подключения [службы Integration Services], о подключениях"
  - "соединения [службы Integration Services]"
  - "пакеты служб SQL Server Integration Services, подключения"
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
caps.latest.revision: 92
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 91
---
# Соединения в службах Integration Services (SSIS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] используют соединения для выполнения различных задач и реализации функций служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Подключение к источникам и назначениям данных, например текстовым документам, XML-документам, книгам Excel и реляционным базам данных, для извлечения и загрузки данных.  
  
-   Подключение к реляционным базам данных, содержащим ссылочные данные, для выполнения точных или нечетких уточняющих запросов.  
  
-   Подключение к реляционным базам данных для выполнения инструкций SQL, таких как SELECT, DELETE и INSERT, а также хранимых процедур.  
  
-   Соединение с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для выполнения задач обслуживания и передачи, таких как резервное копирование баз данных и передача имен входа.  
  
-   Запись строк журнала в текстовые файлы, XML-файлы, таблицы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и конфигурации пакетов в таблицах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Соединение с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для создания временных рабочих таблиц, необходимых для некоторых преобразований.  
  
-   Подключение к проектам и базам данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] для доступа к моделям интеллектуального анализа данных, обработке кубов и измерений и запуска DDL-кода.  
  
-   Указание существующих и создание новых файлов и папок для использования их с перечислителями и задачами контейнера «цикл по каждому элементу».  
  
-   Подключение к очередям сообщений и к инструментарию управления Windows (WMI), управляющим объектам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO), сети Интернет и почтовым серверам.  
  
 Чтобы установить эти соединения, службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] используют диспетчеры соединений, как описано в следующем разделе.  
  
## Диспетчеры соединений  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] используют диспетчер соединений в качестве логического представления соединения. На стадии разработки устанавливаются свойства диспетчера соединений, которые описывают физическое соединение, создаваемое сервером служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] при выполнении пакета. Например, диспетчер соединений имеет свойство **ConnectionString** , устанавливаемое на стадии разработки. На стадии выполнения значение этого свойства используется для создания физического соединения.  
  
 Пакет может содержать несколько экземпляров диспетчера соединений одного типа, и для каждого из них свойства устанавливаются отдельно. На стадии выполнения каждый экземпляр диспетчера соединений создает соединение со своими атрибутами.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предоставляют несколько типов диспетчеров соединений, которые позволяют пакету подключаться к различным источникам данных и серверам.  
  
-   Встроенные диспетчеры соединений, которые устанавливаются со службами [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Диспетчеры соединений, которые можно загрузить на веб-сайте корпорации [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   Можно создать собственный диспетчер соединений, если существующие диспетчеры не отвечают требованиям.  
  
### Встроенные диспетчеры соединений  
 В следующей таблице перечислены типы диспетчеров соединений, предоставляемые службами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Тип|Description|Раздел|  
|----------|-----------------|-----------|  
|ADO|Подключается к объектам данных ActiveX (ADO).|[Диспетчер соединений ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Подключается к источнику данных при помощи поставщика .NET.|[Диспетчер соединений ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Считывает данные из потока данных или из файла кэша (CAW) и может сохранять данные в файле кэша.|[Диспетчер соединений с кэшем](../../integration-services/data-flow/transformations/cache-connection-manager.md)|  
|DQS|Подключается к серверу служб качества данных и базе данных служб Data Quality Services на сервере.|[Диспетчер соединений «Очистка DQS»](../../integration-services/data-flow/transformations/dqs-cleansing-connection-manager.md)|  
|EXCEL|Подключается к файлу книги Excel.|[Диспетчер соединений с Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|Подключается к файлу или папке.|[Диспетчер соединения файлов](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|Подключается к данным в отдельном неструктурированном файле.|[Диспетчер соединений с неструктурированными файлами](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|Подключается к FTP-серверу.|[Диспетчер FTP-соединений](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Подключается к веб-серверу.|[Диспетчер HTTP-соединений](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|Подключается к очереди сообщений.|[Диспетчер соединений MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|Подключается к экземпляру служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] или проекту служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[Диспетчер соединений служб Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|Подключается к нескольким файлам и папкам.|[Диспетчер соединений с несколькими файлами](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Подключается к нескольким файлам данных и папкам.|[Диспетчер соединения с несколькими неструктурированными файлами](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|Подключается к источнику данных при помощи поставщика OLE DB.|[Диспетчер соединений OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|интерфейс ODBC|Подключается к источнику данных через ODBC.|[Диспетчер соединений ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|Подключается к серверу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).|[Диспетчер соединений SMO](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Подключается к почтовому серверу SMTP.|[Диспетчер соединений SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Подключается к базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|[Диспетчер соединений SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Подключается к серверу и определяет на нем область инструментария управления Windows (WMI).|[Диспетчер WMI-соединений](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### Диспетчеры соединений, доступные для загрузки  
 В следующей таблице перечислены дополнительные типы диспетчеров соединений, которые вы можете загрузить с веб-сайта [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Перечисленные в следующей таблице диспетчеры соединений работают только с выпусками [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] и [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Тип|Description|Раздел|  
|----------|-----------------|-----------|  
|ORACLE|Подключается к серверу Oracle \<версия>.|Диспетчер соединений Oracle — это компонент диспетчера соединений соединителя для Oracle [!INCLUDE[msCoName](../../includes/msconame-md.md)] компании Attunity. Кроме того, в состав соединителя для Oracle [!INCLUDE[msCoName](../../includes/msconame-md.md)] компании Attunity входят источник и назначение. Дополнительные сведения см. на странице загрузки [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526)(на английском языке).|  
|SAPBI|Подключается к системе SAP NetWeaver BI версии 7.|Диспетчер соединений SAP BI — это компонент диспетчера соединений соединителя для SAP BI [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Кроме того, в состав соединителя для SAP BI [!INCLUDE[msCoName](../../includes/msconame-md.md)] входят источник и назначение. Дополнительные сведения см. на странице загрузки [Microsoft SQL Server 2008 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=262016)(на английском языке).|  
|TERADATA|Подключается к серверу Teradata \<версия>.|Диспетчер соединений Teradata — это компонент диспетчера соединений соединителя для Teradata [!INCLUDE[msCoName](../../includes/msconame-md.md)] компании Attunity. Кроме того, в состав соединителя для Teradata [!INCLUDE[msCoName](../../includes/msconame-md.md)] компании Attunity входят источник и назначение. Дополнительные сведения см. на странице загрузки [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526)(на английском языке).|  
  
### Пользовательские диспетчеры соединений  
 Кроме того, можно создавать пользовательские диспетчеры соединений. Дополнительные сведения см. в разделе [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## Связанные задачи  
 Дополнительные сведения о добавлении или удалении диспетчера соединений в пакете см. в разделе [Добавление, удаление или совместное использование диспетчера соединений в пакете](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
 Подробные сведения о задании свойств диспетчера соединений в пакете см. в разделе [Задание свойств диспетчера соединений](../Topic/Set%20the%20Properties%20of%20a%20Connection%20Manager.md).  
  
## См. также  
  
-   Видеоролик [Использование Microsoft Attunity Connector for Oracle для повышения производительности пакетов](http://technet.microsoft.com/sqlserver/gg598963.aspx)на сайте technet.microsoft.com  
  
-   Статьи Wiki [Сетевые соединения служб SSIS](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)на сайте social.technet.microsoft.com  
  
-   Запись блога [Подключение к MySQL из SSIS](http://go.microsoft.com/fwlink/?LinkId=217669)на сайте blogs.msdn.com.  
  
-   Техническая статья [Извлечение и загрузка данных SharePoint в SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=247826)на сайте msdn.microsoft.com.  
  
-   Техническая статья [Получено сообщение об ошибке "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" при использовании диспетчера соединений Oracle в SSIS](http://go.microsoft.com/fwlink/?LinkId=233696) на сайте support.microsoft.com.  
  
  