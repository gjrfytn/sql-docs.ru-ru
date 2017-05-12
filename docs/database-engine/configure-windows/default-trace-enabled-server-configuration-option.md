---
title: "Параметр конфигурации сервера &#171;default trace enabled&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "журналы [SQL Server], трассировки"
  - "трассировки [SQL Server], журналы"
  - "default trace enabled, параметр"
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Параметр конфигурации сервера &#171;default trace enabled&#187;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Используйте параметр **default trace enabled** , чтобы включить или отключить файлы журнала трассировки по умолчанию. Функциональные возможности трассировки по умолчанию обеспечивают насыщенный, стабильный журнал активности и изменений, в основном связанных с параметрами конфигурации.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Вместо этого используйте расширенные события.  
  
## Назначение  
 Трассировка по умолчанию обеспечивает помощь в поиске неисправностей администраторам базы данных, гарантируя, что они имеют необходимые регистрационные данные для диагностики проблем сразу же, как только они происходят.  
  
## просмотр  
 Журналы трассировки по умолчанию можно открыть и исследовать в приложении [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , либо к ним можно применить запросы на языке [!INCLUDE[tsql](../../includes/tsql-md.md)] с помощью системной функции `fn_trace_gettable` . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] позволяет открывать файлы используемых по умолчанию журналов трассировки таким же образом, как и обычные выходные файлы трассировки. Файл журнала трассировки по умолчанию хранится по умолчанию в каталоге `\MSSQL\LOG` , используя файл продолжения трассировки. Базовое имя файла для файла журнала трассировки по умолчанию — `log.trc`. Как правило, в установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]трассировка по умолчанию разрешена, поэтому TraceID будет равно 1. Если разрешение будет дано после установки и создания других трассировок, то числовое обозначение TraceID может стать больше.  
  
 Дополнительные сведения об использовании приложения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler для просмотра этого файла трассировки см. в разделе [Открыть файл трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md).  
  
### Пример  
 Следующая инструкция открывает журнал трассировки по умолчанию в расположении по умолчанию:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## Настройка  
 Установка параметра **default trace enabled** в значение 1 включает **трассировку по умолчанию**. Настройка по умолчанию для этого параметра — 1 (включено). Значение 0 выключает трассировку.  
  
 Параметр **default trace enabled** является дополнительным параметром. Если для изменения этого параметра используется системная хранимая процедура **sp_configure**, то возможность изменить значение параметра **default trace enabled** разрешена только в том случае, если параметр **show advanced options** имеет значение 1. Параметр вступает в силу сразу без перезапуска сервера.  
  
## См. также:  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  