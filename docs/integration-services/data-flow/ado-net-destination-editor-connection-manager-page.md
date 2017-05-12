---
title: "Редактор назначения &#171;ADO.NET&#187; (страница &#171;Диспетчер соединений&#187;) | Microsoft Docs"
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
  - "sql13.dts.designer.adonetdest.connection.f1"
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# Редактор назначения &#171;ADO.NET&#187; (страница &#171;Диспетчер соединений&#187;)
  Используйте страницу **Диспетчер соединений** диалогового окна **Редактор назначения «ADO.NET»** , чтобы выбрать соединение [!INCLUDE[vstecado](../../includes/vstecado-md.md)] для назначения. На этой странице также можно выбрать таблицу или представление базы данных.  
  
 Дополнительные сведения о назначении «ADO.NET» см. в разделе [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
 **Открытие страницы «Диспетчер соединений»**  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий назначение «ADO.NET».  
  
2.  На вкладке **Поток данных** дважды щелкните назначение "ADO.NET".  
  
3.  В окне **Редактор назначения «ADO.NET»**нажмите кнопку **Диспетчер соединений**.  
  
## Статические параметры  
 **Диспетчер соединений**  
 Выберите из списка существующий диспетчер соединений или создайте новое соединение, нажав кнопку **Создать**.  
  
 **Создать**  
 Создайте новый диспетчер соединений с помощью диалогового окна **Настройка диспетчера соединений ADO.NET**.  
  
 **Использовать таблицу или представление**  
 Выберите существующую таблицу или представление из списка или создайте новую таблицу, выбрав пункт **Создать**.  
  
 **Создать**  
 Создайте новую таблицу, используя диалоговое окно **Создание таблицы**.  
  
> [!NOTE]  
>  При нажатии кнопки **Создать**службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] по умолчанию формируют инструкцию CREATE TABLE на основе подключенного источника данных. Эта инструкция CREATE TABLE не включает атрибут FILESTREAM, даже если исходная таблица содержит столбец, для которого объявлен атрибут FILESTREAM. Чтобы запустить компонент служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] с атрибутом FILESTREAM, сначала следует создать хранилище FILESTREAM в целевой базе данных. Затем добавьте атрибут FILESTREAM к инструкции CREATE TABLE в диалоговом окне **Создание таблицы** . Дополнительные сведения см. в разделе [Данные большого двоичного объекта (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Предварительный просмотр**  
 Просмотрите предварительные результаты, используя диалоговое окно **Предварительный просмотр результатов запроса**. В окне «Предварительный просмотр» может отображаться до 200 строк.  
  
 **По возможности следует использовать массовую вставку**  
 Укажите, следует ли использовать интерфейс <xref:System.Data.SqlClient.SqlBulkCopy> для улучшения производительности операций массовой вставки.  
  
 Только поставщики ADO.NET, возвращающие объект <xref:System.Data.SqlClient.SqlConnection>, поддерживают использование интерфейса <xref:System.Data.SqlClient.SqlBulkCopy>. Поставщик данных .NET для SQL Server (SqlClient) возвращает объект <xref:System.Data.SqlClient.SqlConnection>, а настраиваемый поставщик может возвращать объект <xref:System.Data.SqlClient.SqlConnection>.  
  
 Вы можете использовать поставщик данных .NET для SQL Server (SqlClient) для подключения к [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 Если был выбран параметр **По возможности использовать массовую вставку**, а для параметра **Ошибка** задано значение **Перенаправить строку**, то в пакет данных, перенаправляемый объектом назначения в вывод ошибок, могут попасть и строки, не содержащие ошибок. Дополнительные сведения об обработке ошибок в массовых операциях см. в разделе [Обработка ошибок в данных](../../integration-services/data-flow/error-handling-in-data.md). Дополнительные сведения о параметре **Ошибка** см. в разделе [Редактор назначения ADO.NET (страница "Вывод ошибок")](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Если исходная таблица [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или Sybase включает столбец идентификаторов, то необходимо использовать задачи «Выполнение SQL» для выполнения инструкции SET IDENTITY_INSERT до и после доступа к назначению «ADO.NET». Это свойство столбца идентификаторов указывает значение приращения для столбца. Инструкция SET IDENTITY_INSERT разрешает вставлять в столбец идентификаторов явно заданные значения. Чтобы выполнить инструкции CREATE TABLE и SET IDENTITY в одном и том же подключении к базе данных, задайте свойство **RetainSameConnection** диспетчера соединений [!INCLUDE[vstecado](../../includes/vstecado-md.md)] равным **True**. Кроме того, используйте один и тот же диспетчер соединений [!INCLUDE[vstecado](../../includes/vstecado-md.md)] для задач «Выполнение SQL» и назначения «ADO NET».  
>   
>  Дополнительные сведения см. в разделе [SET IDENTITY_INSERT (Transact-SQL)](../../t-sql/statements/set-identity-insert-transact-sql.md) и [IDENTITY (свойство) (Transact-SQL)](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md).  
  
## Внешние ресурсы  
 Техническая статья [Быстрый способ загрузки данных в базу данных SQL Windows Azure](http://go.microsoft.com/fwlink/?LinkId=244333)на сайте sqlcat.com  
  
## См. также  
 [Редактор назначения ADO.NET (страница "Сопоставления")](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [Редактор назначения ADO.NET (страница "Вывод ошибок")](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [Диспетчер соединений ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [Задача «Выполнение SQL»](../../integration-services/control-flow/execute-sql-task.md)  
  
  