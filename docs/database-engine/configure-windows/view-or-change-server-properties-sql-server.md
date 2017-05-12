---
title: "Просмотр или изменение свойств сервера (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "просмотр свойств сервера"
  - "свойства сервера [SQL Server]"
  - "отображение свойств сервера"
  - "серверы [SQL Server], просмотр"
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Просмотр или изменение свойств сервера (SQL Server)
  В этом разделе описывается просмотр и изменение свойств экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]или диспетчера конфигурации SQL Server.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Для просмотра или изменения свойств сервера используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Диспетчер конфигурации SQL Server](#PowerShellProcedure)  
  
-   **Дальнейшие действия**. [После изменения свойств сервера](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Используя sp_configure, необходимо выполнить инструкцию RECONFIGURE или инструкцию RECONFIGURE WITH OVERRIDE после установки параметра конфигурации. Инструкция RECONFIGURE WITH OVERRIDE обычно употребляется для параметров конфигурации, которые должны использоваться с особой осторожностью. Однако инструкция RECONFIGURE WITH OVERRIDE пригодна для всех параметров конфигурации, и ее можно использовать вместо инструкции RECONFIGURE.  
  
    > [!NOTE]  
    >  Инструкция RECONFIGURE выполняется внутри транзакции. Если какая-либо из операций повторной настройки завершится ошибкой, ни одна из операций повторной настройки не возымеет действия.  
  
-   Некоторые страницы со свойствами предоставляют сведения, полученные через инструментарий управления Windows (WMI). Для отображения этих страниц на компьютере, где работает среда [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], должен быть установлен инструментарий WMI.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Дополнительные сведения см. в разделе [Роли уровня сервера](../../relational-databases/security/authentication-access/server-level-roles.md).  
  
 Разрешения на выполнение хранимой процедуры **sp_configure** без параметров или только с первым параметром по умолчанию предоставляются всем пользователям. Для выполнения процедуры **sp_configure** с обоими параметрами для изменения параметра конфигурации или запуска инструкции RECONFIGURE необходимо иметь разрешение ALTER SETTINGS на уровне сервера. Разрешение ALTER SETTINGS неявным образом предоставлено предопределенным ролям сервера **sysadmin** и **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Просмотр или изменение свойств сервера  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши сервер и выберите пункт **Свойства**.  
  
2.  В диалоговом окне **Свойства сервера** щелкните страницу, чтобы просмотреть или изменить содержащиеся на сервере сведения об этой странице. Некоторые свойства доступны только для чтения.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Просмотр свойств сервера с помощью встроенной функции SERVERPROPERTY  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере используется встроенная функция [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md) в инструкции `SELECT` для возврата сведений о текущем сервере. Этот сценарий полезен, когда на сервере Windows установлено несколько экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и клиенту приходится открывать другое соединение с тем же экземпляром, который используется текущим соединением.  
  
    ```tsql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### Просмотр свойств сервера с помощью представления каталога sys.servers  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере запрашивается представление каталога [sys.servers](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md) для получения имени (`name`) и идентификатора (`server_id`) текущего сервера, а также имя поставщика OLE DB (`provider`) для подключения к связанному серверу.  
  
    ```tsql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO  
  
    ```  
  
#### Просмотр свойств сервера с помощью представления каталога sys.configurations  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере запрашивается представление каталога [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) , чтобы вернуть сведения о каждом параметре конфигурации для текущего сервера. В примере возвращается имя (`name`) и описание (`description`) параметра, а также указывается, является ли параметр дополнительным (`is_advanced`).  
  
    ```wmimof  
    USE AdventureWorks2012;   
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;   
    GO  
  
    ```  
  
#### Изменение свойства сервера с помощью процедуры sp_configure  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере показано, как изменить свойство сервера с помощью процедуры [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). В примере значение параметра `fill factor` меняется на `100`. Чтобы изменение вступило в силу, необходимо перезапустить сервер.  
  
```tsql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 Дополнительные сведения см. в статье [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="PowerShellProcedure"></a> Использование диспетчера конфигурации SQL Server  
 Некоторые свойства сервера можно просматривать и изменять с помощью диспетчера конфигурации SQL Server. Например, можно просмотреть версию и выпуск экземпляра SQL Server или изменить расположение файлов журнала ошибок. Эти свойства также можно просмотреть, запросив [динамические административные представления и функции динамического управления, относящиеся к серверу](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md).  
  
#### Просмотр или изменение свойств сервера  
  
1.  В меню **Пуск** последовательно укажите пункты **Все программы**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Средства настройки**и выберите пункт **Диспетчер конфигурации SQL Server**.  
  
2.  В **диспетчере конфигурации SQL Server**выберите **Службы SQL Server**.  
  
3.  На панели подробных сведений щелкните **SQL Server (\<***имя_экземпляра***>)** правой кнопкой мыши и выберите пункт **Свойства**.  
  
4.  В диалоговом окне **Свойства SQL Server (\<***имя_экземпляра***>)** измените свойства сервера на вкладке **Служба** или **Дополнительно** и нажмите кнопку **ОК**.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После изменения свойств сервера  
 Для некоторых свойств необходимо перезапустить сервер, чтобы изменения вступили в силу.  
  
## См. также:  
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [Настройка инструментария WMI для отображения состояния сервера в инструментальных средствах SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [Диспетчер конфигурации SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Функции настройки (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Динамические административные представления и функции, связанные с сервером (Transact-SQL)](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  