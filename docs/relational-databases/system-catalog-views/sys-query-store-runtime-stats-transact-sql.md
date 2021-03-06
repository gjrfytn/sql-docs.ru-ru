---
title: sys.query_store_runtime_stats (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3392bcde00439981a401c908ca7a1898d9d026f5
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242312"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Содержит сведения о сведений о статистике выполнения среды выполнения для запроса.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**BIGINT**|Идентификатор строки, представляющее статистические данные для **plan_id**, **execution_type** и **runtime_stats_interval_id**. Он уникален только для последних интервалов статистики среды выполнения. Для активной интервал может быть несколько строк, представляющих статистику времени выполнения для плана, который ссылается **plan_id**, с помощью выполнения тип, представленный **execution_type**. Как правило, одна строка представляет статистику времени выполнения, в который записываются на диск, тогда как другие (s) представляют собой состояние в памяти. Таким образом, чтобы получить фактическое состояние для каждого интервала необходимо выполнять статистическое вычисление метрик, Группировка по **plan_id**, **execution_type** и **runtime_stats_interval_id**.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**plan_id**|**BIGINT**|Внешний ключ. Присоединяет к [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**BIGINT**|Внешний ключ. Присоединяет к [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**TINYINT**|Определяет тип выполнения запроса.<br /><br /> 0 — обычное выполнение (успешно завершено)<br /><br /> 3 - клиент прервал выполнение<br /><br /> 4 - исключение прервал выполнение|  
|**execution_type_desc**|**nvarchar(128)**|Текстовое описание выполнения тип поля:<br /><br /> 0 — обычный<br /><br /> 3 — прервано<br /><br /> 4 - исключение|  
|**first_execution_time**|**datetimeoffset**|Время первого выполнения для плана запроса в пределах интервала статистической обработки.|  
|**last_execution_time**|**datetimeoffset**|Время последнего выполнения запроса план в пределах интервала статистической обработки.|  
|**count_executions**|**BIGINT**|Общее число выполнений для плана запроса в пределах интервала статистической обработки.|  
|**avg_duration**|**FLOAT**|Средняя длительность для плана запроса в течение интервала статистической обработки (указывается в микросекундах).|  
|**last_duration**|**BIGINT**|Последняя длительность запроса план в пределах интервала статистической обработки (указывается в микросекундах).|  
|**min_duration**|**BIGINT**|Минимальная длительность для плана запроса в течение интервала статистической обработки (указывается в микросекундах).|  
|**max_duration**|**BIGINT**|Максимальная длительность для плана запроса в течение интервала статистической обработки (указывается в микросекундах).|  
|**stdev_duration**|**FLOAT**|Длительность стандартное отклонение для плана запроса в течение интервала статистической обработки (указывается в микросекундах).|  
|**avg_cpu_time**|**FLOAT**|Среднее время ЦП для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_cpu_time**|**BIGINT**|Последнее время ЦП для запроса план в пределах интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_cpu_time**|**BIGINT**|Минимальное время ЦП для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_cpu_time**|**BIGINT**|Максимальное время ЦП для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_cpu_time**|**FLOAT**|Стандартное отклонение времени ЦП для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_logical_io_reads**|**FLOAT**|Среднее число логических операций ввода-ВЫВОДА считывает для плана запроса в пределах интервала статистической обработки. (в виде числа Чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_logical_io_reads**|**BIGINT**|Число последних логических операций ввода-ВЫВОДА считывает для плана запроса в пределах интервала статистической обработки. (в виде числа Чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_logical_io_reads**|**BIGINT**|Минимальное число логических операций ввода-ВЫВОДА считывает для плана запроса в пределах интервала статистической обработки. (в виде числа Чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_logical_io_reads**|**BIGINT**|Максимальное число логических операций ввода-ВЫВОДА считывает для плана запроса в пределах интервала статистической обработки. (в виде числа Чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_logical_io_reads**|**FLOAT**|Число логических операций ввода-ВЫВОДА чтения стандартное отклонение для плана запроса в пределах интервала статистической обработки. (в виде числа Чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_logical_io_writes**|**FLOAT**|Среднее число логических операций ввода-ВЫВОДА записывает для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_logical_io_writes**|**BIGINT**|Число последних логических операций ввода-ВЫВОДА записывает для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_logical_io_writes**|**BIGINT**|Минимальное число логических операций ввода-ВЫВОДА записывает для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_logical_io_writes**|**BIGINT**|Максимальное число логических операций ввода-ВЫВОДА записывает для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_logical_io_writes**|**FLOAT**|Число логических операций ввода-ВЫВОДА записи стандартное отклонение для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_physical_io_reads**|**FLOAT**|Среднее число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выраженное как количество чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_physical_io_reads**|**BIGINT**|Последнее число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выраженное как количество чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_physical_io_reads**|**BIGINT**|Минимальное число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выраженное как количество чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_physical_io_reads**|**BIGINT**|Максимальное число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выраженное как количество чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_physical_io_reads**|**FLOAT**|Число физических операций ввода-ВЫВОДА чтения стандартное отклонение для плана запроса в течение интервала статистической обработки (выраженное как количество чтений страниц размером 8 КБ).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_clr_time**|**FLOAT**|Среднее время CLR для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_clr_time**|**BIGINT**|Последнее время среды CLR для запроса план в пределах интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_clr_time**|**BIGINT**|Минимальное время среды CLR для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_clr_time**|**BIGINT**|Максимальное время среды CLR для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_clr_time**|**FLOAT**|Стандартное отклонение времени со средой CLR для плана запроса в течение интервала статистической обработки (указывается в микросекундах).<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_dop**|**FLOAT**|Среднее значение DOP (степень параллелизма) для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_dop**|**BIGINT**|Последние DOP (степень параллелизма) для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_dop**|**BIGINT**|Минимальное значение DOP (степень параллелизма) для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_dop**|**BIGINT**|Максимальная DOP (степень параллелизма) для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_dop**|**FLOAT**|Стандартное отклонение DOP (степень параллелизма) для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_query_max_used_memory**|**FLOAT**|Среднее выделение памяти (указывается как число страниц размером 8 КБ) для плана запроса в пределах интервала статистической обработки. Всегда 0 для запросов с помощью изначально скомпилированы процедуры оптимизированных для памяти.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_query_max_used_memory**|**BIGINT**|Последний временно предоставляемого буфера памяти (указывается как число страниц размером 8 КБ) для плана запроса в пределах интервала статистической обработки. Всегда 0 для запросов с помощью изначально скомпилированы процедуры оптимизированных для памяти.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_query_max_used_memory**|**BIGINT**|Минимальный объем памяти grant (указывается как число страниц размером 8 КБ) для плана запроса в пределах интервала статистической обработки. Всегда 0 для запросов с помощью изначально скомпилированы процедуры оптимизированных для памяти.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_query_max_used_memory**|**BIGINT**|Максимальный объем предоставляемой памяти (указывается как число страниц размером 8 КБ) для плана запроса в пределах интервала статистической обработки. Всегда 0 для запросов с помощью изначально скомпилированы процедуры оптимизированных для памяти.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_query_max_used_memory**|**FLOAT**|Стандартное отклонение (указывается как число страниц размером 8 КБ) на выделение памяти для плана запроса в пределах интервала статистической обработки. Всегда 0 для запросов с помощью изначально скомпилированы процедуры оптимизированных для памяти.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**avg_rowcount**|**FLOAT**|Среднее число возвращенных строк для плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_rowcount**|**BIGINT**|Число возвращенных строк с последнего выполнения плана запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_rowcount**|**BIGINT**|Минимальное число возвращенных строк для запроса план в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_rowcount**|**BIGINT**|Максимальное число возвращенных строк для запроса план в пределах интервала статистической обработки.|  
|**stdev_rowcount**|**FLOAT**|Число строк, возвращаемых стандартное отклонение для плана запроса в пределах интервала статистической обработки.|
|**avg_log_bytes_used**|**FLOAT**|Среднее число байтов в журнале базы данных, используемые планом запроса, в течение интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**last_log_bytes_used**|**BIGINT**|Число байтов в журнале базы данных, используемых для последнего выполнения плана запроса, в течение интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**min_log_bytes_used**|**BIGINT**|Минимальное число байтов в журнале базы данных, используемые планом запроса, в течение интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**max_log_bytes_used**|**BIGINT**|Максимальное число байтов в журнале базы данных, используемые планом запроса, в течение интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
|**stdev_log_bytes_used**|**FLOAT**|Стандартное отклонение число байтов в журнале базы данных, используемый план запроса в пределах интервала статистической обработки.<br/>**Примечание.** Хранилище данных SQL Azure всегда будет возвращать нуль (0).|
  
## <a name="permissions"></a>Разрешения  
 Требуется **VIEW DATABASE STATE** разрешение.  
  
## <a name="see-also"></a>См. также  
 [sys.database_query_store_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Хранимые процедуры в хранилище запросов (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
