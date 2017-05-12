---
title: "Новые возможности индексов columnstore | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe5ea05-5b19-45a4-9b7a-8ae5ca367897
caps.latest.revision: 28
author: barbkess
ms.author: barbkess
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8dc55e28462cd04a90274ada860fd418bcc54775
ms.lasthandoff: 04/11/2017

---
# <a name="columnstore-indexes---what39s-new"></a>Новые возможности индексов columnstore
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Сводка функций columnstore, доступных для каждой версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]и последних выпусков Premium для базы данных SQL Microsoft Azure, хранилища данных SQL Azure и хранилища данных Parallel Data Warehouse.  

 >[!NOTE]
 > Для базы данных SQL Azure индексы columnstore доступны только в выпуске Premium.
 
## <a name="feature-summary-for-product-releases"></a>Сводка функций по выпускам  
 В следующей таблице перечислены основные функции для индексов columnstore и продукты, в которых они доступны.  

  
|Функция индекса columnstore|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|  
|Пакетное выполнение для многопоточных запросов.|да|да|да|да|да|  
|Пакетное выполнение для однопоточных запросов.|||да|да|да|  
|Параметр сжатия архивации.||да|да|да|да|  
|Изоляция моментальных снимков и изоляция моментальных снимков read committed.|||да|да|да|  
|Указание индекса columnstore при создании таблицы.|||да|да|да|  
|AlwaysOn поддерживает индексы columnstore.|да|да|да|да|да|  
|Вторичная реплика для чтения AlwaysOn поддерживает некластеризованные индексы columnstore только для чтения.|да|да|да|да|да|  
|Вторичная реплика для чтения AlwaysOn поддерживает обновляемые индексы columnstore.|||да|||  
|Некластеризованный индекс columnstore только для чтения в куче или сбалансированном дереве.|да|да|да *|да *|да *|  
|Обновляемый некластеризованный индекс columnstore в куче или сбалансированном дереве.|||да|да|да|  
|Разрешены дополнительные индексы сбалансированного дерева в куче или сбалансированном дереве с некластеризованным индексом columnstore.|да|да|да|да|да|  
|Обновляемый кластеризованный индекс columnstore.||да|да|да|да|  
|Индекс сбалансированного дерева в кластеризованном индексе columnstore.|||да|да|да|  
|Индекс columnstore в таблице, оптимизированной для памяти.|||да|да|да|  
|Определение некластеризованного индекса columnstore поддерживает использование отфильтрованных условий.|||да|да|да|  
|Параметр задержки сжатия для индексов columnstore в инструкциях CREATE TABLE и ALTER TABLE.|||да|да|да|   
  
 * Чтобы создать некластеризованный индекс columnstore для чтения, сохраните индекс в файловой группе только для чтения.  
  
## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 В[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] реализованы ключевые усовершенствования для повышения производительности и гибкости индексов columnstore. Они расширяют возможности хранения данных и обеспечивают поддержку оперативной аналитики в реальном времени.  
  
### <a name="functional"></a>Функции  
  
-   Таблица rowstore может включать один обновляемый некластеризованный индекс columnstore. Ранее некластеризованный индекс columnstore был доступен только для чтения.  
  
-   Определение некластеризованного индекса columnstore поддерживает использование отфильтрованных условий. Эта функция позволяет создать некластеризованный индекс columnstore на основе только "холодных" данных операционной рабочей нагрузки. Таким образом, влияние присутствия индекса columnstore в таблице OLTP на производительность будет минимальным.  
  
-   Таблица в памяти может включать один индекс columnstore. Его можно создать при создании таблицы или добавить позже с помощью процедуры [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md). Ранее создание индекса columnstore допускалось только в таблицах на дисках.  
  
-   Кластеризованный индекс columnstore может включать один или несколько некластеризованных индексов rowstore. Ранее индекс columnstore не поддерживал некластеризованные индексы. SQL Server автоматически обслуживает некластеризованные индексы для операций DML.  
  
-   Поддержка первичных и внешних ключей путем использования индекса сбалансированного дерева для применения этих ограничений в кластеризованном индексе columnstore.  
  
-   Индексы columnstore включают параметр задержки сжатия, который сводит к минимуму влияние транзакционной рабочей нагрузки на оперативную аналитику в реальном времени.  Этот параметр позволяет стабилизировать часто изменяющиеся строки перед их сжатием в индекс columnstore. Дополнительные сведения см. в статьях [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md) и [Начало работы с Columnstore для получения операционной аналитики в реальном времени](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>Производительность для уровня совместимости базы данных 120 или 130  
  
-   Индексы columnstore поддерживают уровень изоляции моментальных снимков read committed (RCSI) и изоляцию моментальных снимков (SI). Это позволяет выполнять запросы аналитики, согласованные с транзакциями, без блокировки.  
  
-   Индекс columnstore поддерживает дефрагментацию индексов путем удаления удаленных строк без необходимости явного перестроения индекса. Инструкция ALTER INDEX... REORGANIZE удаляет удаленные строки (на основе внутренней политики) из индекса columnstore в оперативном режиме.  
  
-   Вторичная реплика для чтения AlwaysOn может получать доступ к индексам columnstore. За счет переноса запросов аналитики во вторичную реплику AlwaysOn можно повысить производительность оперативной аналитики.  
  
-   Для повышения производительности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вычисляет агрегатные функции MIN, MAX, SUM, COUNT, AVG во время сканирования таблицы, если тип данных использует не более восьми байтов и не относится к типу string. Включение агрегата поддерживается с предложением Group By и без него для кластеризованных и некластеризованных индексов columnstore.  
  
-   Включение предиката ускоряет запросы, которые сравнивают строки типа [v]char или n[v]char. Это относится к общим операторам сравнения, включая такие операторы, как LIKE, которые используют фильтры битовой карты. Этот способ работает для всех параметров сортировки, поддерживаемых SQL Server.  
  
### <a name="performance-for-database-compatibility-level-130"></a>Производительность для уровня совместимости базы данных 130  
  
-   Поддержка нового пакетного режима для запросов с помощью любой из следующих операций:  
  
    -   SORT  
  
    -   агрегаты с несколькими четко различимыми функциями (некоторые примеры: COUNT/COUNT, AVG/SUM, CHECKSUM_AGG, STDEV/STDEVP);  
  
    -   агрегатные оконные функции — COUNT, COUNT_BIG, SUM, AVG, MIN, MAX и CLR;  
  
    -   определяемые пользователем оконные агрегаты — CHECKSUM_AGG, STDEV, STDEVP, VAR, VARP и GROUPING;  
  
    -   аналитические агрегатные оконные функции — LAG< LEAD, FIRST_VALUE, LAST_VALUE, PERCENTILE_CONT, PERCENTILE_DISC, CUME_DIST и PERCENT_RANK.  
  
-   Однопоточные запросы, выполняемые с MAXDOP 1 или последовательным планом запроса, выполняются в пакетном режиме. Ранее в пакетном режиме могли выполняться только многопоточные запросы.  
  
-   Запросы к таблицам, оптимизированным для памяти, могут иметь параллельные планы в режиме взаимодействия SQL при доступе к данным как в индексе rowstore, так и в индексе columnstore.  
  
### <a name="supportability"></a>Поддержка  
 Следующие системные представления являются новыми для columnstore:  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
 Следующие представления DMV на основе OLTP в памяти содержат обновления для columnstore:  
  
-   [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)  
  
-   [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)  
  
### <a name="limitations"></a>Ограничения  
  
-   Инструкция MERGE отключена, если индекс сбалансированного дерева определен в кластеризованном индексе columnstore.  
  
-   Для таблиц в памяти индекс columnstore должен включать все столбцы; индекс columnstore не может включать отфильтрованное условие.  
  
-   Для таблиц в памяти запросы к индексу columnstore выполняются только в режиме взаимодействия, а не в собственном режиме в памяти. Поддерживается параллельное выполнение.  
  
## <a name="sql-server-2014"></a>SQL Server 2014  
 В SQL Server 2014 кластеризованный индекс columnstore был представлен в качестве основного формата хранилища. Это позволило выполнять регулярные операции загрузки, а также операции обновления, удаления и вставки.  
  
-   Таблица может использовать кластеризованный индекс columnstore в качестве основного хранилища таблиц. Использование других индексов не допускается в таблице, однако кластеризованный индекс columnstore является обновляемым, что позволяет выполнять регулярные операции загрузки и вносить изменения в отдельные строки.  
  
-   Некластеризованный индекс columnstore имеет те же функции, что и в SQL Server 2012, за исключением того, что теперь дополнительные операторы могут выполняться в пакетном режиме. Он по-прежнему не поддерживает обновление, помимо перестроения и переключения секций. Некластеризованный индекс columnstore поддерживается только в таблицах на диске, но не в таблицах в памяти.  
  
-   Кластеризованный и некластеризованный индекс columnstore включает параметр сжатия архивации, обеспечивающий дополнительное сжатие данных. Параметр архивации удобен для сокращения объема данных в памяти и на диске, однако он снижает производительность запросов. Его можно рекомендовать для редко используемых данных.  
  
-   Кластеризованный и некластеризованный индексы columnstore функционируют весьма сходным образом; они используют одинаковый формат хранения по столбцам, подсистему обработки запросов и набор динамических административных представлений. Различие заключается в типе индекса (основной и дополнительный), кроме того, некластеризованный индекс columnstore доступен только для чтения.  
  
-   Следующие операторы выполняются в пакетном режиме для многопоточных запросов: SCAN, FILTER, PROJECT, JOIN, GROUP BY и UNION ALL.  
  
## <a name="sql-server-2012"></a>SQL Server 2012  
 В SQL Server 2012 был представлен некластеризованный индекс columnstore как еще один тип индекса для таблиц rowstore и пакетной обработки запросов к данным columnstore.  
  
-   Таблица rowstore может включать один некластеризованный индекс columnstore.  
  
-   Индекс columnstore доступен только для чтения. После создания индекса columnstore нельзя обновлять таблицу с помощью операций вставки, удаления и обновления: для выполнения этих операций необходимо удалить индекс, обновить таблицу и перестроить индекс columnstore. Дополнительные данные в таблицу можно загрузить с помощью переключения секций. Преимущество переключения секций заключается в том, что можно загрузить данные без удаления и перестроения индекса columnstore.  
  
-   Индекс columnstore всегда требует дополнительного места в хранилище, как правило, на 10 % больше, чем rowstore, поскольку в нем хранятся копии данных.  
  
-   Пакетная обработка обеспечивает двукратное (и более) повышение производительности, но она доступна только для параллельного выполнения запросов.  
  
## <a name="see-also"></a>См. также:  
 Руководство по индексам Columnstore   
 Загрузка данных индексов columnstore   
 [Производительность запросов индексов columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Начало работы с Columnstore для получения операционной аналитики в реальном времени](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 Индексы сolumnstore для хранилищ данных   
 [Дефрагментация индексов columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  
