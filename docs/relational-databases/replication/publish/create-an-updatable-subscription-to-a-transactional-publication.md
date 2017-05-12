---
title: "Создание обновляемых подписок для публикаций транзакций | Документация Майкрософт"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 94a6afee0fbc828b7c3036cfc4d1282b71674384
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>Создание обновляемых подписок для публикаций транзакций

> [!NOTE]  
>  Эта функция поддерживается в версиях [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] с 2012 по 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Настроить обновляемые подписки можно на странице **Обновляемые подписки** **мастера новых публикаций**. Эта страница доступна только тогда, когда включены публикации транзакций для обновляемых подписок. Дополнительные сведения о включении обновляемых подписок см. в статье [Включение обновляемых подписок для публикаций транзакций](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>Настройка обновляемой подписки из издателя  

1. Подключитесь к издателю в среде Microsoft SQL Server Management Studio и раскройте узел сервера.

2. Раскройте папку **Репликация** , а затем папку **Локальные публикации** .

3. Щелкните правой кнопкой мыши публикацию транзакций, настроенную для обновления подписок, а затем щелкните **Создать подписку**.

4. На страницах мастера укажите параметры подписки, например, место, где должен выполняться агент распространения.

5. На странице **Обновляемые подписки** в **мастере создания подписок** должен быть отмечен параметр **Реплицировать**.

6. Выберите параметр **Зафиксировать на стороне издателя** в раскрывающемся списке.

    * Для немедленного обновления подписок выберите **Одновременно фиксировать изменения**. Если выбран этот параметр, а для публикации разрешено обновление подписок посредством очередей (по умолчанию для публикаций, созданных с помощью мастера создания публикаций), то свойство подписки **update_mode** будет иметь значение **failover**. Этот режим позволяет, при необходимости позднее перейти к обновлению посредством очередей.

    * Для обновления подписок посредством очередей выберите **Ставить изменения в очередь и фиксировать при первой возможности**. Если выбран этот параметр, для публикации разрешено немедленное обновление подписок (по умолчанию для публикаций, созданных с помощью мастера создания публикаций), и на подписчике работает SQL Server 2005 или более поздняя версия, то свойство подписки **update_mode** примет значение queued failover. Этот режим позволяет, при необходимости, включить немедленное обновление позднее.

    Дополнительные сведения см. в статье [Переключение между режимами обновления для обновляемой подписки на публикацию транзакций](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. Страница **Имя входа для обновляемых подписок** отображается для подписок, применяющих немедленное обновление, либо имеющих параметр **update_mode** в значении **queued failover**. На странице **Имя входа для обновляемых подписок** укажите связанный сервер, через который устанавливаются соединения с издателем для обновления подписок. Соединения используются триггерами, которые запускаются на подписчике и распространяют изменения на издатель. Выберите один из следующих вариантов.

    * **Создать связанный сервер, который соединяется с использованием проверки подлинности SQL Server.** Выберите этот параметр, если вы не определили удаленный сервер или связанный сервер между подписчиком и издателем. Репликация создает связанный сервер. Указанная учетная запись уже должна существовать на издателе.

    * **Использовать уже указанный связанный или удаленный сервер** Выберите этот параметр, если вы определили удаленный сервер или связанный сервер между подписчиком и издателем с помощью процедуры [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md),[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio или другого метода.

    Дополнительные сведения о разрешениях, требуемых для учетной записи связанного сервера, см. в статье **Подписки, обновляемые посредством очередей** из [введите здесь описание ссылки](../../../relational-databases/replication/security/secure-the-subscriber.md)

8. Завершите работу мастера.

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>Настройка обновляемой подписки из подписчика


1. Подключитесь к подписчику в среде Microsoft SQL Server Management Studio и раскройте узел сервера.

2. Раскройте папку **Репликация** .

3. Щелкните правой кнопкой мыши папку **Локальные подписки** , затем щелкните **Создать подписку**.

4. На странице **Публикация** **мастера создания подписки** выберите **Найти издатель SQL Server** из раскрывающегося списка **Издатель**.

5. Соединитесь с издателем в диалоговом окне **Соединение с сервером** .

6. Выберите публикацию транзакций, настроенную для обновляемых подписок на странице **Публикация**.

7. На страницах мастера укажите параметры подписки, например, место, где должен выполняться агент распространения.

8. На странице **Обновляемые подписки** в мастере создания подписок должен быть отмечен параметр **Реплицировать**.

9. Выберите параметр **Зафиксировать на стороне издателя** в раскрывающемся списке.

    * Для немедленного обновления подписок выберите **Одновременно фиксировать изменения**. Если выбран этот параметр, а для публикации разрешено обновление подписок посредством очередей (по умолчанию для публикаций, созданных с помощью мастера создания публикаций), то свойство подписки **update_mode** будет иметь значение **failover**. Этот режим позволяет, при необходимости позднее перейти к обновлению посредством очередей.

    * Для обновления подписок посредством очередей выберите **Ставить изменения в очередь и фиксировать при первой возможности**. Если выбран этот параметр, для публикации разрешено немедленное обновление подписок (по умолчанию для публикаций, созданных с помощью мастера создания публикаций), и на подписчике работает SQL Server 2005 или более поздняя версия, то свойство подписки **update_mode** примет значение **queued failover**. Этот режим позволяет, при необходимости, включить немедленное обновление позднее.

    Дополнительные сведения см. в статье [Переключение между режимами обновления для обновляемой подписки на публикацию транзакций](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. Страница **Имя входа для обновляемых подписок** отображается для подписок, применяющих немедленное обновление, либо имеющих параметр **update_mode** в значении **queued failover**. На странице **Имя входа для обновляемых подписок** укажите связанный сервер, через который устанавливаются соединения с издателем для обновления подписок. Соединения используются триггерами, которые запускаются на подписчике и распространяют изменения на издатель. Выберите один из следующих вариантов.

    * **Создать связанный сервер, который соединяется с использованием проверки подлинности SQL Server.** Выберите этот параметр, если вы не определили удаленный сервер или связанный сервер между подписчиком и издателем. Репликация создает связанный сервер. Указанная учетная запись уже должна существовать на издателе.

    * **Использовать уже указанный связанный или удаленный сервер** Выберите этот параметр, если вы определили удаленный сервер или связанный сервер между подписчиком и издателем с помощью процедуры [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md),[sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio или другого метода.

    Дополнительные сведения о разрешениях, требуемых для учетной записи связанного сервера, см. в статье **Подписки, обновляемые посредством очередей** из [введите здесь описание ссылки](../../../relational-databases/replication/security/secure-the-subscriber.md)

11. Завершите работу мастера.

## <a name="see-also"></a>См. также:

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[Создание обновляемой подписки для публикации транзакций](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 

