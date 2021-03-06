---
title: Сведения о публикации, трассировочные токены (публикация транзакций, SQL Server 2005 и более поздние версии) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 287d565947a13621fd3ba39cff6437ff76894c03
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792113"
---
# <a name="publication-information-tracer-tokens-transactional-publication-sql-server-2005-and-later"></a>Сведения о публикации, трассировочные токены (публикация транзакций, SQL Server 2005 и более поздние версии)
  На вкладке **Трассировочные токены** можно проверить соединения и измерить задержку той системы, где используется репликация транзакций. Токен (небольшой объем данных) записывается в журнал транзакций базы данных публикации и помечается так, как если бы он был обычной реплицируемой транзакцией, а затем проходит по системе, позволяя вычислить следующие характеристики:  
  
-   Время, прошедшее между фиксацией транзакции на издателе и вставкой соответствующей команды в базу данных распространителя на распространителе.  
  
-   Время, прошедшее между вставкой команды в базу данных распространителя и соответствующей транзакцией, зафиксированной у подписчика.  
  
 Из этих вычислений можно получить ответы на следующие вопросы:  
  
-   Какой подписчик позднее всех получает изменения от издателя?  
  
-   Какие подписчики, ожидающие получение трассировочного токена, его не получили (если таковые имеются)?  
  
## <a name="options"></a>Параметры  
 Чтобы изменить способ отображения данных в сетке, щелкните правой кнопкой мыши сетку, а затем один из следующих параметров.  
  
-   **Сортировка**: Сортировка по столбцам одного или нескольких в **Сортировка столбцов** диалоговое окно.  
  
-   **Выберите столбцы для отображения**: Выберите столбцы для отображения и порядок их отображения в **выбрать столбцы** диалоговое окно.  
  
-   **Фильтр**: Фильтрация строк в сетке на основании значений столбцов в **настройки фильтра** диалоговое окно.  
  
-   **Очистить фильтр**: удалить все настройки фильтра для сетки.  
  
 Настройки фильтра уникальны для каждой сетки. Выбор и сортировка столбцов применяются ко всем сеткам одного типа, как, например, сетка публикаций для каждого издателя.  
  
 **Вставить трассировочный маркер**  
 Выберите этот пункт, чтобы вставить трассировочный токен в журнал транзакций у издателя.  
  
 **Время вставки**  
 Выберите время вставки трассировочного токена. Данные задержки будут выводиться, начиная с этого момента. По умолчанию выводятся данные с самым поздним временем.  
  
> [!NOTE]  
>  Данные трассировочных токенов хранятся в течение того же периода времени, что и другие данные предыстории; этот период определяется сроком хранения журнала в базе данных распространителя. Дополнительные сведения о доступе к этим диалоговым окнам см. в статье [Просмотр и изменение свойств издателя и распространителя](view-and-modify-distributor-and-publisher-properties.md).  
  
 **Подписка**  
 Имя каждой подписки на публикацию.  
  
 **От издателя к распространителю**  
 Время, прошедшее между фиксацией транзакции на издателе и вставкой соответствующей команды в базу данных распространителя на распространителе. Значение **Ожидание** указывает, что токен еще не достиг распространителя. Если состояние ожидания не меняется, убедитесь, что запущен агент чтения журнала.  
  
 **От распространителя к подписчику**  
 Время, прошедшее между вставкой команды в базу данных распространителя и соответствующей транзакцией, зафиксированной на подписчике. Значение **Ожидание** указывает, что токен еще не достиг подписчика. Если состояние ожидания не меняется, убедитесь, что запущен агент распространителя.  
  
 **Общая задержка**  
 Время, прошедшее между фиксацией транзакции у издателя и фиксацией соответствующей транзакции у подписчика. Это значение является совокупной задержкой системы репликации для этого подписчика на данный момент. Значение **Ожидание** указывает, что токен еще не достиг подписчика.  
  
## <a name="see-also"></a>См. также  
 [Запуск и остановка агента репликации (среда SQL Server Management Studio)](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Запуск монитора репликации](monitor/start-the-replication-monitor.md)   
 [Измерение задержки и проверка правильности соединений для репликации транзакций](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Наблюдение за производительностью с помощью монитора репликации](monitor/monitor-performance-with-replication-monitor.md)   
 [Наблюдение за репликацией](monitoring-replication.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  
  
  
