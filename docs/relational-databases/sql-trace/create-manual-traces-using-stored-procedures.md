---
title: "Создание трассировок вручную с помощью хранимых процедур | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ee7ef604dc518fb4765ca5bd944c7fe01500035
ms.lasthandoff: 04/11/2017

---
# <a name="create-manual-traces-using-stored-procedures"></a>Создание трассировок вручную с помощью хранимых процедур
  Для создания трассировок на экземпляре компонента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Microsoft [!INCLUDE[tsql](../../includes/tsql-md.md)] предоставляет системные хранимые процедуры на языке [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Эти системные хранимые процедуры можно использовать для создания трассировок вручную в рамках пользовательских приложений вместо использования приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Это позволяет писать пользовательские приложения, отвечающие конкретным нуждам предприятия.  
  
## <a name="in-this-section"></a>В этом разделе  
 В приведенной ниже таблице представлены системные хранимые процедуры, используемые для трассировки экземпляра компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Хранимая процедура|Выполненная задача|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|Возвращает сведения о событии, включенном в трассировку.|  
|[sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|Возвращает сведения об указанной трассировке или всех существующих трассировках.|  
|[Хранимая процедура sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|Создает определение трассировки. Новая трассировка будет находиться в остановленном состоянии.|  
|[Хранимая процедура sp_trace_generateevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|Создает пользовательское событие.|  
|[Хранимая процедура sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|Добавляет класс событий или столбец данных к трассировке либо удаляет их из трассировки.|  
|[Хранимая процедура sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|Запускает, останавливает или закрывает трассировку.|  
|[sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|Возвращает сведения о фильтрах, примененных к трассировке.|  
|[sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|Применяет новый или измененный фильтр к трассировке.|  
  
 **Определение пользовательской трассировки при помощи хранимых процедур**  
  
1.  Укажите событие, которое необходимо зарегистрировать с помощью процедуры **sp_trace_setevent**.  
  
2.  Укажите фильтры события. Дополнительные сведения см. в разделе [Создание фильтра трассировки (Transact-SQL)](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md).  
  
3.  Укажите назначение для данных зарегистрированного события с помощью процедуры **sp_trace_create**.  
  
 Пример использования хранимых процедур трассировки см. в разделе [Создание трассировки (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **Установка определения трассировки по умолчанию**  
  
 [Приложение SQL Server Profiler](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **Установка параметров по умолчанию для отображения трассировки**  
  
 [Приложение SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Создание трассировки**  
  
 [Приложение SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **Добавление или удаление события из шаблона трассировки**  
  
 [Приложение SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  