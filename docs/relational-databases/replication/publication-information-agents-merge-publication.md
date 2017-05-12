---
title: "Сведения о публикации, вкладка &quot;Агенты&quot; (публикация слиянием) | Документация Майкрософт"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.merge.f1
ms.assetid: 73ff590a-20da-4f10-b592-c60b7226d22b
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 661a6f73257e23f44dc303349dce5de80fcd352d
ms.lasthandoff: 04/11/2017

---
# <a name="publication-information-agents-merge-publication"></a>Сведения о публикации, агенты (публикация слиянием)
  Вкладка **Агенты** отображает общие сведения об агенте моментальных снимков для выбранной публикации.  
  
## <a name="options"></a>Параметры  
 Для получения более подробных сведений и задач, относящихся к агенту моментальных снимков, щелкните правой кнопкой мыши строку этого агента и выберите параметр в контекстном меню. Чтобы изменить способ отображения данных в сетке, щелкните правой кнопкой мыши сетку, а затем один из следующих параметров.  
  
-   **Сортировать**: сортировка по одному или нескольким столбцам в диалоговом окне **Сортировка столбцов** .  
  
-   **Выберите столбцы для отображения**: выбор столбцов для отображения и порядка их отображения в диалоговом окне **Выбор столбцов** .  
  
-   **Фильтр**: фильтрация строк в сетке на основании значений столбцов в диалоговом окне **Параметры фильтра** .  
  
-   **Очистить фильтр**: удаление всех параметров фильтра для сетки.  
  
 Настройки фильтра уникальны для каждой сетки. Выбор и сортировка столбцов применяются ко всем сеткам одного типа, как, например, сетка публикаций для каждого издателя.  
  
 **Состояние**  
 Состояние агента моментальных снимков. Возможные значения состояния показаны в следующем списке:  
  
-   Ошибка  
  
-   Попытка повторно выполнить неудачно завершившиеся команды  
  
-   Не выполняется  
  
-   Завершен  
  
 **Агент**  
 Агент моментальных снимков. Это единственный агент, связанный с публикацией слиянием. Агент слияния связан с подписками на эту публикацию. Дополнительные сведения см. в статье [Просмотр сведений и выполнение задач для агентов, связанных с подпиской (монитор репликации)](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 **Время последнего запуска**  
 Время последнего запуска агента.  
  
 **Длительность**  
 Продолжительность выполнения агента. Этот параметр представляет собой время, прошедшее с момента начала сеанса, если агент запущен в данный момент, или общее время, если агент был запущен ранее.  
  
 **Последнее действие**  
 Последнее действие выполнено во время самого последнего выполнения агента.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для публикации (монитор репликации)](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для агентов, связанных с публикацией (монитор репликации)](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  