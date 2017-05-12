---
title: "Расширенный просмотр целевых данных из расширенных событий в SQL Server | Документация Майкрософт"
ms.custom: 
ms.date: 10/04/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d7fcf086b0eb18db72c2d710c061ccee9c01aaf
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>Расширенный просмотр целевых данных из расширенных событий в SQL Server
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]


В этой статье содержатся сведения об использовании дополнительных возможностей среды SQL Server Management Studio (SSMS.exe) для подробного просмотра целевых данных из расширенных событий. Здесь описывается выполнение следующих задач:


- открытие и просмотр целевых данных различными способами;
- экспорт целевых данных в различные форматы с помощью специальных меню или панели инструментов для расширенных событий;
- управление данными во время просмотра или перед экспортом.



### <a name="prerequisites"></a>Предварительные требования

В данной статье предполагается, что вы уже знаете, как создать и запустить сеанс событий. Инструкции по созданию сеанса событий приводятся в следующей статье:

[Краткое руководство. Расширенные события в SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


В этой статье также предполагается, что вы установили последний ежемесячный выпуск SSMS. Справочные сведения приведены в следующих статьях:

- [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)



### <a name="differences-with-azure-sql-database"></a>Отличия от базы данных SQL Azure


Реализация и возможности расширенных событий в Microsoft SQL Server и базы данных SQL Azure во многом аналогичны. Однако существуют некоторые различия, которые влияют на пользовательский интерфейс среды SSMS.


- Для базы данных SQL целевой объект package0.event_file не может быть файлом на локальном диске. Вместо него необходимо использовать контейнер хранилища Azure. Поэтому при подключении к базе данных SQL в пользовательском интерфейсе SSMS выводится запрос о контейнере хранилища, а не локальном пути и имени файла.


- В пользовательском интерфейсе SSMS флажок **Просмотр данных, передаваемых в режиме реального времени** отображается серым цветом и отключен, так как эта функция недоступна для базы данных SQL.


- Вместе с SQL Server устанавливается несколько расширенных событий. В узле **Сеансы** отображается событие **AlwaysOn_health** и несколько других. Они не видны при подключении к базе данных SQL, так как не существуют для нее.


Эта статья применяется к SQL Server. Здесь используется цель event_file, являющаяся одной из различий. Дальнейшие упоминания отличий связаны с важными или неочевидными различиями.


Сведения о расширенных событиях, относящихся к базе данных SQL Azure, см. в статье:

- [Расширенные события в базе данных SQL Azure](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. Общие параметры


Как правило, доступ к дополнительным параметрам осуществляется указанными далее способами.


- Обычное меню — **Файл** > **Открыть** > **Файл**.
- Щелчки правой кнопкой мыши в **обозревателе объектов** и последующий выбор пунктов **Управление** > **Расширенные события**.
- Специальное меню **Расширенные события**и специальная панель инструментов для расширенных событий.
- Щелчки правой кнопкой мыши в области с вкладками, где отображаются целевые данные.



## <a name="b-bring-target-data-into-ssms-for-display"></a>Б. Перенос целевых данных в SSMS для отображения


Существуют разные способы переноса целевых данных event_file в пользовательский интерфейс SSMS. При указании event_file задаются его имя и путь к файлу:

- XEL — это расширение имени файла.


- Каждый раз при запуске сеанса событий система внедряет большое целое число в новое имя файла, чтобы сделать имя файла уникальным и отличным от имени в предыдущий момент запуска сеанса.
  - *Пример:* Checkpoint_Begins_ES_0_131103935140400000.xel


- Содержимое внутри XEL не является обычным текстом, который можно просмотреть с помощью Notepad.exe.
  - Если необходимо, для объединения нескольких XEL-файлов можно последовательно выбрать **Файл** > **Открыть** > **Объединить файлы расширенных событий**.



SSMS может отображать данные из любого целевого объекта. Однако для разных целевых объектов отображаются данные разного вида.

- *event_file:* данные из целевого объекта event_file отображаются очень хорошо и с доступными расширенными возможностями.


- *ring_buffer:* данные из цели кольцевого буфера ring_buffer отображаются в виде необработанного XML.


- Уровень отображения данных других целевых объектов находится где-то между уровнем отображения event_file и ring_buffer.
  - В число других таких целей входят event_counter, histogram и pair_matching.


- *etw_classic_sync_target:* SSMS не может отображать данные из целевого объекта etw_classic_sync_target.



### <a name="b1-open-xel-with-menu-file--open--file"></a>Б.1. Открытие XEL-файла путем выбора "Файл" > "Открыть" > "Файл"


XEL-файл можно открыть с помощью стандартного меню **Файл** > **Открыть** > **Файл**.

XEL-файл также можно перетащить на панель вкладок в пользовательском интерфейсе среды SSMS.



### <a name="b2-view-target-data"></a>Б.2. Просмотр целевых данных


Параметр **Просмотреть целевые данные** используется для отображения данных, записанных на данный момент.


В области **Обозреватель объектов** можно развернуть следующие узлы и щелкнуть правой кнопкой мыши:

- **Управление** > **Расширенные события** > **Сеансы** > *[ваш_сеанс]* > *[ваш_целевой_узел]* > **Просмотреть целевые данные**.


Целевые данные отображаются в SSMS в области с вкладками. Это показано на следующем снимке экрана.


![ваш целевой объект > Просмотреть целевые данные](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> Параметр **Просмотреть целевые данные** используется для отображения *накопленных данных из нескольких XEL-файлов* из заданного сеанса событий. В ходе каждого цикла **Запуск**-**остановка** создается файл с внедренным в его имя целочисленным значением времени (для каждого последующего файла указывается более позднее время). Все файлы имеют одинаковое корневое имя.



#### <a name="b3-watch-live-data"></a>Б.3.Просмотр динамических данных


В активном сеансе событий можно просматривать данные событий в реальном времени по мере их получения целевым объектом.


- **Управление** > **Расширенные события** > **Сеансы** > *[ваш-сеанс]* > **Просмотреть динамические данные**.


![ваш сеанс > Просмотреть динамические данные](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


Отображение данных обновляется через интервал, который можно задать. См. параметр **Максимальная задержка диспетчеризации** :

- **Расширенные события** > **Сеансы** > *[ваш_сеанс]* > **Свойства** > **Дополнительно** > **Максимальная задержка диспетчеризации**



### <a name="b4-view-xel-with-sysfnxefiletargetreadfile-function"></a>Б.4. Просмотр XEL-файла с помощью функции sys.fn_xe_file_target_read_file


Для выполнения пакетной обработки следующая системная функция может создать XML для записей в XEL-файле:

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>В. Экспорт целевых данных


Целевые данные, добавленные в SSMS, можно экспортировать в различные форматы, выполнив приведенные ниже действия.


1. Перемещение фокуса на отображение данных.
    - Неожиданно появляется новая панель инструментов и новый пункт меню для расширенных событий.

    ![Экспорт отображаемых данных путем выбора "Расширенные события" > "Экспорт" > (CSV-, XEL-файл или в таблицу)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. Щелкните новый пункт меню **Расширенные события**.
3. Щелкните **Экспорт**, а затем выберите формат.



## <a name="d-manipulate-data-in-the-display"></a>Г. Управление отображаемыми данными


В пользовательском интерфейсе среды SSMS помимо простого просмотра данных существует несколько способов управления данными.



### <a name="d1-context-menus-in-the-data-display"></a>Г.1. Контекстные меню в отображении данных


В разных местах отображения данных существуют различные контекстные меню, вызываемые щелчком правой кнопкой мыши.



#### <a name="d11-right-click-a-data-cell"></a>Г.1.1. Щелчок ячейки данных правой кнопкой мыши


На следующем снимке экрана показано контекстное меню, вызываемое при щелчке ячейки правой кнопкой мыши в отображении данных. На снимке экрана также показано расширение пункта меню **Копировать** .


![Щелчок ячейки правой кнопкой мыши в отображении данных](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>Г.1.2. Щелчок заголовка столбца правой кнопкой мыши


На следующем снимке экрана показано контекстное меню, вызванное щелчком заголовка **timestamp** правой кнопкой мыши.


![Щелчок заголовка столбца правой кнопкой мыши в отображении данных. И таблица сведений.](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


На предыдущем снимке экрана также показана специальная панель инструментов для расширенных событий. Яркость отображения кнопки "Сведения" означает, что кнопка активна. Поэтому на рисунке также показана вкладка **Сведения** и сетка как вторая часть отображения данных.



### <a name="d2-choose-columns-merge-columns"></a>Г.2. Выбор столбцов, объединение столбцов


В окне **Выбор столбцов** можно выбрать, какие столбцы данных будут отображаться, а какие — нет. Пункт меню **Выбрать столбцы** находится в нескольких разных местах:

- в меню **Расширенные события** ;
- на панели инструментов расширенных событий;
- в контекстном меню заголовка в отображении данных.


После щелчка пункта **Выбрать столбцы**открывается диалоговое окно с подобным именем.


![В диалоговом окне "Выбор столбцов" также находятся параметры объединения столбцов.](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>Г.2.1. Объединение столбцов


В диалоговом окне **Выбор столбцов** есть раздел, предназначенный для объединения нескольких столбцов в один для целей:

- Отображение.
- Экспорт.



### <a name="d3-filters"></a>Г.3.Фильтры


В области расширенных событий находятся два основных типа фильтров, которые можно указать.

- *Фильтры для предварительной фильтрации.* Фильтры, которые сокращают объем данных, отправляемых подсистемой событий в целевой объект.

- *Фильтры для последующей фильтрации.* Фильтры, которые можно выбрать в пользовательском интерфейсе среды SSMS, чтобы исключить отображение некоторых целевых записей.


В среде SSMS доступны следующие фильтры отображения:

- Фильтр *диапазона времени* , который проверяет столбец **timestamp** .
- Фильтр *значений столбцов* .


Связь между фильтром времени и фильтром столбцов является логическим*AND*.


![Фильтры диапазона времени и фильтры столбцов в диалоговом окне "Фильтры"](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>Г.4. Группирование и агрегирование


Первым шагом к сводному агрегированию данных является группирование строк по совпадающим значениям в заданном столбце.



#### <a name="d41-grouping"></a>Г.4.1. Группирование


На панели инструментов расширенных событий кнопка **Группирование** используется для открытия диалогового окна для группирования отображаемых данных по заданному столбцу. На следующем снимке экрана показано диалоговое окно, используемое для группировки по столбцу *name*.

![Панель инструментов > кнопка "Группирование" > диалоговое окно "Группирование"](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

После группировки данные отображаются в новом виде, как показано далее.

![Новое отображение после группирования](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>Г.4.2. Агрегирование


После группирования отображаемых данных можно перейти к агрегированию данных в других столбцах.  На следующем снимке экрана показаны сгруппированные данные, агрегируемые по типу *count*.

![Панель инструментов > кнопка "Агрегирование" > диалоговое окно "Агрегирование"](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

После агрегирования данные отображаются в новом виде, как показано далее.

![Панель инструментов > кнопка "Агрегирование" > диалоговое окно "Агрегирование"](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>Г.5. Просмотр плана запроса времени выполнения


Событие **query_post_execution_showplan** позволяет просмотреть фактический план запроса в пользовательском интерфейсе SSMS. На отображаемой панели **Сведения** на вкладке **План запроса** можно увидеть схему плана запроса. При наведении указателя мыши на узел в плане запроса появляется список имен свойств и их значений для узла.


![План запроса со списком свойств для одного узла](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)


