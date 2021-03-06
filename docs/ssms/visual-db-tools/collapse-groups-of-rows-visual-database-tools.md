---
title: Сворачивание групп строк (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a40eefb6b60b21387c90b84e7bffdc423b7d798
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503952"
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>Сворачивание групп строк (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Может быть создан результат запроса, в котором каждая результирующая строка соответствует всей группе строк исходных данных. При сворачивании строк следует помнить о следующих моментах.  
  
-   **Можно устранить дублирование строк** Некоторые запросы могут создавать результирующие наборы, в которых есть несколько одинаковых строк. Например, может быть создан результирующий набор, в котором каждая строка содержит название страны и города, где проживает автор; но, если в одном городе проживает несколько авторов, будет несколько одинаковых строк. Конечный код SQL может выглядеть следующим образом:  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
    Результирующий набор, формируемый предыдущим запросом, не очень удобен. Если в городе проживает четыре автора, результирующий набор будет включать в себя четыре одинаковые строки. Так как результирующий набор не включает никаких других столбцов, кроме столбцов города и страны, отличить одну строку от другой нельзя. Одним из способов избежать повторяющихся строк является включение дополнительных столбцов, которые позволят различать строки. Например, если включить имя автора, каждая строка будет отличаться от всех остальных (при условии, что в городе не проживают два автора-однофамильца). Конечный код SQL может выглядеть следующим образом:  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
    ```  
  
    Хотя предыдущий запрос позволяет обойти затруднение, в действительности он не решает проблему. Это значит, что в результирующем наборе нет дублированных строк, но теперь это уже не результирующий набор, относящийся к городам. Чтобы избежать повторов в исходном результирующем наборе и в то же время иметь строки, описывающие только город, можно создать запрос, возвращающий только различающиеся строки. Конечный код SQL может выглядеть следующим образом:  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
    ```  
  
    Подробности об устранении повторов см. в разделе [Исключение повторяющихся строк (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md).  
  
-   **Можно производить вычисления на группах строк** Это означает, что можно обобщать информацию в группах строк. Например, может быть создан результирующий набор, в котором каждая строка содержит название страны и города, в котором проживает один из авторов, плюс количество авторов, проживающих в этом городе. Конечный код SQL может выглядеть следующим образом:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ```  
  
    Подробности о вычислении на группах строк см. в разделах [Резюмирование результатов запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md) и [Результаты запросов сортировки и группирования (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md).  
  
-   **Можно использовать критерии выбора для включения в группы строк** Например, может быть создан результирующий набор, в котором каждая строка содержит название страны и города, в котором проживают несколько авторов, плюс количество авторов, проживающих в этом городе. Конечный код SQL может выглядеть следующим образом:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
    ```  
  
    Сведения о применении критериев выбора на группах строк см. в разделах [Задание условий для групп (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-conditions-for-groups-visual-database-tools.md) и [Использование предложения HAVING и WHERE в одном запросе (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
## <a name="see-also"></a>См. также:  
[Определение критериев поиска (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Разделы по конструированию запросов и представлений (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
