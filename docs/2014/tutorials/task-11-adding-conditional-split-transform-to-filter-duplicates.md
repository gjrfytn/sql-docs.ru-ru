---
title: 'Задача 11: Добавление условного разбиения преобразования для фильтрации повторений | Документация Майкрософт'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae4b77e5788ac21e6962ad7f4a6679982363cd67
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185661"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Задача 11. Добавление преобразования «Условное разбиение» для фильтрации повторений
  В этой задаче в поток данных добавляется преобразование «Условное разбиение». Это преобразование позволяет фильтровать повторения из входящего набора записей. Преобразование «Нечеткое группирование» группирует записи, которые оно распознает как совпадающие, и выбирает одну из записей в качестве сводной записи. Все записи в группе имеют одинаковое значение _key_out. Сводная запись имеет то же значение _key_in, что и значение _key_out. Другие записи в группе имеют различные значения _key_in и _key_out. Поэтому при фильтрации с помощью условия _key_in==_key_out будет получена только сводная строка в группе.  
  
1.  Перетащите **Условное разбиение** преобразования из **распространенных** статьи **область элементов служб SSIS** для **потока данных** вкладки.  
  
2.  Щелкните правой кнопкой мыши **преобразование «Условное разбиение»** в **потока данных** , а щелкните **Переименовать**. Тип **фильтровать повторения** и нажмите клавишу **ввод**.  
  
3.  Подключение **группировать поставщиков с совпадающими идентификаторами** для **фильтровать повторения**.  
  
4.  Дважды щелкните **фильтровать повторения** для запуска **редактор преобразований условного разбиения** диалоговое окно.  
  
5.  Разверните **столбцы** в верхней левой панели.  
  
6.  Перетащите **_key_in** для **условие** столбца.  
  
7.  Тип == (равно) рядом с полем **_key_in** и перетащите **_key_out**.  
  
8.  Нажмите кнопку **вариант 1** в **имя выходного** столбец, тип **уникальных записей**и нажмите клавишу **ввод**.  
  
     ![Conditional Split Transformation Editor](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Conditional Split Transformation Editor")  
  
9. Нажмите кнопку **ОК** закрыть **Conditional Split Transformation Editor** диалоговое окно.  
  
## <a name="next-step"></a>Следующий шаг  
 [Задача 12. Добавление преобразования "Производный столбец" для добавления столбцов, необходимых MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  