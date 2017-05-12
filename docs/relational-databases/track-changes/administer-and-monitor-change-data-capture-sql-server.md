---
title: "Администрирование и мониторинг отслеживания измененных данных (SQL Server) | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c5b04e64e1cea0c24a6695a46eac0a2f94d04cf
ms.lasthandoff: 04/11/2017

---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>Администрирование и наблюдение за отслеживанием измененных данных (SQL Server)
  В этом разделе описано, как администрировать и наблюдать за отслеживанием измененных данных.  
  
##  <a name="Capture"></a> Задание отслеживания  
 Задание отслеживания инициируется путем запуска хранимой процедуры без параметров **sp_MScdc_capture_job**. После запуска данная хранимая процедура получает из таблицы msdb.dbo.cdc_jobs значения, заданные для параметров *maxtrans*, *maxscans*, *continuous*и *pollinginterval* задания отслеживания. Затем эти настроенные значения передаются хранимой процедуре **sp_cdc_scan**в качестве параметров. Это используется для вызова процедуры **sp_replcmds** с целью просмотра журнала.  
  
### <a name="capture-job-parameters"></a>Параметры задания отслеживания  
 Чтобы понять поведение задания отслеживания, необходимо понять, как в хранимой процедуре **sp_cdc_scan**используются настраиваемые параметры.  
  
#### <a name="maxtrans-parameter"></a>Параметр maxtrans  
 Параметр *maxtrans* указывает максимальное количество транзакций, которое может быть обработано в одном цикле просмотра журнала. Если во время просмотра количество обрабатываемых транзакций достигает данного предела, то в текущую операцию просмотра больше не включаются дополнительные транзакции. После завершения цикла просмотра число обработанных транзакций всегда будет меньше или равным значению параметра *maxtrans*.  
  
#### <a name="maxscans-parameter"></a>Параметр maxscans  
 Параметр *maxscans* задает максимальное число циклов просмотра, которые предпринимаются для очистки журнала до возвращения (continuous = 0) или выполнения инструкции waitfor (continuous = 1).  
  
#### <a name="continous-parameter"></a>Параметр continous  
 Параметр *continuous* указывает, отдает ли хранимая процедура **sp_cdc_scan** управление после очистки журнала или выполнения максимального числа циклов сканирования (режим одиночного выполнения). Данный параметр также указывает, продолжает ли процедура **sp_cdc_scan** выполняться до тех пор, пока не будет явно остановлена (непрерывный режим).  
  
##### <a name="one-shot-mode"></a>Режим однократного выполнения  
 В режиме однократного выполнения задание отслеживания запрашивает выполнение хранимой процедуры **sp_cdc_scan** до *maxtrans* сканирований, чтобы попытаться очистить журнал и вернуться. Любые присутствующие в журнале транзакции, вышедшие за пределы значения *maxtrans* , будут обработаны в последующих циклах просмотра.  
  
 Режим однократного выполнения используется в управляемых проверках, когда количество обрабатываемых транзакций известно, а преимуществом является тот факт, что задание автоматически закрывается при завершении работы. Не рекомендуется использовать режим однократного выполнения в процессе эксплуатации. Это обусловлено тем, что данный режим полагается на расписание задания для управления частотой выполнения циклов просмотра.  
  
 При работе в режиме однократного выполнения можно вычислить верхнюю границу ожидаемой пропускной способности задания отслеживания, выраженную в транзакциях в секунду, использовав следующее вычисление:  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 Даже если количество времени, необходимое для просмотра журнала и заполнения таблиц изменений, не сильно отличается от нуля, средняя пропускная способность задания не может превысить значение, которое можно получить, разделив произведение максимального числа допустимых транзакций для одного просмотра и максимального числа допустимых просмотров на число секунд, которое проходит между отдельными обработками журнала.  
  
 Если бы для управления просмотрами журнала использовался режим однократного выполнения, то число секунд, проходящее между обработками журнала, должно было бы управляться расписанием задания. Если необходимо такое поведение, то для управления графиком просмотра журнала лучше использовать задание отслеживания, выполняющееся в непрерывном режиме.  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>Непрерывный режим и интервал опроса  
 В непрерывном режиме задание отслеживания запрашивает непрерывное выполнение процедуры **sp_cdc_scan** . Это позволяет хранимой процедуре управлять собственным циклом ожидания, предоставляя не только значения параметров maxtrans и maxscans, но также и значение числа секунд, проходящее между обработками журнала (интервал опроса). При выполнении в данном режиме задание отслеживания остается активным; в перерывах между просмотрами журнала выполняется инструкция **WAITFOR** .  
  
> [!NOTE]  
>  Если значение интервала опроса больше 0, то верхняя граница пропускной способности для повторяющихся заданий в режиме однократного выполнения также будет применяться и к функционированию задания в непрерывном режиме. То есть значение (*maxtrans* \* *maxscans*), разделенное на ненулевой интервал опроса, будет служить верхней границей для среднего количества транзакций, которое может быть обработано заданием отслеживания.  
  
### <a name="capture-job-customization"></a>Настройка задания отслеживания  
 К заданию отслеживания можно применить дополнительную логику для определения того, будет ли новый просмотр выполняться немедленно или перед запуском нового просмотра будет реализовываться период бездействия, вместо того чтобы полагаться на фиксированный интервал опроса. Выбор может быть основан на времени суток: например, во время пиковой активности можно установить очень большие периоды бездействия, а в конце дня можно установить значение интервала опроса, близкое к 0, что поможет завершить дневную обработку и подготовиться к еженощным выполнениям. Для определения времени просмотра и помещения в таблицы изменений всех транзакций, зафиксированных до полуночи, можно наблюдать за развитием процесса отслеживания. Это позволит заданию отслеживания завершиться для повторного запуска при запланированном ежедневном перезапуске. Заменив выполненный шаг задания, вызывающий хранимую процедуру **sp_cdc_scan** , вызовом написанной пользователем оболочки для хранимой процедуры **sp_cdc_scan**, можно небольшими усилиями обеспечить специальным образом настроенное поведение.  
  
##  <a name="Cleanup"></a> Задание очистки  
 В данном разделе предоставляются сведения о функционировании задания очистки для отслеживания измененных данных.  
  
### <a name="structure-of-the-cleanup-job"></a>Структура задания очистки  
 В системе отслеживания измененных данных для управления размером таблиц изменений используется стратегия очистки данных по истечении срока хранения. Механизм очистки состоит из задания [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] агента [!INCLUDE[tsql](../../includes/tsql-md.md)] , созданного при активации первой таблицы базы данных. Одно задание очистки управляет очисткой всех таблиц изменений базы данных; оно применяет одно значение срока хранения ко всем определенным экземплярам системы отслеживания.  
  
 Задание очистки инициируется путем запуска хранимой процедуры без параметров **sp_MScdc_cleanup_job**. После запуска данная хранимая процедура получает значение срока хранения и пороговое значение, установленные для задания очистки от **msdb.dbo.cdc_jobs**. Значение срока хранения используется для вычисления нижнего предела таблиц изменений. Указанное число минут вычисляется из максимального значения *tran_end_time* таблицы **cdc.lsn_time_mapping** для получения нового значения нижнего предела в виде значения datetime. Затем таблица "CDC.lsn_time_mapping" используется для преобразования значения datetime в соответствующее значение **Isn** . Если одно и то же время фиксации задано для нескольких значений в таблице, то номер **lsn** , соответствующий записи с наименьшим номером **lsn** выбирается в качестве нового значения нижнего предела. Данное значение **lsn** передается объекту **sp_cdc_cleanup_change_tables** , чтобы удалить записи таблиц изменений из таблиц изменений базы данных.  
  
> [!NOTE]  
>  Преимуществом использования времени фиксации недавней транзакции в качестве основы для вычисления нового значения нижнего предела является то, что это позволяет хранить сведения об изменениях в таблицах изменений в течение определенного времени. Это происходит, даже если процесс отслеживания запущен позже. Все изменения, имеющие то же время фиксации, что и значение нижнего предела, и далее представляются в таблицах изменений методом выбора наименьшего номера **lsn** , имеющего то же время фиксации, что и реальное значение нижнего предела.  
  
 Если выполняется очистка, то значение нижнего предела всех экземпляров системы отслеживания изначально обновляется в одной транзакции. Затем производится попытка удаления устаревших записей из таблиц изменений и таблицы cdc.lsn_time_mapping. Настраиваемое пороговое значение ограничивает количество записей, удаляемое в любой одиночной инструкции. Неуспешное выполнение удаления в любой отдельной таблице не повлияет на выполнение операции в остальных таблицах.  
  
### <a name="cleanup-job-customization"></a>Настройка задания очистки  
 В задании очистки присутствует возможность настройки стратегии, определяющей, какие из записей таблиц изменений подлежат удалению. В передаваемом задании очистки поддерживается только основанная на времени стратегия. В данной ситуации новое значение нижнего предела вычисляется методом вычитания допустимого срока хранения из времени фиксации последней обработанной транзакции. Поскольку лежащие в основе процедуры очистки используют вместо времени номера **lsn** , для определения наименьшего сохраняемого в таблицах изменений номера **lsn** может использоваться любое число стратегий. Только часть из этих стратегий являются полностью основанными на времени. Сведения о клиентах, например, могут быть использованы для обеспечения предохранительных мер на тот случай, если не удастся запустить последующие процессы, которым необходим доступ к таблицам изменений. Хотя в стратегии по умолчанию для очистки таблиц изменений всех баз данных используется один и тот же номер **lsn** , для выполнения очистки на уровне экземпляра системы отслеживания также можно вызвать процедуру очистки на уровне экземпляра отслеживания.  
  
##  <a name="Monitor"></a> Наблюдение за процессом отслеживания измененных данных  
 Наблюдение за процессом отслеживания измененных данных позволяет определить, правильно ли записываются изменения и насколько приемлема задержка при записи в таблицы изменений. Наблюдение также помогает выявить возможные ошибки. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] включает два динамических представления управления, которые помогают отслеживать фиксацию измененных данных: [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) и [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md).  
  
### <a name="identify-sessions-with-empty-result-sets"></a>Выявление сеансов с пустыми результирующими наборами  
 Каждая строка в административном представлении sys.dm_cdc_log_scan_sessions представляет сеанс просмотра журнала (за исключением строки с идентификатором 1). Сеанс просмотра журнала является эквивалентом одного выполнения хранимой процедуры [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md). Во время сеанса просмотр может возвратить изменения или пустой результат. Если результирующий набор пуст, то для столбца empty_scan_count в представлении sys.dm_cdc_log_scan_sessions устанавливается значение 1. Если пустые результирующие наборы встречаются последовательно (например, при непрерывном выполнении задания отслеживания), то счетчик empty_scan_count в последней существующей строке увеличивается. Например, если в представлении sys.dm_cdc_log_scan_sessions уже существует 10 строк просмотров, возвративших данные об изменениях, и пять результатов подряд были пусты, то в представлении будет содержаться 11 строк. В столбце empty_scan_count последней строки содержится значение 5. Чтобы определить сеансы, возвратившие пустой результирующий набор, выполните следующий запрос.  
  
 `SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0`  
  
### <a name="determine-latency"></a>Определение задержки  
 В административное представление sys.dm_cdc_log_scan_sessions включен столбец, записывающий задержку для каждого сеанса отслеживания. Задержка представляет собой время, прошедшее между фиксацией транзакции в исходной таблице и фиксацией последней отслеженной транзакции в таблицу изменений. Столбец задержки заполняется только для активных сеансов. У сеансов, значение в столбце empty_scan_count для которых больше 0, для столбца задержки устанавливается значение 0. Следующий запрос возвращает среднее время задержки для наиболее новых сеансов.  
  
 `SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
 Данные о задержках можно использовать для определения того, насколько быстро или медленно процесс отслеживания обрабатывает транзакции. Эти данные наиболее полезны в том случае, если процесс отслеживания выполняется непрерывно. Если процесс отслеживания выполняется по расписанию, то задержка может быть высокой, ввиду запаздывания между фиксацией транзакций в исходной таблице и выполнением процесса отслеживания по его расписанию.  
  
 Еще одним важным показателем эффективности процесса отслеживания является пропускная способность. Это среднее число команд в секунду, обрабатываемых в каждом сеансе. Для определения пропускной способности сеанса следует разделить значение в столбце command_count column на значение в столбце продолжительности. Следующий запрос возвращает среднюю пропускную способность для наиболее новых сеансов.  
  
 `SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
### <a name="use-data-collector-to-collect-sampling-data"></a>Получение выборки данных с помощью сборщика данных  
 Сборщик данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет осуществлять сбор моментальных снимков из любой таблицы или динамического административного представления и создать хранилище данных о производительности. Если для базы данных активирована система отслеживания измененных данных, то полезно создавать снимки представлений sys.dm_cdc_log_scan_sessions и sys.dm_cdc_errors с регулярными интервалами для последующего анализа. Следующая процедура настраивает сборщик данных на сбор образцов данных из административного представления sys.dm_cdc_log_scan_sessions.  
  
 **Настройка сбора данных**  
  
1.  Включите сборщик данных и настройте хранилище данных управления. Дополнительные сведения см. в разделе [Управление сбором данных](../../relational-databases/data-collection/manage-data-collection.md).  
  
2.  Выполните следующий код для создания пользовательского сборщика для отслеживания измененных данных.  
  
    ```tsql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @paramters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @paramters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @paramters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]разверните вкладку **Управление**, затем вкладку **Сбор данных**. Щелкните правой кнопкой мыши пункт **Сборщик данных о производительности CDC**, затем пункт **Запустить набор сбора данных**.  
  
4.  В хранилище данных, которое было настроено в шаге 1, найдите таблицу custom_snapshots.cdc_log_scan_data. В данной таблице предоставлен архивный моментальный снимок данных из сеансов просмотра журнала. Эти данные могут быть использованы для анализа задержки, пропускной способности и других показателей производительности во времени.  
  
## <a name="see-also"></a>См. также:  
 [Отслеживание измененных данных (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Об отслеживании измененных данных (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Включение и отключение фиксации измененных данных (SQL Server)](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Работа с информацией об изменениях (SQL Server)](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  