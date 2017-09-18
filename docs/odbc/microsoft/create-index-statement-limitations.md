---
title: "Создание ограничений инструкции ИНДЕКСА | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 874aba454df680626a126f19faa821f885e9d040
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-statement-limitations"></a>Создание ограничений оператора ИНДЕКСА
Инструкции CREATE INDEX не поддерживается для драйверов Microsoft Excel или текст.  
  
 Индекс можно определить в более 10 столбцов. Если более чем 10 столбцов включаются в инструкции CREATE INDEX, не будут распознаны индекса и таблицы будут рассматриваться, как если бы, если индекс не были созданы.  
  
 Драйвер dBASE невозможно создать индекс для ЛОГИЧЕСКОГО столбца.  
  
 При использовании драйвера dBASE путем построения многомерных выражений (или .ndx) индекс на столбце (поле), указанных в предложениях WHERE инструкции SELECT можно улучшить время ответа на больших файлов. Существующие индексы многомерных выражений применяются автоматически для =, >, \<, > =, = <, а также МЕЖДУ операторами в предложении WHERE и предикатах LIKE, а также в предикатах соединения.  
  
 При использовании драйвера dBASE индекса, созданного с помощью инструкции CREATE UNIQUE INDEX фактически не являются уникальными и повторяющиеся значения могут быть вставлены в индексированный столбец. Только одна запись из набора с одинаковыми значениями ключа можно добавить в индекс.  
  
 При использовании драйвера Paradox после смежных подмножества столбцов в таблице, включая первый столбец должен быть определен уникальный индекс. Если не определен уникальный индекс для таблицы или при использовании драйвера Paradox без реализации компонента Borland Database Engine таблицу невозможно обновить драйвером Paradox.