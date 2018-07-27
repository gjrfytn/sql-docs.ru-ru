---
title: Просмотр сведений и выполнение задач для агентов, связанных с публикацией (монитор репликации) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f385a167fe56db1c9db2a2238b22de66daa3ab6a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37281000"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-publication-replication-monitor"></a>Просмотр сведений и выполнение задач для агентов, связанных с публикацией (монитор репликации)
  Монитор репликации содержит вкладку **Агенты** , на которой приведены сведения об агентах, связанных с выбранной публикацией. Агент распределения и агент слияния ассоциированы с подписками. Дополнительные сведения о них вы найдете в статье [Просмотр сведений и выполнение задач для агентов, связанных с подпиской (монитор репликации)](view-information-and-perform-tasks-for-subscription-agents.md).  
  
 На этой вкладке отображаются сведения о следующих агентах:  
  
-   Агент моментальных снимков, используемый всеми публикациями.  
  
-   Агент чтения журналов, используемый всеми публикациями транзакций.  
  
-   Агент чтения очереди, используемый публикациями транзакций, активированными для подписок, обновляемых посредством очередей.  
  
 Чтобы просмотреть дополнительные сведения о параметрах, доступных на этой вкладке, выберите пункт **Справка** в главном меню. Сведения о запуске монитора репликации см. в [этой статье](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>Просмотр сведений и выполнение задач для агентов, связанных с публикацией  
  
1.  Раскройте на левой панели группу издателей, раскройте издатель и выберите нужную публикацию.  
  
2.  Перейдите на вкладку **Агенты** для просмотра сведений об агентах. На этой вкладке можно также просмотреть другие подробные сведения и выполнить дополнительные задачи.  
  
    -   Чтобы просмотреть подробные сведения об агенте (например, информационные сообщения и возможные сообщения об ошибках), щелкните правой кнопкой мыши агент, а затем щелкните **Просмотреть сведения**.  
  
    -   Чтобы просмотреть подробные сведения о задании, запустившем агента (например, расписание, описание шагов задания и т. п.), щелкните правой кнопкой мыши агент, а затем щелкните **Свойства**.  
  
    -   Чтобы управлять профилями агентов, щелкните правой кнопкой мыши агент, затем выберите **Профиль агента**. Дополнительные сведения см. в статье [Работа с профилями агента репликации](../agents/replication-agent-profiles.md).  
  
    -   Чтобы запустить агент, который еще не запущен, щелкните правой кнопкой мыши этот агент, а затем щелкните **Запустить агент**.  
  
    -   Чтобы остановить агент, который запущен, щелкните правой кнопкой мыши этот агент, а затем щелкните **Остановить агент**.  
  
## <a name="see-also"></a>См. также  
 [Настройка пороговых значений и предупреждений в мониторе репликации](set-thresholds-and-warnings-in-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для публикации (монитор репликации)](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Администрирование агента репликации](../agents/replication-agent-administration.md)   
 [Наблюдение за репликацией](../monitoring-replication.md)  
  
  