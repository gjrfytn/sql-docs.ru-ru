---
title: "Подробнее о репликации слиянием — обнаружение и разрешение конфликтов | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be8f8a4e1df903cc70191dc582ce2aef19e7e7aa
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>Подробнее о репликации слиянием — обнаружение и разрешение конфликтов
  Когда издатель и подписчик соединяются и происходит синхронизация, агент слияния проверяет наличие конфликтов. При обнаружении конфликтов сопоставитель слияния использует арбитр конфликтов (указанный при добавлении статьи в публикацию), чтобы определить, какие данные являются приемлемыми и распространяются на другие сайты.  
  
> [!NOTE]  
>  Хотя подписчик синхронизируется с издателем, конфликты обычно возникают между обновлениями, осуществляемыми на различных подписчиках, а не между обновлениями, осуществляемыми на подписчике и издателе.  
  
 Логика обнаружения и разрешения конфликтов зависит от следующих параметров, описание которых приводится в данном разделе:  
  
-   указано ли отслеживание на уровне столбцов, строк или логических записей;  
  
-   указан ли механизм разрешения конфликтов на основе приоритетов (по умолчанию) или указан сопоставитель статей. Сопоставитель статей может быть:  
  
    -   *обработчиком бизнес-логики* , разработанным в управляемом коде;  
  
    -   *пользовательским сопоставителем конфликтов*на основе COM;  
  
    -   Основанный на технологии COM сопоставитель, поддерживаемый [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
     При использовании механизма разрешения конфликтов по умолчанию логика работы определяется используемым типом подписки: клиентской или серверной.  
  
## <a name="conflict-detection"></a>Обнаружение конфликтов  
 Квалифицируется ли изменение данных как конфликт или зависит от типа отслеживания конфликтов, установленного для статьи:  
  
-   Если выбрано отслеживание конфликтов на уровне столбцов, то изменение данных считается конфликтом, если оно сделано в одном и том же столбце в одной и той же строке в нескольких узлах репликации.  
  
-   Если выбрано отслеживание на уровне строк, то изменение данных считается конфликтом, если оно выполнено для каких-либо столбцов в одной и той же строке в нескольких узлах репликации (изменяемые столбцы в соответствующих строках могут быть разными).  
  
-   Если выбрано отслеживание на уровне логических записей, то изменение данных считается конфликтом, если оно выполнено в какой-либо строке в одной и той же логической записи в нескольких узлах репликации (изменяемые столбцы в соответствующих строках могут быть разными).  
  
 Дополнительные сведения см. в статье [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 Чтобы указать уровень отслеживания конфликтов и разрешений, см. раздел [Specify the Conflict Tracking and Resolution Level for Merge Articles](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md).  
  
## <a name="conflict-resolution"></a>Устранение конфликтов  
 После обнаружения конфликта агент слияния запускает выбранный сопоставитель конфликтов и использует его для определения победителя в конфликте. Победившая строка применяется на издателе и подписчике, а данные из проигравшей строки записываются в таблицу конфликтов. Разрешение конфликтов осуществляется немедленно после выполнения сопоставления конфликтов, если не выбран интерактивный режим разрешения конфликтов.  
  
### <a name="resolver-types"></a>Типы сопоставителя конфликтов  
 В репликации слиянием устранение конфликтов осуществляется на уровне статей. Для публикаций, состоящих из нескольких статей, можно использовать разные сопоставители конфликтов для разных статей или один и тот же сопоставитель конфликтов, обслуживающий одну статью, несколько статей или все статьи публикации.  
  
 Если планируется использование сопоставителя конфликтов на основе приоритетов (по умолчанию), то не нужно устанавливать свойство сопоставителя для статьи. Если вместо сопоставителя конфликтов по умолчанию нужно использовать сопоставитель статей, следует установить свойство сопоставителя для статьи, которая будет использовать его, выбирая доступный сопоставитель конфликтов на издателе. Любую конкретную информацию, которую необходимо передать сопоставителю конфликтов, также можно указать в информационном свойстве сопоставителя.  
  
 Для репликации слиянием предлагается четыре типа сопоставителя конфликтов:  
  
-   Сопоставитель конфликтов на основе приоритетов (по умолчанию)  
  
     Механизм разрешения конфликтов по умолчанию функционирует по-разному в зависимости от того, является подписка клиентской или серверной. Можно назначать приоритеты различным подписчикам, использующим серверные подписки; изменения, внесенные на узле с наибольшим приоритетом, побеждают во всех конфликтах. В случае клиентских подписок первое изменение, записанное на издателе, побеждает в конфликте.  
  
     После того, как подписка создана, ее тип нельзя изменить.  
  
-   Обработчик бизнес-логики  
  
     Платформа обработчика бизнес-логики всегда доступна для добавления сборки управляемого кода, который выполняется во время процесса синхронизации слиянием. Сборка включает бизнес-логику, которая может реагировать на конфликты и некоторые другие условия, возникающие во время синхронизации. Дополнительные сведения см. в статье [Выполнение бизнес-логики при синхронизации слиянием](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
-   Пользовательский сопоставитель на основе COM  
  
     Репликация слиянием обеспечивает API-интерфейс, предназначенный для написания сопоставителей в виде COM-объектов на различных языках программирования — [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] , [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]и других. Дополнительные сведения см. в статье [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
-   Основанный на технологии COM сопоставитель, поддерживаемый [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] includes a number of COM-based resolvers. Дополнительные сведения см. в статье [Microsoft COM-Based Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 Сведения о выборе подходящего типа сопоставителя см. в статье [Выбор сопоставителя](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md).  
  
> [!NOTE]  
>  Некоторые сопоставители статей написаны для разрешения конфликтов только для определенных операций. Например, сопоставитель может обрабатывать обновления, но не вставки или удаления. Сопоставитель конфликтов на основе приоритетов (по умолчанию) обрабатывает все конфликты, не обработанные сопоставителем статей.  
  
 Указание типа подписки на публикацию слиянием и приоритета устранения конфликтов см. в разделе  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Specify a Merge Subscription Type and Conflict Resolution Priority &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   Программирование репликации с помощью [!INCLUDE[tsql](../../../includes/tsql-md.md)] и объектов RMO: [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) и [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>Интерактивный сопоставитель  
 Репликация предоставляет пользовательский интерфейс интерактивного сопоставителя, который может использоваться совместно либо с сопоставителем конфликтов на основе приоритетов (по умолчанию), либо с сопоставителем статей. При выполнении синхронизации по требованию с помощью диспетчера синхронизации [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows интерактивный сопоставитель отображает конфликтные данные во время выполнения, позволяя выбрать методы разрешения конфликтов. Дополнительные сведения о том, как включить интерактивное устранение конфликтов и запуск интерактивного сопоставителя, см. в разделе [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="viewing-conflicts"></a>Просмотр конфликтов  
 Наиболее простым способом просмотра конфликтов является использование средства просмотра конфликтов репликации, доступного из среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] также предоставляет хранимые процедуры, которые позволяют создавать запросы к таблицам конфликтов.). Средство просмотра конфликтов и интерактивный сопоставитель являются аналогичными инструментами, но интерактивный сопоставитель позволяет разрешать конфликты во время выполнения синхронизации, в то время как средство просмотра конфликтов предназначено для просмотра конфликтов после их разрешения. Если метаданные конфликта остаются доступными в системных таблицах (по умолчанию метаданные конфликтов сохраняются в течение 14 суток), то результаты устранения конфликтов можно изменить в средстве просмотра конфликтов, однако при необходимости частого прямого вмешательства стоит рассмотреть возможность использования интерактивного сопоставителя.  
  
> [!NOTE]  
>  Конфликты, затрагивающие логические записи, не отображаются в средстве просмотра конфликтов. Для просмотра сведений о таких конфликтах используются хранимые процедуры репликации. Дополнительные сведения см. в статье [Просмотр сведений о конфликтах для публикаций слиянием (программирование репликации на языке Transact-SQL)](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
 Средство просмотра конфликтов отображает информацию из трех системных таблиц:  
  
-   При репликации для каждой таблицы в статье слияния создается таблица конфликтов с именем следующего вида: **MSmerge_conflict_\<имя_публикации>_\<имя_статьи>**.  
  
     Таблицы конфликтов имеют структуру, аналогичную структуре таблиц, на которых они основаны. Строка в одной из этих таблиц состоит из проигравшей версии строки конфликта (победившая версия строки находится в существующей пользовательской таблице).  
  
-   Таблица **MSmerge_conflicts_info** содержит сведения о каждом из конфликтов, включая его тип.  
  
-   Таблица **sysmergearticles** определяет пользовательские таблицы, для которых существуют таблицы конфликтов, и предоставляет информацию об этих таблицах конфликтов.  
  
 По умолчанию сведения о конфликтах сохраняются:  
  
-   На издателе и подписчике, если уровень совместимости публикации 90RTM или выше.  
  
-   На издателе, если уровень совместимости публикации ниже, чем 80RTM.  
  
-   На издателе, если подписчики используют [!INCLUDE[ssEW](../../../includes/ssew-md.md)]. Данные о конфликтах не могут храниться на подписчиках, использующих [!INCLUDE[ssEW](../../../includes/ssew-md.md)] .  
  
 **Просмотр конфликтов**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   Репликация [!INCLUDE[tsql](../../../includes/tsql-md.md)] Программирование: [Просмотр сведений о конфликтах для публикаций слиянием (программирование репликации на языке Transact-SQL)](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="see-also"></a>См. также:  
 [Синхронизация данных](../../../relational-databases/replication/synchronize-data.md)  
  
  