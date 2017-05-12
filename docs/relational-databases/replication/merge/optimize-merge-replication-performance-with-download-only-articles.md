---
title: "Оптимизация производительности репликации слиянием при работе со статьями, доступными только для скачивания | Документация Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b82a117316022f7c30920d9174855522d374f1b
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>Оптимизация производительности репликации слиянием при работе со статьями, доступными только для загрузки
  Репликация слиянием предлагает два разных типа статей, которые удовлетворяют требованиям приложений. Публикации могут содержать одну или несколько статей каждого из этих типов в соответствии с требованиями приложения:  
  
-   Стандартные статьи  
  
-   статьи только для загрузки  
  
 Статьи, доступные только для загрузки, имеют преимущества в производительности перед стандартными статьями и должны применяться везде, где они уместны.  
  
> [!NOTE]  
>  Для использования статей, доступных только для загрузки, уровень совместимости публикации должен быть не менее 90RTM.  
  
## <a name="standard-articles"></a>Стандартные статьи  
 Стандартные статьи используются по умолчанию и предлагают полный диапазон возможностей репликации слиянием, включая широкий выбор средств обнаружения и разрешения конфликтов. Стандартные статьи подходят для таблиц, обновляемых несколькими подписчиками. Объекты, отличные от таблиц, такие как хранимые процедуры и представления, всегда публикуются в виде стандартных статей.  
  
## <a name="download-only-articles"></a>статьи только для загрузки  
 Статьи, доступные только для загрузки, предназначены для приложений, содержащих данные, которые не обновляются на подписчиках, например наборы статей в каталогах продуктов. Каталог продуктов обычно обновляется на издателе, а не на подписчиках. Учитывая то, что статьи только для загрузки не могут обновляться у подписчика, отслеживаемые метаданные подписчикам не отправляются. Это может привести к уменьшению объема хранилища на подписчиках и увеличению производительности, особенно в условиях медленного сетевого соединения.  
  
 Статьи, доступные только для загрузки, работают совместно с клиентскими подписками: если статья предназначена только для загрузки, строки для этой статьи не могут вставляться, обновляться и удаляться на подписчиках, использующих клиентские подписки. Издатели и подписчики, использующие серверные подписки (обычно это подписчики, которые переиздают данные для других подписчиков), могут вставлять, обновлять и удалять данные. Дополнительные сведения о клиентских подписках см. в статье [Подписка на публикации](../../../relational-databases/replication/subscribe-to-publications.md).  
  
 Чтобы указать, что статья предназначена только для загрузки, см. раздел [Specify That a Merge Table Article is Download-Only](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md).  
  
## <a name="using-different-article-types-in-your-applications"></a>Использование в приложениях статей иных типов  
 Изучив требования своего приложения, можно найти компромиссный вариант между максимальной гибкостью и оптимальной производительностью. Например, приложения с многочисленными конфликтами и изменениями как на издателе, так и на подписчике будут использовать публикацию, составленную из стандартных статей. Некоторые приложения, например приложение по автоматизации управления продажами, могут иметь статьи с высокой вероятностью конфликтов и другие статьи, использующиеся в качестве поисковых таблиц, которые могут определяться как статьи, доступные только для загрузки. Приложения ввода данных, такие как системы точки продажи и приложения автоматизации выездного обслуживания, часто строго секционируют данные, чтобы полностью исключить конфликты, при этом данные от одного подписчика никогда не передаются другому подписчику. В этих ситуациях сочетание неперекрывающихся секций, статей, доступных только для загрузки, и предварительно вычисляемых секций обеспечивает максимальную производительность и масштабируемость. Дополнительные сведения о неперекрывающихся секциях и предварительно вычисляемых секциях см. в разделе [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>См. также:  
 [Параметры статьи для репликации слиянием](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Оптимизация производительности репликации слиянием с помощью отслеживания условного удаления](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  