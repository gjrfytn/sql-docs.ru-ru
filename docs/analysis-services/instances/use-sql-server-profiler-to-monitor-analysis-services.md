---
title: "Использование приложения SQL Server Profiler для мониторинга служб Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Profiler, службы Analysis Services"
  - "мониторинг служб Analysis Services [SQL Server]"
  - "производительность [Analysis Services], SQL Server Profiler"
  - "Profiler [SQL Server Profiler], службы Analysis Services"
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# Использование приложения SQL Server Profiler для мониторинга служб Analysis Services
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отслеживает события обработки ядра, например начало пакета или транзакции, и фиксирует данные об этих событиях, тем самым давая возможность осуществлять мониторинг операций серверов и баз данных (например, пользовательские операции запросов и входа в систему). Можно фиксировать данные приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или файл для дальнейшего анализа, а также можно воспроизводить зафиксированные события в том же или в другом экземпляре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , чтобы точно определить, что произошло. Можно воспроизводить события в режиме реального времени или в пошаговом режиме. Также очень полезно запускать события трассировки вместе со счетчиками приложения «Производительность» на одном и том же компьютере. Приложение SQL Profiler может определять корреляцию между ними на основе времени и отображать их совместно на одной временной шкале. События трассировки предоставят подробные сведения, в то время как счетчики приложения «Производительность» дадут общее представление. Дополнительные сведения о создании и запуске трассировок см. в разделе [Создание трассировки приложения Profiler для воспроизведения (службы Analysis Services)](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
 В следующей таблице описаны подразделы, содержащиеся в этом разделе.  
  
## В этом разделе  
  
|Раздел|Description|  
|-----------|-----------------|  
|[Введение в мониторинг служб Analysis Services при помощи приложения SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Содержит описание использования приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] для мониторинга экземпляра служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Создание трассировки приложения Profiler для воспроизведения (службы Analysis Services)](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)|Содержит требования к созданию трассировки для воспроизведения с помощью приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[События трассировки служб Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)|Содержит описание классов событий служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Эти классы событий соответствуют действиям, формируемым службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , и используются для воспроизведения трассировок.|  
  
## См. также  
 [Наблюдение за экземпляром служб Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  