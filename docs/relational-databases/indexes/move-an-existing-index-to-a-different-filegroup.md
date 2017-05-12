---
title: "Перемещение существующего индекса в другую файловую группу | Документация Майкрософт"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cfc19f15cee7ca1185a2a9177474510c368b56bf
ms.lasthandoff: 04/11/2017

---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>Перемещение существующего индекса в другую файловую группу
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  В этом разделе описывается, как переместить текущий индекс из текущей файловой группы в другую файловую группу в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Для перемещения существующего индекса в другую файловую группу используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Если таблица имеет кластеризованный индекс, то перемещение кластеризованного индекса в новую файловую группу перемещает в эту файловую группу саму таблицу.  
  
-   В среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]нельзя перемещать индексы, созданные с помощью ограничения UNIQUE или PRIMARY KEY. Для перемещения этих индексов используйте инструкцию [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) с параметром (DROP_EXISTING=ON) в [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Необходимо разрешение ALTER для таблицы или представления. Пользователь должен быть членом предопределенной роли сервера **sysadmin** или предопределенных ролей базы данных **db_ddladmin** и **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>Перемещение существующего индекса в другую файловую группу с помощью конструктора таблиц  
  
1.  В обозревателе объектов щелкните знак «плюс», чтобы развернуть базу данных, содержащую таблицу, где находится индекс, который нужно переместить.  
  
2.  Чтобы развернуть папку **Таблицы** , щелкните значок «плюс».  
  
3.  Щелкните правой кнопкой мыши таблицу, содержащую индекс, который нужно переместить, и выберите пункт **Конструктор**.  
  
4.  В меню **Конструктор таблиц** выберите пункт **Индексы и ключи**.  
  
5.  Выберите индекс, который нужно переместить.  
  
6.  В основной сетке разверните узел **Спецификация пространства данных**.  
  
7.  Выберите значение **Имя файловой группы или схемы секционирования** и выберите из списка файловую группу или схему секционирования, в которую нужно переместить индекс.  
  
8.  Щелкните **Закрыть**.  
  
9. В меню **Файл** выберите пункт **Сохранить***имя_таблицы*.  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>Перемещение существующего индекса в другую файловую группу в обозревателе объектов  
  
1.  В обозревателе объектов щелкните знак «плюс», чтобы развернуть базу данных, содержащую таблицу, где находится индекс, который нужно переместить.  
  
2.  Чтобы развернуть папку **Таблицы** , щелкните значок «плюс».  
  
3.  Щелкните знак «плюс», чтобы развернуть таблицу, содержащую индекс, который необходимо переместить.  
  
4.  Чтобы развернуть папку **Индексы** , щелкните знак «плюс» (+).  
  
5.  Щелкните правой кнопкой мыши индекс, который нужно переместить, и выберите пункт **Свойства**.  
  
6.  В разделе **Выбор страницы**выберите пункт **Хранение**.  
  
7.  Выберите файловую группу, в которую необходимо переместить индекс.  
  
     если таблица или индекс секционированы, выберите схему секционирования, в которую переместить индекс. Дополнительные сведения о секционированных индексах см. в разделе [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
     если перемещается кластеризованный индекс, можно использовать обработку в сети. Обработка в сети разрешает одновременный доступ пользователей к основным данным и к некластеризованным индексам в течение операции с индексами. Дополнительные сведения см. в статье [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
     На многопроцессорных компьютерах с [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]можно настроить количество ЦП, используемых для выполнения инструкции индекса, указав значение максимальной степени параллелизма. Параллельные операции с индексами доступны не во всех выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Сведения о функциях, поддерживаемых различными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в статье "Возможности, поддерживаемые выпусками SQL Server 2016". Дополнительные сведения о параллельных операциях с индексами см. в статье [Настройка параллельных операций с индексами](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
8.  Нажмите кнопку **ОК**.  
  
 На странице **Хранение** диалогового окна **Свойства индекса ―** *имя_индекса* доступны следующие сведения:  
  
 **Файловая группа**  
 Сохраняет индекс в указанной файловой группе. Этот список содержит только стандартные файловые группы (ROW). По умолчанию из этого списка выбирается первичная файловая группа (PRIMARY) текущей базы данных.  
  
 **Файловая группа файлового потока**  
 Задает файловую группу для данных FILESTREAM. Этот список содержит только файловые группы FILESTREAM. По умолчанию из этого списка выбирается файловая группа PRIMARY FILESTREAM.  
  
 **Схема секционирования**  
 Хранит индекс в схеме секционирования. Если нажать кнопку **Схема секционирования** , активируется сетка внизу. По умолчанию из списка выбирается схема секционирования, использованная для хранения данных таблицы. При выборе из списка другой схемы секционирования данные в сетке обновляются.  
  
 Параметр схемы секционирования недоступен, если в базе данных нет ни одной схемы секционирования.  
  
 **Схема секционирования файлового потока**  
 Задает схему секционирования для данных FILESTREAM. Схема секционирования должна быть симметрична схеме, указанной в параметре **Схема секционирования** .  
  
 Если таблица не секционирована, это поле пусто.  
  
 **Параметр схемы секционирования**  
 Отображает имя столбца, участвующего в схеме секционирования.  
  
 **Столбец таблицы**  
 Выберите таблицу или представление для сопоставления схеме секционирования.  
  
 **Тип данных столбца**  
 Выводит сведения о типах данных для данного столбца.  
  
> [!NOTE]  
>  Если это вычисляемый столбец, в поле **Тип данных столбца** отображается отметка "вычисляемый столбец".  
  
 **Разрешить обработку в сети DML-инструкций во время переноса индекса**  
 Параметр дает пользователям возможность получать доступ к данным базовой таблицы или кластеризованного индекса, а также к любым связанным с ними некластеризованным индексам при операциях с индексами.  
  
> [!NOTE]  
>  Этот параметр недоступен для XML-индексов, а также в случае, если индекс является отключенным кластеризованным индексом.  
  
 **Укажите максимальную степень параллелизма**  
 Ограничивает число процессоров, используемых в одновременном исполнении планов. При значении по умолчанию 0 используется реальное число доступных ЦП. При установке значения 1 создание параллельных планов становится невозможным; при установке значения больше 1 ограничивается максимальное число процессоров, используемых для выполнения одного запроса. Этот параметр становится доступным только в случае, если диалоговое окно находится в состоянии **Перестроение** или **Повторное создание** .  
  
> [!NOTE]  
>  Если задано значение, превышающее число доступных ЦП, используется фактическое число доступных ЦП.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>Перемещение существующего индекса в другую файловую группу  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 Дополнительные сведения см. в разделе [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md).  
  
  
