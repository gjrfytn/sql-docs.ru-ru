---
title: "Категория событий &#171;Отчеты о состоянии&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "события состояния [службы Analysis Services]"
  - "категория событий «Отчеты о состоянии»"
  - "классы событий [службы Analysis Services], отчеты о состоянии"
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 23
---
# Категория событий &#171;Отчеты о состоянии&#187;
  Категория событий «Отчеты о состоянии» содержит классы событий, описанные в следующей таблице.  
  
|Класс событий|Идентификатор события|Description|  
|-----------------|--------------|-----------------|  
|Начало отчета о состоянии|5|Позволяет собрать все события начала отчета о состоянии с момента запуска трассировки.|  
|Окончание отчета о состоянии|6|Собирает все события окончания отчета о состоянии с момента запуска трассировки.|  
|Текущий отчет о состоянии|7|Собирает все текущие события отчета о состоянии с момента запуска трассировки. Например, во время обработки текущие отчеты включают в себя данные, относящиеся к обрабатываемым объектам (измерения, секции, куб и т. д.).|  
|Ошибка отчета о состоянии|8|Собирает все события ошибки отчета о состоянии с момента запуска трассировки.|  
  
 Каждое событие начала отчета о состоянии начинается с потока событий состояния и завершается событием конца отчета о состоянии. В потоке может содержаться любое количество событий ошибки отчета о состоянии и текущих событий отчета о состоянии.  
  
 Дополнительные сведения о столбцах, связанных с каждым из классов событий «Отчеты о состоянии», см. в разделе [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## См. также  
 [События трассировки служб Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  