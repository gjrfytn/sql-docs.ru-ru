---
title: Хэш-индексы | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2c2b4c055eea6aef2e7825ee6589c6611ceaf7a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295234"
---
# <a name="hash-indexes"></a>Хэш-индексы.
  Индексы используются в качестве точек входа для таблиц, оптимизированных для памяти. Для считывания строк из таблицы требуется индекс, который определяет местоположение данных в памяти.  
  
 Хэш-индекс состоит из коллекции контейнеров, организованных в массив. Хэш-функция сопоставляет ключи индекса с соответствующими контейнерами в хэш-индексе. На следующем рисунке показаны три ключа индекса, сопоставленные с тремя различными контейнерами в хэш-индексе. Для наглядности хэш-функция называется f(x).  
  
 ![Ключи индекса, сопоставленные с различными контейнерами. ] (../../2014/database-engine/media/hekaton-tables-2.gif "Ключи индекса, сопоставленные с различными контейнерами.")  
  
 Функция, используемая для хэширования индексов, имеет следующие характеристики.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] имеет одну хэш-функцию, используемую для всех хэш-индексов.  
  
-   Хэш-функция является детерминированной. Один ключ индекса всегда связан с одним контейнером в хэш-индексе.  
  
-   Несколько ключей индекса могут быть сопоставлены с одним и тем же хэш-контейнером индекса.  
  
-   Хэш-функция сбалансирована, а это означает, что распределение значений ключей индекса, связанных с хэш-контейнерами, соответствует распределению Пуассона.  
  
     Распределение Пуассона не является равномерным. Значения ключа индекса не распределяются в хэш-контейнерах равномерно. Например, распределение Пуассона разных ключей индекса *n* по хэш-контейнерам *n* приводит к созданию примерно трети пустых контейнеров, трети контейнеров, содержащих один ключ индекса, и трети, содержащей по два ключа индекса. Небольшое число контейнеров всегда будет содержать более двух ключей.  
  
 Если два ключа индекса сопоставляются с одним хэш-контейнером, происходит конфликт хэша. Большое число конфликтов хэша может оказывать негативное влияние на операции чтения.  
  
 Структура хэш-индекса в памяти состоит из массива указателей памяти. Каждый контейнер связан с определенным смещением в этом массиве. Каждый контейнер в массиве указывает на первую строку в этом хэш-контейнере. Каждая строка в контейнере указывает на следующую строку, образуя таким образом цепочку строк для каждого хэш-контейнера, как показано на рисунке ниже.  
  
 ![Структура индекса в памяти. ] (../../2014/database-engine/media/hekaton-tables-3.gif "Структуры индекса в памяти.")  
  
 На рисунке изображены три контейнера со строками. Второй контейнер сверху содержит три красные строки. Четвертый контейнер — одну голубую строку. Нижний контейнер содержит две зеленые строки. Это могут быть разные версии одной строки.  
  
 Дополнительные сведения об индексах оптимизированных для памяти таблиц см. в разделе [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>См. также  
 [Индексы для оптимизированных для памяти таблиц](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  