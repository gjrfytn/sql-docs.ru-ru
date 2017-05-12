---
title: "Настройка доступа только для чтения в реплике доступности (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "доступ по соединению к репликам доступности"
  - "группы доступности [SQL Server], вторичные реплики для чтения"
  - "активные вторичные реплики [SQL Server], доступ только для чтения"
  - "группы доступности [SQL Server], маршрутизация только для чтения"
  - "группы доступности [SQL Server], подключение клиента"
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
caps.latest.revision: 35
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 35
---
# Настройка доступа только для чтения в реплике доступности (SQL Server)
  По умолчанию и доступ для чтения и записи, и доступ только для чтения разрешены в первичной реплике, а подключения к вторичным репликам группы доступности AlwaysOn запрещены. В этом разделе описывается настройка доступа к соединениям реплики доступности в группе доступности AlwaysOn в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] или PowerShell.  
  
 Сведения о последствиях включения доступа только для чтения во вторичной реплике и обзор доступа к соединениям см. в статьях [Сведения о доступе клиентского подключения к репликам доступности (SQL Server)](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md) и [Клиентский доступ при подключении к репликам доступности (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Требования и ограничения](#Prerequisites)  
  
     [Безопасность](#Security)  
  
-   **Настройка доступа к реплике доступности с использованием:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Дальнейшие действия:** [после настройки доступа только для чтения для реплики доступности](#FollowUp)  
  
-   [Связанные задачи](#RelatedTasks)  
  
-   [См. также](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Требования и ограничения  
  
-   Если нужно настроить разный доступ к подключениям, необходимо подключиться к экземпляру сервера, на котором размещается первичная реплика.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
  
|Задача|Разрешения|  
|----------|-----------------|  
|Настройка реплик при создании группы доступности|Требуется членство в предопределенной роли сервера **sysadmin** и разрешение сервера CREATE AVAILABILITY GROUP, ALTER ANY AVAILABILITY GROUP или CONTROL SERVER.|  
|Изменение реплики доступности|Необходимо разрешение ALTER AVAILABILITY GROUP для группы доступности, разрешение CONTROL AVAILABILITY GROUP, разрешение ALTER ANY AVAILABILITY GROUP или разрешение CONTROL SERVER.|  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 **Настройка доступа к реплике доступности**  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена первичная реплика, и разверните дерево сервера.  
  
2.  Разверните узел **Высокий уровень доступности AlwaysOn** и узел **Группы доступности**.  
  
3.  Щелкните группу доступности, реплику которой нужно изменить.  
  
4.  Щелкните правой кнопкой мыши реплику доступности и выберите пункт **Свойства**.  
  
5.  В диалоговом окне **Свойства реплики доступности** можно изменить доступ к соединению для первичной и вторичной роли следующим образом:  
  
    -   Для вторичной роли выберите новое значение в раскрывающемся списке **Доступная для чтения вторичная** следующим образом.  
  
         **Нет**  
         Для баз данных-получателей этой реплики соединения пользователя не разрешаются. Для них не разрешен доступ для чтения. Это параметр по умолчанию.  
  
         **Назначение — только чтение**  
         Для баз данных-получателей этой реплики разрешены лишь подключения только для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
         **Да**  
         Для баз данных-получателей этой реплики разрешены все соединения, но только с доступом для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
    -   Для первичной роли выберите новое значение в раскрывающемся списке **Соединения в первичной роли** следующим образом:  
  
         **разрешить все соединения.**  
         Разрешаются все соединения с базами данных в первичной реплике. Это параметр по умолчанию.  
  
         **разрешить соединения с доступом на чтение и запись;**  
         Если свойство «Назначение приложения» имеет значение **ReadWrite** или не задано, то соединение разрешено. Соединения, у которых свойство соединения «Назначение приложения» равно **ReadOnly** , не разрешены. Таким образом, клиент не сможет по ошибке подключить рабочую нагрузку с намерением чтения к первичной реплике. Дополнительные сведения о свойстве соединения «Назначение приложения» см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Настройка доступа к реплике доступности**  
  
> [!NOTE]  
>  Пример этой процедуры см. в подразделе [Примеры (Transact-SQL)](#TsqlExample) далее в этом разделе.  
  
1.  Подключитесь к экземпляру сервера, на котором находится первичная реплика.  
  
2.  Если вы указываете реплику для новой группы доступности, воспользуйтесь инструкцией [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Если вы добавляете или изменяете реплику существующей группы доступности, воспользуйтесь инструкцией [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Чтобы настроить доступ к соединению для вторичной роли, укажите в предложении ADD REPLICA или MODIFY REPLICA WITH параметр SECONDARY_ROLE следующим образом:  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         где  
  
         NO  
         Прямые подключения для баз данных-получателей этой реплики не разрешаются. Для них не разрешен доступ для чтения. Это параметр по умолчанию.  
  
         READ_ONLY  
         Для баз данных-получателей этой реплики разрешены лишь подключения только для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
         ALL  
         Для баз данных-получателей этой реплики разрешены все соединения, но только с доступом для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
3.  Чтобы настроить доступ к соединению для первичной роли, укажите в предложении ADD REPLICA или MODIFY REPLICA WITH параметр PRIMARY_ROLE следующим образом:  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     где  
  
     READ_WRITE  
     Соединения, у которых свойство "Назначение приложения" равно **ReadOnly**, не разрешены.  Если свойство «Назначение приложения» имеет значение **ReadWrite** или не задано, то соединение разрешено. Дополнительные сведения о свойстве соединения «Назначение приложения» см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
     ALL  
     Разрешаются все соединения с базами данных в первичной реплике. Это параметр по умолчанию.  
  
###  <a name="TsqlExample"></a> Пример (Transact-SQL)  
 В следующем примере вторичная реплика добавляется в группу доступности с именем *AG2*. Для размещения новой реплики доступности указывается отдельный экземпляр сервера *COMPUTER03\HADR_INSTANCE*. В этой реплике разрешены только соединения для чтения и записи для первичной роли, а для вторичной роли разрешены соединения с намерением чтения.  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Использование PowerShell  
 **Настройка доступа к реплике доступности**  
  
> [!NOTE]  
>  Пример кода см. в подразделе [Пример (PowerShell)](#PSExample) далее в этом разделе.  
  
1.  Перейдите в каталог (**cd**) экземпляра сервера, в котором находится первичная реплика.  
  
2.  При добавлении реплики доступности в группу доступности воспользуйтесь командлетом **New-SqlAvailabilityReplica**. При изменении существующей реплики доступности воспользуйтесь командлетом **Set-SqlAvailabilityReplica**. Соответствующие параметры:  
  
    -   Чтобы настроить доступ к соединению для вторичной роли, укажите параметр **ConnectionModeInSecondaryRole***secondary_role_keyword*, где *secondary_role_keyword* равно одному из следующих значений:  
  
         **AllowNoConnections**  
         Не допускаются прямые соединения с базами данных во вторичной реплике, кроме того, к базам данных также нельзя получить доступ только для чтения. Это параметр по умолчанию.  
  
         **AllowReadIntentConnectionsOnly**  
         Разрешаются только соединения с базами данных во вторичной реплике, у которых свойство "Назначение приложения" равно **ReadOnly**. Дополнительные сведения об этом свойстве см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         К базам данных во вторичной реплике разрешаются все соединения на доступ только для чтения.  
  
    -   Чтобы настроить доступ к соединению для первичной роли, укажите параметр **ConnectionModeInPrimaryRole***primary_role_keyword*, где *primary_role_keyword* равно одному из следующих значений:  
  
         **AllowReadWriteConnections**  
         Соединения, у которых свойство «Назначение приложения» равно ReadOnly, разрешены. Если свойство «Назначение приложения» имеет значение ReadWrite либо оно не задано, то соединение разрешено. Дополнительные сведения о свойстве соединения «Назначение приложения» см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Разрешаются все соединения с базами данных в первичной реплике. Это параметр по умолчанию.  
  
    > [!NOTE]  
    >  Чтобы просмотреть синтаксис командлета, воспользуйтесь командлетом **Get-Help** в среде [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Дополнительные сведения см. в разделе [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [SQL Server PowerShell, поставщик](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> Пример (PowerShell)  
 В следующем примере параметры **ConnectionModeInSecondaryRole** и **ConnectionModeInPrimaryRole** устанавливаются в значение **AllowAllConnections**.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="FollowUp"></a> Дальнейшие действия: после настройки доступа только для чтения для реплики доступности  
 **Доступ только для чтения к к доступным для чтения вторичным репликам.**  
  
-   При использовании [bcp Utility](../../../tools/bcp-utility.md) или [sqlcmd Utility](../../../tools/sqlcmd-utility.md) можно указать доступ только для чтения к любой вторичной реплике, которой разрешен доступ только для чтения. Для этого нужно указать параметр **-K ReadOnly**.  
  
-   Обеспечение возможности подключения клиентских приложений к доступным для чтения вторичным репликам.  
  
    ||Предварительные требования|Ссылка|  
    |-|------------------|----------|  
    |![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Убедитесь, что группа доступности имеет прослушиватель.|[Создание или настройка прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Настройте маршрутизацию только для чтения в группе доступности.|[Настройка маршрутизации только для чтения в группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Факторы, которые могут повлиять на триггеры и задания после отработки отказа.**  
  
 Если имеются триггеры и задания, которые не могут выполняться в недоступной или доступной для чтения базы данных-получателе, то в скриптах триггеров и заданий следует проверять, какой базой данных является искомая реплика, базой данных-источником или базой данных-получателем, доступной для чтения. Для получения этих сведений следует использовать функцию [DATABASEPROPERTYEX](../../../t-sql/functions/databasepropertyex-transact-sql.md) , возвращающую свойство **Updatability** базы данных. Чтобы определить базу данных, доступную только для чтения, задайте в качестве значения READ_ONLY, как в примере ниже:  
  
```  
DATABASEPROPERTYEX([db name],’Updatability’) = N’READ_ONLY’  
```  
  
 Чтобы определить базу данных для чтения и записи, укажите в качестве значения READ_WRITE.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Настройка маршрутизации только для чтения в группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Создание или настройка прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> См. также  
  
-   [AlwaysOn: ценностное предложение читаемой вторичной реплики](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-value-proposition-of-readable-secondary.aspx)  
  
-   [AlwaysOn: почему есть два варианта включения вторичной реплики для читаемой рабочей нагрузки?](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [AlwaysOn: настройка читаемой вторичной реплики](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-setting-up-readable-seconary-replica.aspx)  
  
-   [AlwaysOn: я только что включил читаемую вторичную реплику, но мой запрос был заблокирован. В чем дело?](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [AlwaysOn: обеспечение доступности последних статистических данных о читаемой вторичной реплике, базе данных только для чтения и моментальном снимке базы данных](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [AlwaysOn: проблемы со статистическими данными о базе данных только для чтения, моментальном снимке базы данных и вторичной реплике](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [AlwaysOn: влияние на основную рабочую нагрузку при запуске рабочей нагрузки составления отчетов на вторичной реплике](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [AlwaysOn: влияние сопоставления рабочей нагрузки составления отчетов на вторичной реплике на изоляцию моментальных снимков](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [AlwaysOn: минимизация блокировок потока REDO при запуске рабочей нагрузки составления отчетов на вторичной реплике](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [AlwaysOn: читаемая вторичная реплика и задержка данных](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On.aspx)  
  
## См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Активные вторичные реплики. Доступ только для чтения к вторичным репликам (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Сведения о доступе клиентского подключения к репликам доступности (SQL Server)](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  