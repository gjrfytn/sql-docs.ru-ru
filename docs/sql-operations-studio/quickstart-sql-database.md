---
title: "Краткое руководство: Подключение и запроса к базе данных Azure SQL с помощью операций SQL Studio (Предварительная версия) | Документы Microsoft"
description: "Краткого руководства показано, как использовать для подключения к базе данных SQL и выполнить запрос SQL Studio операций (Предварительная версия)"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0e2d48ed411f883a904decce5d836dde7aaa41b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Краткое руководство: Использование [!INCLUDE[name-sos](../includes/name-sos-short.md)] для подключения и запроса базы данных Azure SQL

Это краткое руководство демонстрирует использование  *[!INCLUDE[name-sos](../includes/name-sos-short.md)]*  для подключения к базе данных Azure SQL, а затем использовать инструкции Transact-SQL (T-SQL) для создания *TutorialDB* используется в [!INCLUDE[name-sos](../includes/name-sos-short.md)] учебники.

## <a name="prerequisites"></a>предварительные требования

Для выполнения краткого руководства, необходимо [!INCLUDE[name-sos](../includes/name-sos-short.md)]и сервер Azure SQL.

- [Установка [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Если у вас еще нет сервер Azure SQL, выполните одно из следующих примеры использования базы данных SQL Azure (Помните, имя сервера и учетные данные входа!).

- [Создание БД - портала](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Создание БД - CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Создание база данных — PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Подключение к серверу базы данных SQL Azure

Используйте [!INCLUDE[name-sos](../includes/name-sos-short.md)] для установления соединения с сервером базы данных SQL Azure.

1. При первом запуске [!INCLUDE[name-sos](../includes/name-sos-short.md)] **подключения** должна открыться страница. Если **подключения** страница не открывается, нажмите кнопку **новое подключение** значок в **СЕРВЕРЫ** боковой панели:
   
   ![Значок нового подключения](media/quickstart-sql-database/new-connection-icon.png)

2. В этой статье используется *входа SQL*, но *проверки подлинности Windows* также поддерживается. Заполните поля следующим образом:

   | Настройка       | Предлагаемое значение | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Имя сервера** | Полное имя сервера | Имя должно быть примерно следующим образом: **servername.database.windows.net** |
   | **Проверка подлинности** | Имя входа SQL| В этом учебнике используется проверка подлинности SQL. |
   | **User name** | Учетная запись администратора сервера | Это учетная запись, которая была указана при создании сервера. |
   | **Пароль (имя входа SQL)** | Пароль для учетной записи администратора сервера | Это пароль, который был указан при создании сервера. |
   | **Сохранить пароль?** | "Да" или "Нет". | Если вы не хотите вводить пароль каждый раз, нажмите кнопку "Да". |
   | **Имя базы данных** | *не указывайте* | Имя базы данных, которую вы хотите подключиться. |
   | **Группы серверов** | Выберите<Default> | Если вы создали группу серверов, можно задать конкретную группу серверов. | 

   ![Значок нового подключения](media/quickstart-sql-database/new-connection-screen.png)  

3. Если возникает ошибка, о брандмауэрах, необходимо создать правило брандмауэра. Чтобы создать правило брандмауэра, см. [правила брандмауэра](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

4. После успешного подключения сервера будет отображаться в *серверы* боковой панели.

## <a name="create-the-tutorial-database"></a>Создайте в учебной базе данных

*TutorialDB* базы данных используется в нескольких [!INCLUDE[name-sos](../includes/name-sos-short.md)] учебники.

1. Щелкните правой кнопкой мыши сервер Azure SQL на боковой панели СЕРВЕРОВ и выберите **новый запрос.**

1. Вставьте следующий фрагмент кода в редакторе запросов.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. Чтобы выполнить запрос, нажмите кнопку **запуска**.


## <a name="create-a-table"></a>Создание таблицы

Редактор запросов подключен *master* требуется создание таблицы в базу данных, но мы *TutorialDB* базы данных. 

1. Изменить контекст подключения к **TutorialDB**:

   ![Контекст изменения](media/quickstart-sql-database/change-context.png)



1. Вставьте следующий фрагмент кода в редакторе запросов.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```
1. Чтобы выполнить запрос, нажмите кнопку **запуска**.

## <a name="insert-rows"></a>Вставка строк

1. Вставьте следующий фрагмент кода в редакторе запросов:
   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

1. Чтобы выполнить запрос, нажмите кнопку **запуска**.

## <a name="view-the-result"></a>Просмотреть результаты
1. Вставьте следующий фрагмент кода в редакторе запросов.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Чтобы выполнить запрос, нажмите кнопку **запуска**.

   ![Выберите результаты](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>Очистка ресурсов

Другие статьи в этой коллекции созданы на основе краткого руководства. Если вы планируете продолжить работу с последующей краткие руководства, очищает ресурсы, созданные в этом кратком руководстве. Если вы не планируете продолжить работу, выполните следующие действия, чтобы удалить ресурсы, созданные на портале Azure краткого руководства.
Очистка ресурсов путем удаления группы ресурсов, которые больше не нужны. Дополнительные сведения см. в разделе [очистки ресурсов](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Следующие шаги

Теперь, успешного подключения к базе данных Azure SQL и запущен запрос, Попробуйте поработать [учебник редактора кода](tutorial-sql-editor.md).