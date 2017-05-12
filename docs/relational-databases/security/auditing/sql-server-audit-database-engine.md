---
title: "Подсистема аудита SQL Server (ядро СУБД) | Документация Майкрософт"
ms.custom: 
ms.date: 11/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- audit
helpviewer_keywords:
- SQL Server Audit
- audits [SQL Server], SQL Server Audit
ms.assetid: 0c1fca2e-f22b-4fe8-806f-c87806664f00
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f00c5db3574f21010e682f964d06f3c2b61a1d09
ms.openlocfilehash: 7852b00948b193a07e4ac38d1ace6135a63bc599
ms.lasthandoff: 04/29/2017

---
# <a name="sql-server-audit-database-engine"></a>Подсистема аудита SQL Server (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  *Аудит* экземпляра среды [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] или отдельной базы данных включает в себя отслеживание и протоколирование событий, происходящих в компоненте [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Аудит среды[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] позволяет проводить аудит сервера, который может включать в себя спецификации аудита сервера для событий на уровне сервера, а также спецификации аудита базы данных для событий на уровне базы данных. События аудита могут записываться в журналы событий или файлы аудита.  
  
 В [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]доступно несколько уровней аудита, применение которых зависит от существующих требований или стандартов установки. Подсистема аудита[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предоставляет средства и процессы, необходимые для включения, хранения и просмотра аудитов на различных объектах серверов и баз данных.  
  
 Группы действий аудита сервера можно записывать для всего экземпляра, а также группы действий аудита базы данных либо действия аудита базы данных для каждой базы данных. Событие аудита будет происходить каждый раз при обнаружении действия, подлежащего аудиту.  
  
 Аудит на уровне сервера поддерживается во всех выпусках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Все выпуски поддерживают аудит на уровне базы данных, начиная с [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] с пакетом обновления 1 (SP1). Раньше аудит на уровне базы банных был доступен только в выпусках Enterprise Edition, Developer Edition и Evaluation Edition. Дополнительные сведения см. в разделе [Функции, поддерживаемые различными выпусками SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
> [!NOTE]  
>  Этот раздел относится к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  Дополнительные сведения для [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]см. в статье [Приступая к работе с аудитом базы данных SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/).  
  
## <a name="sql-server-audit-components"></a>Компоненты подсистемы аудита SQL Server  
 *Аудит* — это сочетание в едином пакете нескольких элементов для определенной группы действий сервера или базы данных. Компоненты подсистемы аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] совместно формируют выходные данные, называемые аудитом, аналогично тому, как определение отчета в сочетании с элементами графики и данных формирует отчет.  
  
 Подсистема аудита[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] использует *расширенные события* для создания аудита. Дополнительные сведения о расширенных событиях см. в разделе [Расширенные события](../../../relational-databases/extended-events/extended-events.md).  
  
### <a name="sql-server-audit"></a>подсистема аудита SQL Server  
 Объект *Подсистема аудита SQL Server* объединяет отдельные экземпляры действий или групп действий уровня сервера или базы данных, за которыми нужно проводить наблюдение. Аудит работает на уровне экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . На одном экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] может существовать несколько аудитов.  
  
 При определении аудита задается место для вывода результатов. Оно называется назначением аудита. Аудит создается в *отключенном* состоянии и не выполняет автоматический аудит никаких действий. После включения аудита назначение аудита начинает получать от него данные.  
  
### <a name="server-audit-specification"></a>Спецификация аудита сервера  
 Объект *Спецификация аудита сервера* принадлежит аудиту. Для каждого аудита вы можете создать один объект спецификации аудита сервера, поскольку они оба создаются в области экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Спецификация аудита сервера собирает множество групп действий уровня сервера, вызываемых компонентом расширенных событий. В спецификацию аудита сервера можно включить *группы действий аудита* . Группы действий аудита — это стандартные группы действий, являющиеся атомарными событиями, происходящими в компоненте [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Эти действия передаются аудиту, который регистрирует их в целевом объекте.  
  
 Группы действий аудита уровня базы данных описываются в разделе [Действия и группы действий подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
### <a name="database-audit-specification"></a>Спецификация аудита базы данных  
 Объект *Спецификация аудита базы данных* также принадлежит подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Для каждого аудита каждой базы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] можно создать одну спецификацию аудита базы данных.  
  
 Спецификация аудита базы данных включает действия аудита уровня базы данных, вызываемые компонентом расширенных событий. В спецификацию аудита базы данных можно добавлять либо группы действий аудита, либо события аудита. *События аудита* — это атомарные события, аудит которых может производиться ядром [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . *Группы действий аудита* — это стандартные группы действий. Они расположены в области базы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Эти действия передаются аудиту, который регистрирует их в целевом объекте. Не включайте объекты области сервера, такие как системные представления, в пользовательскую спецификацию аудита базы данных.  
  
 Группы действий подсистемы аудита уровня базы данных и действия подсистемы аудита описываются в разделе [Действия и группы действий подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
### <a name="target"></a>Цель  
 Результаты аудита отправляются цели, которая может быть файлом, журналом событий безопасности Windows или журналом событий приложений Windows. Журналы необходимо периодически просматривать и архивировать, чтобы у цели оставалось достаточно места для создания дополнительных записей.  
  
> [!IMPORTANT]  
>  Любой прошедший проверку пользователь может осуществлять чтение и запись в журнале событий приложений. Для работы с журналом событий приложений необходимо меньше разрешений, чем для работы с журналом событий безопасности Windows; журнал событий приложений менее защищен, чем журнал событий безопасности Windows.  
  
 Для записи в журнал событий безопасности Windows необходимо добавить в политику [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Создание аудитов безопасности **учетную запись службы** . По умолчанию в эту политику входят учетные записи «Локальная система», «Локальная служба» и «Сетевая служба». Этот параметр можно настроить с помощью оснастки политики безопасности (secpol.msc). Кроме того, политика безопасности **Аудит доступа к объектам** должна быть включена для регистрации как **успешных** , так и **неуспешных**действий. Этот параметр можно настроить с помощью оснастки политики безопасности (secpol.msc). В ОС [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] и Windows Server 2008 можно проводить более детальную настройку **создаваемых приложением** политик из командной строки с помощью программы политики аудита (**AuditPol.exe)**. Дополнительные сведения по включению функции записи в журнал безопасности Windows см. в разделе [Запись событий подсистемы аудита SQL Server в журнал безопасности](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md). Дополнительные сведения о программе Auditpol.exe см. в статье базы знаний 921469 [Использование групповой политики для детальной настройки аудита безопасности](http://support.microsoft.com/kb/921469/). Журналы событий Windows являются глобальными для операционной системы Windows. Дополнительные сведения о журналах событий Windows см. в разделе [Общие сведения о средстве просмотра событий](http://go.microsoft.com/fwlink/?LinkId=101455). Если для аудита необходимы более точные разрешения, используйте назначение «двоичный файл».  
  
 Если данные аудита сохраняются в файл, то для предотвращения подмены можно ограничить доступ к файлу следующим образом.  
  
-   Учетная запись службы [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] должна обладать разрешением на чтение и запись.  
  
-   Администраторам аудита обычно требуется разрешение на чтение и запись. Здесь подразумевается, что администраторы аудита — это учетные записи Windows, предназначенные для администрирования файлов аудита, в том числе копирования их в другие общие папки, резервного копирования и других операций.  
  
-   Агенты чтения аудита должны иметь разрешение только для чтения файлов аудита.  
  
 Даже если запись в файл выполняется компонентом [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , другие пользователи Windows могут прочитать файл аудита, если имеют нужное разрешение. Компонент [!INCLUDE[ssDE](../../../includes/ssde-md.md)] не получает монопольную блокировку, запрещающую операции чтения.  
  
 Поскольку компонент [!INCLUDE[ssDE](../../../includes/ssde-md.md)] может получать доступ к файлу, то имена входа [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , имеющие разрешение CONTROL SERVER, могут использовать компонент [!INCLUDE[ssDE](../../../includes/ssde-md.md)] для доступа к файлам аудита. Чтобы зарегистрировать пользователей, читающих файлы аудита, определите аудит в функции master.sys.fn_get_audit_file. В результате будут записаны имена входа с разрешением CONTROL SERVER, которые получали доступ к файлу аудита через [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Если администратор аудита скопирует файл в другое место (в целях архивирования или по другой причине), то список управления доступом к новому месту следует сократить до следующего набора разрешений:  
  
-   администратор аудита — чтение и запись;  
  
-   агент чтения аудита — только чтение.  
  
 Рекомендуется создавать отчеты аудита в отдельном экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], например в экземпляре [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)], к которому будут иметь доступ только администраторы аудита и агенты чтения аудита. Использование отдельного экземпляра компонента [!INCLUDE[ssDE](../../../includes/ssde-md.md)] для составления отчетов помогает предотвратить несанкционированный доступ пользователей к записям аудита.  
  
 Можно обеспечить дополнительную защиту от несанкционированного доступа путем шифрования папки, в которой хранится файл аудита, с применением шифрования диска Windows BitLocker или шифрованной файловой системы Windows (EFS).  
  
 Дополнительные сведения о записях аудита, записываемых в целевое назначение, см. в разделе [Записи подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-records.md).  
  
## <a name="overview-of-using-sql-server-audit"></a>Общие сведения об использовании подсистемы аудита SQL Server  
 Для определения аудита можно использовать среду [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)] . После создания и включения аудита он начнет вести записи в целевое назначение.  
  
 Просматривать журналы событий Windows можно с помощью программы **Средство просмотра событий** в Windows. Для чтения целевых файлов можно использовать **Средство просмотра журнала** в [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или функцию [fn_read_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) .  
  
 Обычно процесс создания и использования аудита происходит следующим образом.  
  
1.  Создайте аудит и определите цель.  
  
2.  Создается либо спецификация аудита сервера, либо спецификация аудита базы данных, которая сопоставляет аудит. Включается спецификация аудита.  
  
3.  Включите аудит.  
  
4.  Производится считывание событий аудита с помощью **Просмотр событий**Windows, **Средства просмотра журнала**или функции fn_get_audit_file.  
  
 Дополнительные сведения об аудите см. в разделах [Создание аудита сервера и спецификации аудита сервера](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md) и [Создание спецификации аудита для сервера и базы данных](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md).  
  
## <a name="considerations"></a>Замечания  
 В случае ошибки при инициализации аудита сервер не будет запущен. В этом случае его можно запустить, если в командную строку включить параметр **-f** .  
  
 Если ошибка аудита вызывает отключение сервера или не дает ему запуститься, поскольку для аудита был задан режим ON_FAILURE=SHUTDOWN, то в журнал будет записано событие MSG_AUDIT_FORCED_SHUTDOWN. Поскольку выключение происходит при первом возникновении этого события, это событие будет записано один раз. Это событие записывается после получения сообщения об ошибке, означающего, что аудит вызвал отключение. Администратор может обойти завершения работы, вызываемые аудитом, запустив [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] в однопользовательском режиме с использованием флага **–m** . При запуске в однопользовательском режиме будет произведено изменение настроек любого аудита, запускающегося в этом сеансе, для которого было задано условие ON_FAILURE=SHUTDOWN. Такие аудиты будут запускаться с условием ON_FAILURE=CONTINUE. Если [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] запускается с использованием флага **–m** , то в журнал ошибок будет записано сообщение MSG_AUDIT_SHUTDOWN_BYPASSED.  
  
 Дополнительные сведения о параметрах запуска службы см. в разделе [Параметры запуска службы Database Engine](../../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
### <a name="attaching-a-database-with-an-audit-defined"></a>Присоединение базы данных с определенным аудитом  
 При присоединении базы данных, имеющей спецификацию аудита с идентификатором GUID, который не существует на сервере, такая спецификация аудита получит состояние *потерянная* . Поскольку в экземпляре сервера не существует аудита с совпадающим идентификатором GUID, события аудита записываться не будут. Исправить эту ситуацию можно, используя команду ALTER DATABASE AUDIT SPECIFICATION для присоединения потерянной спецификации аудита к существующему аудиту сервера. Также можно использовать команду CREATE SERVER AUDIT для создания на сервере нового аудита с указанным идентификатором GUID.  
  
 Базу данных, для которой была задана спецификация аудита, можно присоединить к другому выпуску [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , не поддерживающему подсистему аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , например [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] , но запись событий аудита производиться не будет.  
  
### <a name="database-mirroring-and-sql-server-audit"></a>Зеркальное отображение баз данных и подсистема аудита SQL Server  
 Если для базы данных определена спецификация аудита базы данных и используется зеркальное отображение базы данных, то в нее будет включена спецификация аудита базы данных. Для правильной работы на зеркальном экземпляре SQL необходимо выполнить настройку следующих элементов.  
  
-   Чтобы спецификация аудита базы данных могла создавать записи аудита, на зеркальном сервере должен присутствовать аудит с тем же идентификатором GUID. Это можно настроить с помощью команды CREATE AUDIT WITH GUID**=***\<идентификатор GUID подсистемы аудита целевого сервера*>.  
  
-   При использовании в качестве цели двоичного файла учетная запись службы зеркального сервера должна обладать необходимыми разрешениями на место назначения, куда производится запись аудиторского следа.  
  
-   При использовании в качестве целей журналов событий Windows политика безопасности на компьютере, на котором расположен зеркальный сервер, должна разрешать учетной записи службы доступ к журналу событий безопасности или приложений.  
  
### <a name="auditing-administrators"></a>Администраторы аудита  
 Члены предопределенной роли сервера **sysadmin** определены как пользователь **dbo** в каждой базе данных. Действия аудита администраторов выполняются как действия аудита пользователя **dbo** .  
  
## <a name="creating-and-managing-audits-with-transact-sql"></a>Создание аудита и работа с ним на Transact-SQL  
 Для реализации всех аспектов аудита среды [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] можно использовать инструкции DDL, представления каталогов и динамические административные представления и функции.  
  
### <a name="data-definition-language-statements"></a>Инструкции языка определения данных DDL  
 Чтобы создать, изменить или удалить спецификацию аудита, можно использовать следующие инструкции DDL.  
  
|||  
|-|-|  
|[ALTER AUTHORIZATION](../../../t-sql/statements/alter-authorization-transact-sql.md)|[CREATE SERVER AUDIT](../../../t-sql/statements/create-server-audit-transact-sql.md)|  
|[ALTER DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)|[CREATE SERVER AUDIT SPECIFICATION](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)|  
|[ALTER SERVER AUDIT](../../../t-sql/statements/alter-server-audit-transact-sql.md)|[DROP DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)|  
|[ALTER SERVER AUDIT SPECIFICATION](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)|[DROP SERVER AUDIT](../../../t-sql/statements/drop-server-audit-transact-sql.md)|  
|[CREATE DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)|[DROP SERVER AUDIT SPECIFICATION](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)|  
  
### <a name="dynamic-views-and-functions"></a>Динамические представления и функции  
 В следующей таблице перечисляются динамические представления и функции, которые можно использовать в подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Динамические представления и функции|Description|  
|---------------------------------|-----------------|  
|[sys.dm_audit_actions](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)|Возвращает строку для каждого действия аудита, которое может быть зарегистрировано в журнале аудита, и каждой группы действий аудита, которая может быть настроена в составе аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[sys.dm_server_audit_status](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)|Предоставляет сведения о текущем состоянии аудита.|  
|[sys.dm_audit_class_type_map](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)|Возвращает таблицу, которая сопоставляет поле class_type в журнале аудита с полем class_desc в представлении sys.dm_audit_actions.|  
|[fn_get_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)|Возвращает сведения из файла аудита, созданного аудитом сервера.|  
  
### <a name="catalog-views"></a>Представления каталога  
 В следующей таблице перечисляются представления каталога, которые можно использовать в подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Представления каталога|Description|  
|-------------------|-----------------|  
|[sys.database_ audit_specifications](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)|Содержит сведения о спецификациях аудита базы данных в аудите [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на экземпляре сервера.|  
|[sys.database_audit_specification_details](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)|Содержит сведения о спецификациях аудита базы данных в аудите [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на экземпляре сервера для всех баз данных.|  
|[sys.server_audits](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)|Содержит по одной строке для каждого аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] в экземпляре сервера.|  
|[sys.server_audit_specifications](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)|Содержит сведения о спецификациях аудита сервера в подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на экземпляре сервера.|  
|[sys.server_audit_specifications_details](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)|Содержит сведения об элементах (действиях) спецификации аудита сервера в подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на экземпляре сервера.|  
|[sys.server_file_audits](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)|Содержит расширенные сведения о типах аудита файлов в подсистеме аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на экземпляре сервера.|  
  
## <a name="permissions"></a>Разрешения  
 У каждой функции и команды подсистемы аудита [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] существуют индивидуальные требования к разрешениям.  
  
 Чтобы создать, изменить или удалить аудит сервера или спецификацию аудита сервера, участникам на уровне сервера требуется разрешение ALTER ANY SERVER AUDIT или CONTROL SERVER. Чтобы создать, изменить или удалить спецификацию аудита базы данных, участникам базы данных требуется разрешение ALTER ANY DATABASE AUDIT либо разрешение ALTER или CONTROL на эту базу данных. Кроме того, участникам необходимо разрешение на подключение к базе данных либо разрешение ALTER ANY SERVER AUDIT или CONTROL SERVER.  
  
 Разрешение VIEW ANY DEFINITION предоставляет доступ на просмотр представлений аудита на уровне сервера, а разрешение VIEW DEFINITION — на уровне базы данных. В случае отказа в этих разрешениях возможность просматривать представления каталога переопределяется, даже если субъект имеет разрешения ALTER ANY SERVER AUDIT или ALTER ANY DATABASE AUDIT.  
  
 Дополнительные сведения о предоставлении прав и разрешений см. в разделе [GRANT (Transact-SQL)](../../../t-sql/statements/grant-transact-sql.md).  
  
> [!CAUTION]  
>  Члены роли sysadmin могут изменять любой компонент аудита; члены роли db_owner могут изменять спецификации аудита в базе данных. Подсистема аудита[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] выполнит проверку наличия у имени входа, пытающегося выполнить создание или изменение спецификации аудита (хотя бы разрешения ALTER ANY DATABASE AUDIT). Однако при присоединении базы данных проверка не производится. Следует считать, что спецификации аудита базы данных настолько надежны, насколько надежны участники, имеющие роли sysadmin или db_owner.  
  
## <a name="related-tasks"></a>Связанные задачи  
 [Создание аудита сервера и спецификации аудита сервера](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [Создание спецификации аудита для сервера и базы данных](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [Просмотр журнала подсистемы аудита SQL Server](../../../relational-databases/security/auditing/view-a-sql-server-audit-log.md)  
  
 [Запись событий подсистемы аудита SQL Server в журнал безопасности](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
## <a name="topics-closely-related-to-auditing"></a>Темы, тесно связанные с аудитом  
 [Свойства сервера (страница "Безопасность")](../../../database-engine/configure-windows/server-properties-security-page.md)  
 Описывает, как включить аудит входа в систему для [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Записи аудита хранятся в журнале приложений Windows.  
  
 [Параметр конфигурации сервера "c2 audit mode"](../../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)  
 Описывается режим аудита в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], соответствующий стандарту безопасности С2.  
  
 [Категория событий Security Audit (приложение SQL Server Profiler)](../../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md)  
 Описываются события аудита, которые можно использовать в приложении [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Дополнительные сведения см. в разделе [Start SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md).  
  
 [Трассировка SQL](../../../relational-databases/sql-trace/sql-trace.md)  
 Объясняется, как в пользовательских приложениях можно использовать приложение трассировки SQL вместо приложения [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Profiler.  
  
 [Триггеры DDL](../../../relational-databases/triggers/ddl-triggers.md)  
 Объясняется, как можно использовать триггеры языка DDL для отслеживания изменения в базах данных.  
  
 [Microsoft TechNet, технический центр SQL Server: "SQL Server 2005 — безопасность и защита"](http://go.microsoft.com/fwlink/?LinkId=101152)  
 Содержит актуальные сведения о безопасности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также:  
 [Действия и группы действий подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)   
 [Записи подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-records.md)  
  
  

