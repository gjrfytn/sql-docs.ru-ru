---
title: "Переключение между режимами обновления для обновляемой подписки на публикацию транзакций | Документация Майкрософт"
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
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 271b9ff4060284d50e66130f8bbd4b8d5b288912
ms.lasthandoff: 04/11/2017

---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Переключение между режимами обновления для обновляемой подписки на публикацию транзакций
  В этом разделе описывается переключение между режимами обновления для обновляемой подписки на публикацию транзакций в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Режим обновляемых подписок можно указать с помощью мастера создания подписки. Сведения об установке режима с помощью этого мастера см. в статье [Просмотр и изменение свойств подписки по запросу](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Рекомендации](#Recommendations)  
  
-   **Для переключения между режимами обновления для обновляемой подписки на публикацию транзакций используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Переход из режима немедленного обновления в режим отложенного обновления может быть произведен в любой момент, однако после этого возврат в режим немедленного обновления будет возможен только тогда, когда появится соединение между подписчиком и издателем, а агент чтения очереди применит к издателю все сообщения, находящиеся в очереди.  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Если обновляемая подписка на публикацию транзакций поддерживает отработку отказа из одного режима обновления в другой, то возможно программное переключение режимов обновления для выхода из ситуаций, когда возможность подключения изменяется на короткий промежуток времени. Режим обновления может быть установлен как программно, так и по запросу при помощи хранимых процедур репликации. Дополнительные сведения см. в статье [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
> [!NOTE]  
>  Чтобы изменить режим обновления после создания подписки, необходимо установить для свойства **update_mode** значение **failover** (что позволяет переключиться с немедленного обновления на обновление посредством очередей) или значение **queued failover** (что позволяет переключиться с обновления по очереди на немедленное обновление), когда подписка создана. Эти свойства устанавливаются автоматически в мастере создания подписки.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Установка режима обновления для принудительной подписки  
  
1.  Подключитесь к подписчику в [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]и раскройте узел сервера.  
  
2.  Раскройте папку **Репликация** , а затем — папку **Локальные подписки** .  
  
3.  Щелкните правой кнопкой подписку, для которой хотите установить режим обновления, и щелкните **Выбор метода обновления**.  
  
4.  В диалоговом окне **Выбор метода обновления — \<подписчик>: \<база_данных_подписки>** выберите **Немедленное обновление** или **Обновление посредством очереди**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Установка режима обновления для подписки по запросу  
  
1.  В диалоговом окне **Свойства подписки — \<издатель>: \<база данных публикации>** выберите значение **Немедленно реплицировать изменения** или **Ставить изменения в очередь** для параметра **Метод обновления подписчика**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Дополнительные сведения о доступе к диалоговому окну **Свойства подписки — \<издатель>: \<база данных публикации>** см. в статье [Просмотр и изменение свойств подписки по запросу](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Переключение режимов обновления  
  
1.  Удостоверьтесь в том, что данная подписка поддерживает отработку отказа, выполнив хранимую процедуру [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) для подписки по запросу или [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) для принудительной подписки. Если значение **update mode** результирующего набора равен **3** или **4**, то отработка отказа поддерживается.  
  
2.  На подписчике в базе данных подписки выполните процедуру [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Задайте значения параметров **@publisher**, **@publisher_db**, **@publication**, а в качестве параметра **@failover_mode**укажите одно из следующих значений:  
  
    -   **queued** — переход в режим обновления посредством очередей при временной потере соединения;  
  
    -   **immediate** — переход в режим немедленного обновления, при восстановлении.  
  
## <a name="see-also"></a>См. также:  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  