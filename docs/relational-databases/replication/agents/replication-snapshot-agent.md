---
title: "Агент моментальных снимков репликации | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Snapshot Agent, executables
- agents [SQL Server replication], Snapshot Agent
- command prompt [SQL Server replication]
- Snapshot Agent, parameter reference
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8b57f94d20f03f7d6d9ec0b71bba122548808c24
ms.lasthandoff: 04/11/2017

---
# <a name="replication-snapshot-agent"></a>Агент моментальных снимков репликации
  Агент моментальных снимков репликации — это исполняемый файл, который подготавливает файлы моментальных снимков, содержащие схему, данные опубликованных таблиц и объекты базы данных, сохраняет их в папке моментальных снимков и регистрирует задания синхронизации в базе данных распространителя.  
  
> [!NOTE]  
>  Параметры можно указывать в любом порядке.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## <a name="arguments"></a>Аргументы  
 **-?**  
 Выводит список всех доступных параметров.  
  
 **-Publisher**  *имя_сервера*[**\\***имя_экземпляра*]  
 Имя издателя. Укажите имя сервера (server_name) для экземпляра [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на этом сервере. Укажите *server_name***\\***instance_name* , чтобы обратиться к именованному экземпляру [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] по умолчанию.  
  
 **-Publication** *публикация*  
 Имя публикации. Этот параметр допустим только в том случае, если в данной публикации моментальный снимок всегда доступен для новых или повторно инициализированных подписок.  
  
 **-70Subscribers**  
 Указание обязательно в том случае, если существуют подписчики, работающие на платформе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] версии 7.0.  
  
 **-BcpBatchSize** *bcp*_ *batch*\_ *size*  
 Число строк для отправки при операции массового копирования. При выполнении операции **bcp in** размер пакета равен числу строк для отправки на сервер в одной транзакции, а также числу строк, которые необходимо отправить до того, как агент распространителя зарегистрирует сообщение о ходе выполнения от программы **bcp** . При выполнении операции **bcp out** используются пакеты фиксированного размера (1000). Значение 0 указывает на отсутствие регистрации сообщений.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 Путь к файлу определения агента. Файл определения агента содержит параметры командной строки для данного агента. Содержимое файла анализируется как для исполняемого файла. Для указания значений параметров, содержащих произвольные символы, используются двойные кавычки (").  
  
 **-Distributor** *server_name*[**\\***instance_name*]  
 Имя распространителя. Укажите *server_name* , чтобы использовать экземпляр сервера [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] по умолчанию. Укажите *имя_сервера***\\***имя_экземпляра* для именованного экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на этом сервере.  
  
 **-DistributorDeadlockPriority** [**-1**|**0**|**1**]  
 Приоритет соединения агента моментальных снимков с распространителем при возникновении взаимоблокировки. Этот параметр указывается для разрешения взаимоблокировок, которые могут возникать между агентом моментальных снимков и пользовательскими приложениями при создании моментальных снимков.  
  
|DistributorDeadlockPriority|Описание|  
|---------------------------------------|-----------------|  
|**-1**|При возникновении взаимоблокировки на распространителе агент моментальных снимков имеет меньший приоритет, чем другие приложения.|  
|**0** (по умолчанию)|Приоритет не назначается.|  
|**1**|При возникновении взаимоблокировки на распространителе агент моментальных снимков имеет больший приоритет.|  
  
 **-DistributorLogin** *distributor_login*  
 Имя входа, используемое при соединении с распространителем с проверкой подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-DistributorPassword** *distributor_password*  
 Пароль, используемый при соединении с распространителем с проверкой подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Указывает режим безопасности распространителя. Значение **0** означает проверку подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (по умолчанию), а значение **1** — проверку подлинности Windows.  
  
 **-DynamicFilterHostName** *dynamic_filter_host_name*  
 Позволяет указать значение [HOST_NAME (Transact-SQL)](../../../t-sql/functions/host-name-transact-sql.md) для фильтра, который создает динамический моментальный снимок. Так, если для какой-либо статьи указано предложение фильтра подмножества `rep_id = HOST_NAME()` и перед вызовом агента слияния свойство **DynamicFilterHostName** устанавливается в значение «FBJones», в столбце **rep_id** будет производиться репликация только тех строк, которые содержат значение «FBJones».  
  
 **-DynamicFilterLogin** *dynamic_filter_login*  
 Позволяет указать значение [SUSER_SNAME (Transact-SQL)](../../../t-sql/functions/suser-sname-transact-sql.md) для фильтра, который создает динамический моментальный снимок. Так, если для какой-либо статьи указано предложение фильтра подмножества `user_id = SUSER_SNAME()` и перед вызовом метода **Run** объекта **SQLSnapshot** установить свойство **DynamicFilterLogin** в значение «rsmith», в моментальный снимок будут включены только те строки, в которых столбец **user_id** содержит значение «rsmith».  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 Папка, в которой должен быть создан динамический моментальный снимок.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Уровень шифрования по протоколу SSL, используемый агентом моментальных снимков при установлении соединений.  
  
|Значение EncryptionLevel|Описание|  
|---------------------------|-----------------|  
|**0**|Указывает, что SSL не используется.|  
|**1**|Указывает, что SSL используется, но агент не проверяет, подписан ли сертификат сервера SSL надежным издателем.|  
|**2**|Указывает, что SSL используется и сертификат подтвержден.|  
  
 Дополнительные сведения см. в статье [Общие сведения о безопасности (репликация)](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-FieldDelimiter** *field_delimiter*  
 Символ или последовательность символов, обозначающая конец поля в файле данных массового копирования [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . По умолчанию имеет значение \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Указывает объем данных, регистрируемых в журнале при выполнении моментального снимка. Выбрав значение **1**, можно свести к минимуму влияние ведения журнала на производительность.  
  
|Значение HistoryVerboseLevel|Описание|  
|-------------------------------|-----------------|  
|**0**|Сообщения о ходе работы записываются либо в консоль, либо в выходной файл. Записи журнала не регистрируются в базе данных распространителя.|  
|**1**|Всегда обновлять предыдущее сообщение журнала с таким же состоянием (запуск, выполнение, успех и т. д.). Если предыдущих сообщений с таким состоянием нет, то вставить новую запись.|  
|**2** (по умолчанию)|Если есть сообщения о таких событиях, как состояние простоя или долго выполняемое задание, то обновить предыдущие записи, в противном случае вставить новые записи журнала.|  
|**3**|Если сообщения не о состоянии простоя, то всегда вставлять новые записи.|  
  
 **-HRBcpBlocks** *number_of_blocks*  
 Число блоков данных **bcp** , составляющих очередь между потоками модуля записи и модуля чтения. Значение по умолчанию: 50. Параметр**HRBcpBlocks** используется только с публикациями Oracle.  
  
> [!NOTE]  
>  Этот параметр используется для настройки производительности операции **bcp** из издателя Oracle.  
  
 -**HRBcpBlockSize***block_size*  
 Размер каждого блока данных программы **bcp** (в килобайтах). Значение по умолчанию — 64 КБ. Параметр**HRBcpBlocks** используется только с публикациями Oracle.  
  
> [!NOTE]  
>  Этот параметр используется для настройки производительности операции **bcp** из издателя Oracle.  
  
 **-HRBcpDynamicBlocks**  
 Указывает, возможно ли динамическое увеличение размера блоков данных **bcp** . Параметр**HRBcpBlocks** используется только с публикациями Oracle.  
  
> [!NOTE]  
>  Этот параметр используется для настройки производительности операции **bcp** из издателя Oracle.  
  
 **-KeepAliveMessageInterval** *keep_alive_interval*  
 Период ожидания в секундах, после которого агент моментальных снимков регистрирует в таблице [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) запись об ожидании сообщения от сервера. Значение по умолчанию — 300 секунд.  
  
 **-LoginTimeOut** *время_ожидания_входа_в_сек*  
 Время ожидания входа в секундах. Значение по умолчанию составляет **15** секунд.  
  
 **-MaxBcpThreads** *number_of_threads*  
 Указывает число операций массового копирования, которые можно проводить параллельно. Максимальное число потоков и соединений ODBC, которые существуют одновременно, равно меньшему из **MaxBcpThreads** и числа запросов на массовое копирование, которые появляются в транзакции синхронизации в базе данных распространителя. Значение**MaxBcpThreads** должно быть больше **0** и не имеет жестко зафиксированного максимума. Значение по умолчанию равно **1**.  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Указывает, направляются ли подписчику операции удаления, которые не имеют к нему отношения. Это направляемые подписчикам инструкции DELETE, которые относятся к строкам, не входящим в секцию соответствующего подписчика. Такие команды не влияют на целостность и конвергенцию данных, однако они могут вызвать нежелательный сетевой трафик. По умолчанию параметр **MaxNetworkOptimization** имеет значение **0**. Если задать параметру **MaxNetworkOptimization** значение **1** , то вероятность не относящихся к нему удалений будет сведена к минимуму, что позволит сократить объем сетевого трафика и оптимизировать работу сети. Однако при установке этого параметра в значение **1** может возрасти объем хранимых метаданных и снизиться производительность на издателе, если используется несколько уровней фильтров соединений и сложных фильтров подмножеств. Устанавливать значение параметра **MaxNetworkOptimization** в значение **1** следует после тщательного рассмотрения топологии репликации и только в тех случаях, когда объем трафика, инициируемого неправильными командами удаления, является неприемлемым.  
  
> [!NOTE]  
>  Значение **1** для этого параметра полезно только в тех случаях, когда параметр оптимизации синхронизации для публикации слиянием имеет значение **true** (параметр **@keep_partition_changes** для процедуры [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Output** *output_path_and_file_name*  
 Путь к выходному файлу агента. Если имя файла не указано, данные выводятся на консоль. Если указанный файл существует, то выходные данные добавляются в конец файла.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Указывает, должны ли выводимые данные быть подробными.  
  
|Значение OutputVerboseLevel|Описание|  
|------------------------------|-----------------|  
|**0**|Выводятся только сообщения об ошибках.|  
|**1** (по умолчанию)|Выводятся все сообщения отчета о состоянии (значение по умолчанию).|  
|**2**|Выводятся все сообщения об ошибках, а также сообщения отчета о состоянии, что может оказаться при отладке.|  
  
 **-PacketSize** *packet_size*  
 Размер пакета (в байтах) агента моментальных снимков при соединении с [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Значение по умолчанию — 8192 байт.  
  
> [!NOTE]  
>  Не изменяйте размер пакета, если нет уверенности в том, что это повысит производительность. Для большинства приложений оптимальным является размер пакета, установленный по умолчанию.  
  
 **-ProfileName** *имя_профиля*  
 Указывает профиль агента, из которого берутся параметры агента. Если **ProfileName** имеет значение NULL, профиль агента отключен. Если значение **ProfileName** не указано, используется профиль по умолчанию для агентов этого типа. Дополнительные сведения см. в статье [Профили агента репликации](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** *publisher_database*  
 Имя базы данных публикации. *Этот параметр не поддерживается для издателей Oracle*.  
  
 **-PublisherDeadlockPriority** [**-1**|**0**|**1**]  
 Приоритет соединения агента моментальных снимков с издателем при возникновении взаимоблокировки. Этот параметр указывается для разрешения взаимоблокировок, которые могут возникать между агентом моментальных снимков и пользовательскими приложениями при создании моментальных снимков.  
  
|Значение PublisherDeadlockPriority|Описание|  
|-------------------------------------|-----------------|  
|**-1**|При возникновении взаимоблокировки на издателе агент моментальных снимков имеет меньший приоритет, чем другие приложения.|  
|**0** (по умолчанию)|Приоритет не назначается.|  
|**1**|При возникновении взаимоблокировки на издателе агент моментальных снимков имеет больший приоритет.|  
  
 **-PublisherFailoverPartner** *имя_сервера*[**\\***имя_экземпляра*]  
 Указывает партнера по обеспечению отработки отказа служб [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , участвующего в сеансе зеркального отображения базы данных с базой данных публикации. Дополнительные сведения см. в статье [Database Mirroring and Replication &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** *publisher_login*  
 Имя входа при соединении с издателем с проверкой подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-PublisherPassword**  *пароль_на_издателе*  
 Пароль, используемый при соединении с издателем с проверкой подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Указывает режим безопасности издателя. Значение **0** означает проверку подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (по умолчанию), а значение **1** — проверку подлинности Windows.  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 Время ожидания запроса в секундах. Значение по умолчанию — 1800 секунд.  
  
 **-ReplicationType** [ **1**| **2**]  
 Указывает тип репликации. Значение **1** указывает на репликацию транзакций, а значение **2** — на репликацию слиянием.  
  
 **-RowDelimiter** *разделитель_строк*  
 Символ или последовательность символов, обозначающая конец строки в файле данных массового копирования [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . По умолчанию имеет значение \n\<,@g>\n.  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 Максимальное время ожидания (в секундах) агента моментальных снимков в ситуациях, когда число параллельно выполняемых процессов динамических моментальных снимков достигло предельного значения, заданного свойством **@max_concurrent_dynamic_snapshots** хранимой процедуры [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Если по истечении этого времени агент моментальных снимков все еще находится в процессе ожидания, то его работа будет завершена. Значение 0 означает, что агент ждет неопределенно долгое время, хотя его выполнение может быть отменено.  
  
 \- **UsePerArticleContentsView** *use_per_article_contents_view*  
 Этот параметр устарел и поддерживается только для обеспечения обратной совместимости.  
  
## <a name="remarks"></a>Замечания  
  
> [!IMPORTANT]  
>  Если агент [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] установлен для запуска от учетной записи пользователя не домена (по умолчанию), а локальной системы, то служба имеет доступ только к локальному компьютеру. Если агент моментальных снимков, запускаемый агентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , настроен для входа в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]с проверкой подлинности Windows, то работа агента моментальных снимков завершится ошибкой. Значением по умолчанию является проверка подлинности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Чтобы запустить агент моментальных снимков, из командной строки выполните файл **snapshot.exe** . Дополнительные сведения см. в разделе [Исполняемые объекты агента репликации](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>См. также:  
 [Администрирование агента репликации](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  