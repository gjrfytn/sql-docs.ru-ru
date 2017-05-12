---
title: "Репликация транзакций | Документация Майкрософт"
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
- transactional replication, about transactional replication
- transactional replication
ms.assetid: 3ca82fb9-81e6-4c3c-94b3-b15f852b18bd
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c496335127a2f2d8acbacec53efa8ecdae697cfc
ms.lasthandoff: 04/11/2017

---
# <a name="transactional-replication"></a>Репликация транзакций
  Репликация транзакций обычно начинается с создания моментального снимка объектов и данных базы данных публикации. Как только создан исходный моментальный снимок, последующие изменения данных и схемы на издателе обычно доставляются подписчику без задержек (практически в реальном времени). Изменения данных применяются на подписчике в том же порядке и в тех же рамках транзакций, в которых они выполнялись у издателя. Поэтому в пределах публикации гарантируется согласованность транзакций.  
  
 Репликация транзакций обычно используется в серверных средах и пригодна в следующих случаях:  
  
-   Необходимо, чтобы дополнительные изменения распространялись подписчикам сразу же, как только они происходят.  
  
-   Для приложения необходимы малые задержки между моментом внесения изменений на издателе и моментом прибытия изменений на подписчик.  
  
-   Для приложения необходим доступ к промежуточным состояниям данных. Например, если строка изменяется пять раз, репликация транзакций позволяет приложению реагировать на каждое изменение (например, срабатывание триггера), а не просто на окончательное изменение строки.  
  
-   На издателе выполняется очень большой объем вставок, обновлений и удалений.  
  
-   Издатель и подписчик являются базами данных, отличными от баз данных[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (например, Oracle).  
  
 По умолчанию для подписчиков все подписки на публикацию транзакций доступны только для чтения, так как все изменения нельзя применить на издателе. Однако репликация транзакций позволяет выполнять обновления на подписчике.  
  
 **В этом разделе**  
  
 [Как работает репликация транзакций](#HowWorks)  
  
 [Исходная база данных](#Dataset)  
  
 [агент моментальных снимков](#SnapshotAgent)  
  
 [Агент чтения журнала.](#LogReaderAgent)  
  
 [Агент распространителя](#DistributionAgent)  
  
##  <a name="HowWorks"></a> Как работает репликация транзакций  
 Репликация транзакций реализуется агентом моментальных снимков, агентом чтения журналов и агентом распространителя [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Агент моментальных снимков готовит файлы моментальных снимков, содержащие схему, данные публикуемых таблиц и объекты базы данных, хранит файлы в папке моментальных снимков и записывает задания синхронизации в базу данных распространителя на распространителе.  
  
 Агент чтения журнала контролирует журнал транзакций всех баз данных, настроенных для репликации транзакций, и копирует транзакции, отмеченные для репликации, из журнала транзакций в базу данных распространителя, которая действует как надежная очередь с функциями хранения и переадресации данных. Агент распространителя копирует файлы исходного моментального снимка из папки моментальных снимков и транзакции, хранимые в таблицах базы данных распространителя, на подписчики.  
  
 Добавочные изменения, вносимые на издателе, поступают подписчикам согласно расписанию агента распространителя, который может выполняться непрерывно для достижения минимальной задержки либо в запланированные интервалы времени. Поскольку изменения данных должны вноситься на издателе (когда репликация транзакций используется без немедленного обновления и отложенного обновления), возникновение конфликтов обновления исключается. В конечном счете, для всех подписчиков устанавливаются такие же значения, как и на издателе. Если с репликацией транзакций используется немедленное или отложенное обновление, в этом случае обновления могут вноситься на подписчике, и для отложенного обновления возможно возникновение конфликтов.  
  
 На следующем рисунке показаны основные компоненты репликации транзакций.  
  
 ![Компоненты и поток данных репликации транзакций](../../../relational-databases/replication/transactional/media/trnsact.gif "Компоненты и поток данных репликации транзакций")  
  
##  <a name="Dataset"></a> Исходная база данных  
 Прежде чем новый подписчик репликации транзакций сможет получить добавочные изменения от издателя, на подписчике должны находиться таблицы со схемой и данными, совпадающими со схемой и данными в таблицах на издателе. Исходный набор данных обычно является моментальным снимком, созданным агентом моментальных снимков, который распространяется и применяется агентом распространителя. Исходный набор данных может также предоставляться через резервную копию или другим способом, например службами [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Integration Services.  
  
 При распространении и применении моментальных снимков на подписчиках изменениям подвергаются только те подписчики, которые ожидают исходные моментальные снимки. Другие подписчики на эту публикацию (которые уже инициализированы) остаются без изменений.  
  
## <a name="concurrent-snapshot-processing"></a>Параллельная обработка моментальных снимков  
 Репликация моментальных снимков устанавливает общие блокировки на все таблицы, опубликованные как часть репликации, на время создания моментального снимка. Это может препятствовать выполнению обновлений публикуемых таблиц. Параллельная обработка моментального снимка, выполняемая по умолчанию с репликацией транзакций, не сохраняет общие блокировки в течение всего времени создания моментального снимка, что позволяет пользователям продолжать работу без перерыва, пока репликация создает файлы исходного моментального снимка.  
  
##  <a name="SnapshotAgent"></a> агент моментальных снимков  
 Агент моментальных снимков реализует исходный моментальный снимок в репликации транзакций с помощью тех же самых процедур, которые используются в репликации моментальных снимков (за исключением параллельной обработки моментального снимка, описанной выше).  
  
 После создания файлов моментальных снимков их можно просмотреть в папке моментальных снимков, используя проводник [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
##  <a name="LogReaderAgent"></a> Изменение данных и агент чтения журналов  
 Агент чтения журналов выполняется на распространителе; обычно он выполняется непрерывно, но может также запускаться согласно задаваемому расписанию. При выполнении агент чтения журнала сначала читает журнал транзакций публикации (тот же самый журнал базы данных используется для отслеживания и восстановления данных во время выполнения обычных операций компонента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Database Engine) и выявляет все инструкции INSERT, UPDATE и DELETE или другие изменения данных в транзакциях, отмеченных для репликации. Далее агент копирует эти транзакции в пакетах в базу данных распространителя на стороне распространителя. Агент чтения журнала использует внутреннюю хранимую процедуру **sp_replcmds** для получения из журнала следующего набора команд, отмеченных для репликации. После этого база данных распространителя становится очередью с функциями хранения и переадресации, из которой изменения отправляются подписчикам. В базу данных распространителя отправляются только зафиксированные транзакции.  
  
 После того как весь пакет транзакций успешно записан в базу данных распространителя, он фиксируется. После фиксации каждого пакета команд на распространителе агент чтения журнала вызывает хранимую процедуру **sp_repldone** , чтобы отметить место, где в последний раз была завершена репликация. В заключение, агент отмечает строки в журнале транзакций, готовые к очистке. Строки, ожидающие репликации, не очищаются.  
  
 Команды транзакций хранятся в базе данных распространителя до тех пор, пока они не будут распространены на все подписчики или пока не закончится максимальный срок хранения на распространителе. Подписчики получают транзакции в том же порядке, в котором они применялись на издателе.  
  
##  <a name="DistributionAgent"></a> Агент распространителя  
 Агент распространителя работает на распространителе для принудительных подписок и на подписчике для подписок по запросу. Агент перемещает транзакции из базы данных распространителя на подписчик. Если подписка отмечена для проверки подлинности, агент распространителя также проверяет соответствие данных на издателе и подписчике.  
  
  