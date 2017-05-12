---
title: "Создание связанных серверов (компонент SQL Server Database Engine) | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/20/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 219a32bb6296fac9ec50f78899a31fe52475095c
ms.lasthandoff: 04/11/2017

---
# <a name="create-linked-servers-sql-server-database-engine"></a>Создание связанных серверов (компонент SQL Server Database Engine)
  В этом разделе описано, как создать связанный сервер и производить доступ к данным из другого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Путем создания связанного сервера вы можете работать с данными из нескольких источников. Связанный сервер не обязательно должен быть другим экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], хотя такой вариант часто встречается.  
  
##  <a name="Background"></a> Историческая справка  
 Связанные серверы позволяют выполнять распределенные разнородные запросы к источникам данных OLE DB. После создания связанного сервера можно выполнять распределенные запросы к этому серверу, причем в запросах могут соединять таблицы из нескольких источников данных. Если связанный сервер определен в качестве экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], на нем могут выполняться удаленные хранимые процедуры.  
  
 Возможности связанного сервера и необходимые аргументы могут сильно различаться. В примерах из этого раздела представлены типичные ситуации, но описаны не все параметры. Дополнительные сведения см. в статье [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
##  <a name="Security"></a> Безопасность  
  
### <a name="permissions"></a>Разрешения  
 При использовании инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] требуется разрешение **ALTER ANY LINKED SERVER** на сервер или членство в предопределенной роли сервера **setupadmin** . Для работы с [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] требуется разрешение **CONTROL SERVER** или членство в предопределенной роли сервера **sysadmin** .  
  
##  <a name="Procedures"></a> Создание связанного сервера  
 Можно использовать следующие параметры.  
  
-   [Среда SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>Создание связанного сервера для другого экземпляра SQL Server в среде SQL Server Management Studio  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]откройте обозреватель объектов, разверните узел **Объекты сервера**, щелкните правой кнопкой мыши узел **Связанные серверы**и выберите команду **Создать связанный сервер**.  
  
2.  На странице **Общие** в поле **Связанный сервер** введите имя экземпляра **SQL Server** , с которым связывается область.  
  
     **SQL Server**  
     Идентификация связанного сервера как экземпляра [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. При использовании этого метода определения связанного сервера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имя, указанное в поле **Связанный сервер** , должно быть сетевым именем этого сервера. Кроме того, все таблицы, полученные от сервера, будут получены из базы данных, по умолчанию определенной для имени входа на связанный сервер.  
  
     **Другой источник данных**  
     Укажите тип сервера OLE DB, отличный от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Включение этой функции активирует дополнительные параметры, расположенные под ней.  
  
     **Поставщик**  
     Выберите источник данных OLE DB в окне списка. Поставщик OLE DB зарегистрирован в реестре с данным идентификатором PROGID.  
  
     **Название продукта**  
     Введите название продукта для источника данных OLE DB, который добавляется в качестве связанного сервера.  
  
     **Источник данных**  
     Введите имя источника данных согласно интерпретации поставщика OLE DB. При соединении с экземпляром служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]указывается имя экземпляра.  
  
     **Строка поставщика**  
     Введите уникальный программный идентификатор (PROGID) поставщика OLE DB, соответствующий источнику данных. Примеры допустимых строк поставщиков см. в статье [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
     **Местоположение**  
     Введите местонахождение базы данных, понятное поставщику OLE DB.  
  
     **Каталог**  
     Введите имя каталога, который следует использовать при соединении с поставщиком OLE DB.  
  
     Чтобы проверить возможность соединения со связанным сервером, щелкните его в обозревателе объектов правой кнопкой мыши и выберите команду **Проверить соединение**.  
  
    > [!NOTE]  
    >  Если экземпляр **SQL Server** является экземпляром по умолчанию, то введите имя компьютера, на котором размещается экземпляр **SQL Server**. Если экземпляр **SQL Server** является именованным, введите имя компьютера и имя экземпляра, например **Accounting\SQLExpress**.  
  
3.  В области **Тип сервера** выберите **SQL Server** , чтобы показать, что связанные сервер является другим экземпляром **SQL Server**.  
  
4.  На странице **Безопасность** укажите контекст безопасности, который будет использоваться при подключении исходного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] к связанному серверу. В среде с доменами, где пользователи соединяются с именами входа домена, лучшим вариантом часто оказывается **Выполнять с использованием текущего контекста безопасности имени входа** . Если пользователи соединяются с исходным экземпляром **SQL Server** по имени входа **SQL Server** , то лучшим вариантом часто оказывается **С использованием этого контекста безопасности**с последующим указанием необходимых учетных данных для проверки подлинности на связанном сервере.  
  
     **Локальное имя входа**  
     Указывает локальное имя входа, с помощью которого может осуществляться соединение со связанным сервером. Локальное имя входа может представлять собой либо имя входа с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , либо имя входа с проверкой подлинности Windows. Используйте этот список для разрешения соединений только определенным именам входа или для разрешения некоторым именам входа подключаться в качестве другого имени входа.  
  
     **Impersonate**  
     Передает имя пользователя и пароль из локального имени входа на связанный сервер. Для проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на удаленном сервере должны существовать учетные данные входа с тем же самым именем и паролем. Для имен входа Windows имя входа должно быть допустимым на связанном сервере.  
  
     Чтобы использовать олицетворение, конфигурация должна соответствовать требованиям, предъявляемым к делегированию.  
  
     **Удаленный пользователь**  
     Сопоставьте удаленного пользователя c пользователями, не определенными в **локальном имени входа**. **Удаленный пользователь** на удаленном сервере должен представлять собой имя входа для проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Пароль для удаленного входа**  
     Указывает пароль удаленного пользователя.  
  
     **Добавить**  
     Добавляет новое локальное имя входа.  
  
     **Удалить**  
     Удаляет существующее локальное имя входа.  
  
     **Не выполнять**  
     Указывает, что для имен входа, не определенных в списке, соединение невозможно.  
  
     **Выполняется без использования контекста безопасности**  
     Указывает, что для имен входа, не определенных в списке, соединение будет выполняться без использования контекста безопасности.  
  
     **Выполняется с использованием текущего контекста безопасности имени входа**  
     Указывает, что для имен входа, не определенных в списке, соединение будет выполняться с использованием текущего контекста безопасности имени входа. При наличии соединения с локальным сервером с использованием проверки подлинности Windows для подключения к удаленному серверу будут использоваться учетные данные Windows. При наличии соединения с локальным сервером с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для подключения к удаленному серверу будут использоваться имя входа и пароль. В этом случае на удаленном сервере должны существовать учетные данные входа с теми же именем и паролем.  
  
     **Выполнять с использованием данного контекста безопасности**  
     Указывает, что для имен входа, не определенных в списке, соединение будет выполняться при помощи имени входа и пароля, заданных в полях **Удаленный вход** и **С паролем** . Удаленное имя входа на удаленном сервере должно представлять собой имя входа для проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Для просмотра и установки параметров сервера можно также открыть страницу **Параметры сервера**  .  
  
     **Совместимые параметры сортировки**  
     Влияет на выполнение распределенных запросов на связанных серверах. Если этот параметр установлен в значение true, то [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предполагает, что все символы в связанном сервере совместимы с локальным сервером в зависимости от набора символов и параметров сортировки (или порядка сортировки). Это позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] отправлять поставщику сравнения по символьным столбцам. Если этот параметр не задан, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] всегда выполняет сравнения по символьным столбцам локально.  
  
     Этот параметр необходимо задать только в том случае, если источник данных, соответствующий связанному серверу, имеет тот же набор символов и тот же порядок сортировки, что и локальный сервер.  
  
     **Доступ к данным**  
     Разрешает и запрещает доступ распределенных запросов к связанному серверу.  
  
     **RPC**  
     Включает RPC с определенного сервера.  
  
     **RPC Out**  
     Включает RPC на определенный сервер.  
  
     **Использовать параметры сортировки удаленного сервера**  
     Определяет, будут ли использоваться параметры сортировки удаленного столбца или локального сервера.  
  
     Если значение равно true, в источниках данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] используются параметры сортировки удаленных столбцов, а в не-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] источниках данных — режим, заданный в имени параметров сортировки.  
  
     Если значение равно false, при распределенных запросах всегда будут использоваться установленные по умолчанию параметры сортировки на локальном сервере, в то время как имя параметров сортировки и параметры сортировки удаленных столбцов будут пропускаться. Значение по умолчанию — false.  
  
     **Имя параметров сортировки**  
     Позволяет задать имя параметров сортировки, используемое удаленным источником данных, если значение параметра «Использовать параметры сортировки удаленного сервера» равно true, а источник данных не является источником данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Этот имя должно быть одним из параметров сортировки, поддерживаемых [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Этот параметр используется при доступе к источнику данных OLE DB, отличному от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], параметры сортировки которого совпадают с одним из параметров сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Связанный сервер должен поддерживать использование единых параметров сортировки для всех столбцов на этом сервере. Не задавайте этот параметр, если связанный сервер поддерживает несколько параметров сортировки для одного источника данных, или если невозможно определить, соответствуют ли параметры сортировки связанного сервера одному из параметров сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Время ожидания соединения**  
     Значение времени ожидания соединения со связанным сервером.  
  
     Если значение равно 0, используется значение, заданное через **sp_configure** по умолчанию, — [remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) .  
  
     **Время ожидания запроса**  
     Значение времени ожидания для запросов к связанному серверу, в секундах.  
  
     Если значение равно 0, используется значение, заданное через **sp_configure** по умолчанию, — [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) .  
  
     **Разрешить продвижение распределенных транзакций**  
     Используйте этот параметр, чтобы защитить действия процедуры между серверами посредством транзакции координатора распределенных транзакций (Майкрософт) ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] DTC). Если этот параметр имеет значение TRUE, то вызов удаленной хранимой процедуры приводит к запуску распределенной транзакции и прикрепляет к выполнению транзакции MS DTC. Дополнительные сведения см. в статье [sp_serveroption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).  
  
6.  Нажмите кнопку **ОК**.  
  
##### <a name="to-view-the-provider-options"></a>Просмотр параметров поставщика  
  
-   Чтобы просмотреть доступные параметры поставщика, откройте страницы **Параметры поставщиков** .  
  
     У всех поставщиков нет общего набора доступных параметров. Например, некоторые типы данных могут быть индексированы, а некоторые нет. Используйте это диалоговое окно, чтобы ознакомить службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с возможностями поставщика. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливает несколько общих поставщиков данных, однако при изменении продукта, поставляющего данные, поставщик, установленный с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , может не поддерживать все новейшие функции. Лучшим источником сведений о возможностях продукта, поставляющего данные, является документация по продукту.  
  
     **Динамический параметр**  
     Указывает, что поставщик разрешает использовать синтаксис маркеров параметров «?» для параметризованных запросов. Установите этот параметр только в том случае, если поставщик поддерживает интерфейс **ICommandWithParameters** и символ «?» в качестве маркера параметров. Установка этого параметра позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполнять параметризованные запросы к поставщику. Возможность выполнять параметризованные запросы к поставщику может повысить производительность некоторых запросов.  
  
     **Вложенные запросы**  
     Указывает, что поставщик разрешает вложенные инструкции `SELECT` в предложении FROM. Установка этого параметра позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] делегировать поставщику определенные запросы, требующие вложенных инструкций SELECT в предложении FROM.  
  
     **Только нулевой уровень**  
     Для поставщика вызываются только интерфейсы OLE DB уровня 0.  
  
     **Допускать в ходе процесса**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешает создание экземпляра поставщика в виде внутрипроцессного сервера. Если этот параметр не установлен, поведением по умолчанию является создание экземпляра поставщика вне процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Создание экземпляра поставщика вне процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] защищает процесс [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] от ошибок в поставщике. Если экземпляр поставщика создается вне процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , обновления или вставки, ссылающиеся на длинные столбцы (**text**, **ntext**или **image**), не разрешаются.  
  
     **Обновления без использования транзакций**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешает обновления, даже если недоступен интерфейс **ITransactionLocal** . Если этот параметр включен, обновления поставщика необратимы, поскольку этот поставщик не поддерживает транзакции.  
  
     **Индекс в качестве пути доступа**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] пытается использовать индексы поставщика для выборки данных. По умолчанию индексы используются только для метаданных и никогда не открываются.  
  
     **Запретить нерегламентированный доступ**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не разрешает нерегламентированный доступ с помощью функций OPENROWSET и OPENDATASOURCE к поставщику OLE DB. Если этот параметр не задан, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] также не разрешает нерегламентированный доступ.  
  
     **Поддерживает оператор Like.**  
     Указывает, что поставщик поддерживает запросы с использованием ключевого слова LIKE.  
  
###  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 Чтобы создать связанный сервер с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)], используйте инструкции [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN (Transact-SQL)](../../t-sql/statements/create-login-transact-sql.md) и [sp_addlinkedsrvlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Создание связанного сервера для другого экземпляра SQL Server с помощью Transact-SQL  
  
1.  В редакторе запросов введите следующую команду [!INCLUDE[tsql](../../includes/tsql-md.md)] , чтобы установить связь с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с именем `SRVR002\ACCTG`:  
  
    ```tsql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  Выполните следующий код, чтобы настроить связанный сервер для использования учетных данных домена для имени входа, которое использует связанный сервер.  
  
    ```tsql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> Дальнейшие действия после создания связанного сервера  
  
#### <a name="to-test-the-linked-server"></a>Проверка связанного сервера  
  
-   Выполните следующий код, чтобы проверить соединение со связанным сервером. Этот пример возвращает имена баз данных на связанном сервере.  
  
    ```tsql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>Создание запроса, соединяющего таблицы со связанного сервера  
  
-   Для ссылки на объект, расположенный на связанном сервере, используйте четырехкомпонентные имена. Выполните следующий код, чтобы получить список всех имен входа на локальном сервере и соответствующих имен входа на связанном сервере.  
  
    ```tsql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     Если для имени входа связанного сервера возвращается значение NULL, это значит, что имя входа не существует на связанном сервере. Такие имена входа не смогут использовать связанный сервер, если на нем не настроена передача другого контекста безопасности и он не принимает анонимные подключения.  
  
## <a name="see-also"></a>См. также:  
 [Связанные серверы (компонент Database Engine)](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
