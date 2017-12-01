---
title: "sys.query_store_runtime_stats (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs: TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cf026cb9beff10c6570a94bdd805aa2b78c0a4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Содержит сведения о сведений о статистике выполнения среды выполнения для запроса.  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Идентификатор строки, представляющий статистические данные для **plan_id**, **execution_type** и **runtime_stats_interval_id**. Он уникален только для последних интервалов статистики среды выполнения. Для активной интервала может быть несколько строк, представляющих Статистика времени выполнения для плана, на который указывает **plan_id**, с помощью выполнения типа, представленного **execution_type**. Как правило, одна строка представляет статистику времени выполнения, записываются на диск, в то время как другие (s) представляют состояние в памяти. Таким образом, чтобы получить фактическое состояние для каждого интервала необходимо статистические показатели, Группировка по **plan_id**, **execution_type** и **runtime_stats_interval_id**. |  
|**plan_id**|**bigint**|Внешний ключ. Присоединяет к [sys.query_store_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Внешний ключ. Присоединяет к [sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Определяет тип выполнения запроса.<br /><br /> 0 — регулярного выполнения (успешно завершено)<br /><br /> 3 — инициируется клиентом прервал выполнение<br /><br /> 4 - выполнение прервано исключение|  
|**execution_type_desc**|**nvarchar(128)**|Текстовое описание выполнения тип поля:<br /><br /> 0 — обычный<br /><br /> 3 — прервана<br /><br /> 4 - исключение|  
|**first_execution_time**|**datetimeoffset**|Первого выполнения для плана запроса в течение интервала статистической обработки.|  
|**last_execution_time**|**datetimeoffset**|Время последнего выполнения запроса план в течение интервала статистической обработки.|  
|**count_executions**|**bigint**|Общее число выполнений плана запроса в течение интервала статистической обработки.|  
|**avg_duration**|**float**|Средняя продолжительность для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**last_duration**|**bigint**|Длительность последнего запроса планирования в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**min_duration**|**bigint**|Минимальная длительность для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**max_duration**|**bigint**|Максимальная длительность для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**stdev_duration**|**float**|Длительность среднеквадратичное отклонение для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**avg_cpu_time**|**float**|Среднее время ЦП для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**last_cpu_time**|**bigint**|Последнее время ЦП для запроса планирования в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**min_cpu_time**|**bigint**|Минимальное время ЦП для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**max_cpu_time**|**bigint**|Максимальное время ЦП для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**stdev_cpu_time**|**float**|Среднеквадратичное отклонение времени ЦП для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**avg_logical_io_reads**|**float**|Среднее число логических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки. (в виде число считываемых страниц размером 8 КБ).|  
|**last_logical_io_reads**|**bigint**|Последнее число логических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки. (в виде число считываемых страниц размером 8 КБ).|  
|**min_logical_io_reads**|**bigint**|Минимальное число логических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки. (в виде число считываемых страниц размером 8 КБ).|  
|**max_logical_io_reads**|**bigint**|Максимальное число логических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки. (в виде число считываемых страниц размером 8 КБ). |  
|**stdev_logical_io_reads**|**float**|Число логических операций ввода-ВЫВОДА считывает стандартное отклонение для плана запроса в течение интервала статистической обработки. (в виде число считываемых страниц размером 8 КБ).|  
|**avg_logical_io_writes**|**float**|Среднее число логических операций ввода-ВЫВОДА создает план запроса в течение интервала статистической обработки.|  
|**last_logical_io_writes**|**bigint**|Последнее число логических операций ввода-ВЫВОДА создает план запроса в течение интервала статистической обработки.|  
|**min_logical_io_writes**|**bigint**|Минимальное число логических операций ввода-ВЫВОДА создает план запроса в течение интервала статистической обработки.|  
|**max_logical_io_writes**|**bigint**|Максимальное число логических операций ввода-ВЫВОДА создает план запроса в течение интервала статистической обработки.|  
|**stdev_logical_io_writes**|**float**|Число логических операций ввода-ВЫВОДА записывает стандартное отклонение для плана запроса в течение интервала статистической обработки.|  
|**avg_physical_io_reads**|**float**|Среднее число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выражается как число считываемых страниц размером 8 КБ).|  
|**last_physical_io_reads**|**bigint**|Последнее число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выражается как число считываемых страниц размером 8 КБ).|  
|**min_physical_io_reads**|**bigint**|Минимальное число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выражается как число считываемых страниц размером 8 КБ).|  
|**max_physical_io_reads**|**bigint**|Максимальное число физических операций ввода-ВЫВОДА считывает для плана запроса в течение интервала статистической обработки (выражается как число считываемых страниц размером 8 КБ).|  
|**stdev_physical_io_reads**|**float**|Количество физических операций ввода-ВЫВОДА чтения стандартное отклонение для плана запроса в течение интервала статистической обработки (выражается как число считываемых страниц размером 8 КБ).|  
|**avg_clr_time**|**float**|Среднее время CLR для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**last_clr_time**|**bigint**|Время последнего CLR для запроса планирования в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**min_clr_time**|**bigint**|Минимальное время CLR для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**max_clr_time**|**bigint**|Максимальное время CLR для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**stdev_clr_time**|**float**|Среднеквадратичное отклонение времени со средой CLR для плана запроса в течение интервала статистической обработки (предупреждение в микросекундах).|  
|**avg_dop**|**float**|Среднее значение DOP (степень параллелизма) для плана запроса в течение интервала статистической обработки.|  
|**last_dop**|**bigint**|Последние DOP (степень параллелизма) для плана запроса в течение интервала статистической обработки.|  
|**min_dop**|**bigint**|Минимальное значение DOP (степень параллелизма) для плана запроса в течение интервала статистической обработки.|  
|**MAX_DOP**|**bigint**|Максимальное DOP (степень параллелизма) для плана запроса в течение интервала статистической обработки.|  
|**stdev_dop**|**float**|Среднеквадратичное отклонение DOP (степень параллелизма) для плана запроса в течение интервала статистической обработки.|  
|**avg_query_max_used_memory**|**float**|Среднее предоставления памяти (отмечено как число страниц размером 8 КБ) для плана запроса в течение интервала статистической обработки. Всегда 0 для запросов, использующих в собственном коде процедур, скомпилированных в оптимизированных для памяти.|  
|**last_query_max_used_memory**|**bigint**|Последний предоставления памяти (отмечено как число страниц размером 8 КБ) для плана запроса в течение интервала статистической обработки. Всегда 0 для запросов, использующих в собственном коде процедур, скомпилированных в оптимизированных для памяти.|  
|**min_query_max_used_memory**|**bigint**|Минимальный объем памяти (отмечено как число страниц размером 8 КБ) для плана запроса в течение интервала статистической обработки. Всегда 0 для запросов, использующих в собственном коде процедур, скомпилированных в оптимизированных для памяти.|  
|**max_query_max_used_memory**|**bigint**|Максимальный объем предоставляемой памяти (отмечено как число страниц размером 8 КБ) для плана запроса в течение интервала статистической обработки. Всегда 0 для запросов, использующих в собственном коде процедур, скомпилированных в оптимизированных для памяти.|  
|**stdev_query_max_used_memory**|**float**|Стандартное отклонение (отмечено как число страниц размером 8 КБ) на выделение памяти для плана запроса в течение интервала статистической обработки. Всегда 0 для запросов, использующих в собственном коде процедур, скомпилированных в оптимизированных для памяти.|  
|**avg_rowcount**|**float**|Среднее число возвращенных строк для плана запроса в течение интервала статистической обработки.|  
|**last_rowcount**|**bigint**|Число возвращенных строк с последнего выполнения плана запроса в течение интервала статистической обработки.|  
|**min_rowcount**|**bigint**|Минимальное количество возвращенных строк для запроса планирования в течение интервала статистической обработки.|  
|**max_rowcount**|**bigint**|Максимальное число возвращенных строк для запроса планирования в течение интервала статистической обработки.|  
|**stdev_rowcount**|**float**|Число строк, возвращаемых стандартное отклонение для плана запроса в течение интервала статистической обработки.|
|**avg_log_bytes_used**|**float**|Среднее число байтов в журнале базы данных, используемые планом запроса в течение интервала статистической обработки. Применяет **только к базе данных Azure SQL**.|    
|**last_log_bytes_used**|**bigint**|Число байтов в журнале базы данных, используемых для последнего выполнения плана запроса в течение интервала статистической обработки. Применяет **только к базе данных Azure SQL**.|  
|**min_log_bytes_used**|**bigint**|Минимальное число байтов в журнале базы данных, используемые планом запроса в течение интервала статистической обработки.  Применяет **только к базе данных Azure SQL**.|  
|**max_log_bytes_used**|**bigint**|Максимальное число байтов в журнале базы данных, используемые планом запроса в течение интервала статистической обработки.  Применяет **только к базе данных Azure SQL**.| 
|**stdev_log_bytes_used**|**float**|Стандартное отклонение число байтов в журнале базы данных, используемый план запроса в течение интервала статистической обработки.  Применяет **только к базе данных Azure SQL**.|
  
## <a name="permissions"></a>Permissions  
 Требуется **VIEW DATABASE STATE** разрешение.  
  
## <a name="see-also"></a>См. также:  
 [sys.database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Мониторинг производительности с использованием хранилища запросов](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Хранимые процедуры &#40; в хранилище запросов Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  