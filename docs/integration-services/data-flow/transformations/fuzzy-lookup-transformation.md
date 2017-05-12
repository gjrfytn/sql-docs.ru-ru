---
title: "Преобразование &#171;Нечеткий уточняющий запрос&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzylookuptrans.f1"
helpviewer_keywords: 
  - "очистка данных"
  - "сравнение данных"
  - "разделители токенов [службы Integration Services]"
  - "временные индексы [службы Integration Services]"
  - "временные таблицы [службы Integration Services]"
  - "преобразование «Нечеткий уточняющий запрос»"
  - "ссылочные таблицы [службы Integration Services]"
  - "сопоставление схожих данных [службы Integration Services]"
  - "замена пропущенных значений"
  - "исправление данных [службы Integration Services]"
  - "кэш [службы Integration Services]"
  - "стандартизация данных [службы Integration Services]"
  - "уточняющие запросы [службы Integration Services]"
  - "степень достоверности [службы Integration Services]"
  - "нечеткие соответствия"
  - "замененные пропущенные значения [службы Integration Services]"
  - "пороги подобия [службы Integration Services]"
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
caps.latest.revision: 75
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 75
---
# Преобразование &#171;Нечеткий уточняющий запрос&#187;
  Преобразование «Нечеткий уточняющий запрос» выполняет задачи по очистке данных, такие как стандартизация данных, исправление данных и предоставление отсутствующих значений.  
  
> [!NOTE]  
>  Дополнительные сведения о преобразовании "Нечеткий уточняющий запрос", в том числе сведения об ограничениях производительности и памяти, см. в техническом документе [Преобразования "Нечеткий уточняющий запрос" и "Нечеткое группирование" в службах SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604).  
  
 Преобразование «Нечеткий уточняющий запрос» отличается от преобразования «Уточняющий запрос» использованием нечеткого соответствия. Преобразование «Уточняющий запрос» использует эквивалентное соединение для обнаружения совпадающих записей в ссылочной таблице. Возвращает записи хотя бы с одной совпадающей записью и возвращает записи без совпадающих записей. В то же время преобразование «Нечеткий уточняющий запрос» замечает и нечеткие соответствия, возвращая одну или несколько похожих записей из ссылочной таблицы.  
  
 В потоке данных пакета преобразование «Нечеткий уточняющий запрос» часто следует за преобразованием «Уточняющий запрос». Сначала преобразование «Уточняющий запрос» пытается найти точные совпадения. Если ничего не найдено, преобразование «Нечеткий уточняющий запрос» приводит несколько неточных соответствий из ссылочной таблицы.  
  
 Для данного преобразования необходим доступ к эталонному источнику данных, в котором содержатся значения, используемые для очистки и расширения входных данных. Эталонный источник данных должен быть таблицей в базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Соответствие между значением во входном столбце и значением в ссылочной таблице может быть точным или нечетким. Однако для настройки преобразования необходимо хотя бы одно нечеткое соответствие столбца. Если необходимы только четкие соответствия, используйте преобразование «Уточняющий запрос».  
  
 Это преобразование имеет один вход и один выход.  
  
 В нечетком соответствии могут использоваться только входные столбцы с типами данных **DT_WSTR** и **DT_STR**. Точное соответствие может быть применено к столбцам любых типов данных служб DTS, кроме **DT_TEXT**, **DT_NTEXT** и **DT_IMAGE**. Дополнительные сведения см. в статье [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md). Столбцы, которые участвуют в соединении входной и ссылочной таблиц, должны иметь совместимые типы данных. Например, можно соединить столбец с типом данных DTS **DT_WSTR** и столбец с типом данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nvarchar**, однако установление связи между столбцом с типом данных **DT_WSTR** и столбцом с типом данных **int** невозможно.  
  
 Это преобразование можно настраивать, определяя максимальный объем памяти, алгоритм сравнения строк и используемое данным преобразованием кэширование индексов и ссылочных таблиц.  
  
 Объем памяти, используемой преобразованием "Нечеткий уточняющий запрос", можно задать в пользовательском свойстве MaxMemoryUsage. Можно указать число мегабайтов (МБ) или значение 0, которое позволяет преобразованию использовать динамический объем памяти в зависимости от своих потребностей и наличия доступной физической памяти. Пользовательское свойство MaxMemoryUsage можно обновить с помощью выражения свойства при загрузке пакета. Дополнительные сведения см. в разделах [Выражения служб Integration Services (SSIS)](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Использование выражений свойств в пакетах](../../../integration-services/expressions/use-property-expressions-in-packages.md) и [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## Управление режимом нечеткого соответствия  
 Преобразование "Нечеткий уточняющий запрос" содержит три параметра настройки поиска: максимальное количество возвращаемых соответствий на входную строку, разделители маркеров и пороги подобия.  
  
 Преобразование возвращает ноль или более результатов поиска вплоть до максимального числа, определенного пользователем. Определение максимального числа результатов поиска не гарантирует того, что преобразование выдаст максимально возможное число результатов поиска; оно гарантирует только то, что количество результатов поиска, возвращаемое преобразованием, не превысит заданного числа. Если установить значение максимального количества результатов поиска больше 1, выходные данные преобразования могут содержать более одной строки на один уточняющий запрос и некоторые строки могут дублироваться.  
  
 Преобразование предоставляет набор разделителей, используемый по умолчанию для маркировки данных, но можно добавить собственные разделители токенов. В свойстве Delimiters содержатся установленные по умолчанию разделители. Маркировка важна, так как она определяет блоки внутри данных, которые будут сравниваться друг с другом.  
  
 Пороги подобия могут быть установлены на уровне компонентов и соединений. Порог подобия на уровне соединений доступен только тогда, когда преобразование «Нечеткий уточняющий запрос» производится между столбцами входной и ссылочной таблиц. Диапазон подобия охватывает значения от 0 до 1. Чем ближе порог к 1, тем более сходными должны быть строки и столбцы, чтобы называться дубликатами. Порог подобия определяется при помощи установки свойства MinSimilarity на уровне компонентов и соединений. Чтобы удовлетворять условиям подобия, определенным на уровне компонентов, все строки должны иметь во всех результатах поиска степень сходства, большую, чем порог подобия, определенный на уровне компонентов, или равную ему. Таким образом, невозможно определить очень близкие совпадения на уровне компонентов до тех пор, пока совпадения на уровне строк или соединений не будут столь же близки.  
  
 Каждое совпадение включает показатель сходства и показатель достоверности. Показатель сходства — это математическая мера структурного сходства между входной записью и записью, найденной преобразованием «Нечеткий уточняющий запрос» в ссылочной таблице. Показатель достоверности — это вероятность того, что полученная величина является наиболее точным совпадением с искомой величиной среди всех остальных результатов поиска в ссылочной таблице. Присвоенный записи показатель достоверности зависит от остальных найденных совпадающих записей. Например, соответствие между *СПб* и *Санкт-Петербург* обладает низкой степенью сходства независимо от других результатов поиска. Но если *Санкт-Петербург* является единственным результатом поиска, то показатель достоверности будет высоким. Если же и *Санкт-Петербург* , и *СПб* найдены в ссылочной таблице, то достоверность *СПб* будет высокой, а достоверность *Санкт-Петербург* будет низкой. Однако из того, что у результата поиска высокий показатель сходства может совсем не следовать, что у него высокий показатель достоверности. Например, если ищется значение *Раздел 4*, то результаты поиска *Раздел 1*, *Раздел 2*и *Раздел 3* будут иметь высокий показатель сходства, но низкий показатель достоверности, так как остается неясным, какой из результатов является наиболее близким к искомому.  
  
 Показатель сходства является десятичным числом от 0 до 1, причем показатель сходства, равный единице, означает точное совпадение значения во входном столбце и значения в ссылочной таблице. Показатель достоверности, также являющийся десятичным числом от 0 до 1, показывает достоверность результата поиска. Если не найдено ни одного возможного соответствия, то данной строке присваиваются значения показателей совпадения и достоверности, равные 0, а выходные столбцы, скопированные из ссылочной таблицы, будут содержать значения NULL.  
  
 Иногда преобразование «Нечеткий уточняющий запрос» может не найти соответствий в ссылочной таблице. Это может произойти в том случае, если входной строкой для уточняющего запроса является одиночное короткое слово. Например, *helo* не совпадет с *hello* в ссылочной таблице, если в том или каком-нибудь другом столбце строки нет других токенов.  
  
 Выходные столбцы преобразования включают входные столбцы, отмеченные как передаваемые столбцы, выделенные столбцы в таблице уточняющих запросов и следующие дополнительные столбцы:  
  
-   **_Similarity** — столбец, содержащий показатели сходства между значениями во входном и ссылочном столбце.  
  
-   **_Confidence** — столбец, содержащий показатели достоверности соответствий.  
  
 Преобразование использует соединение с базой данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] для создания временных таблиц, необходимых алгоритму нечеткого соответствия.  
  
## Выполнение преобразования «Нечеткий уточняющий запрос»  
 При первом запуске преобразования пакетом преобразование копирует ссылочную таблицу, добавляет ключ целочисленного типа данных в новую таблицу и создает индекс в ключевом столбце. Затем преобразование создает в копии ссылочной таблицы индекс, называемый индексом соответствия. В индексе соответствия сохраняются результаты маркировки значений во входных столбцах преобразования, а затем преобразование использует эти токены при операциях поиска. Индекс соответствия — это таблица базы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 При повторном выполнении пакета преобразование может либо использовать уже существующий индекс соответствия, либо создать новый индекс. Если ссылочная таблица является статической, пакет может избежать потенциально затратных процессов перестроения индекса для повторных сеансов очистки данных. Если выбрано использование уже существующего индекса, индекс будет создан при первом запуске пакета. Если несколько преобразований «Нечеткий уточняющий запрос» используют одну и ту же ссылочную таблицу, то все они могут использовать один и тот же индекс. Операции поиска должны быть одинаковыми, чтобы можно было использовать индекс повторно; в них должны задействоваться одни и те же столбцы. Индексу можно присвоить имя и выбрать соединение с базой данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , в которой он будет сохранен.  
  
 Если преобразование сохраняет индекс соответствия, этот индекс может поддерживаться автоматически. Это означает, что каждый раз при обновлении записей в ссылочной таблице индекс соответствия также будет обновляться. Поддержка индекса соответствия может уменьшить время обработки, так как исчезает необходимость перестройки индекса во время запуска пакета. Можно определить способ, как преобразование управляет индексом соответствия.  
  
 В следующей таблице приводятся описания параметров индекса соответствия.  
  
|Параметр|Description|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|Создает новый индекс, сохраняет и поддерживает его. Преобразование устанавливает триггеры на ссылочную таблицу для синхронизации ссылочной таблицы и таблицы индекса.|  
|**GenerateAndPersistNewIndex**|Создает и сохраняет новый индекс, но не поддерживает его.|  
|**GenerateNewIndex**|Создает новый индекс, но не сохраняет его.|  
|**ReuseExistingIndex**|Повторно использует уже существующий индекс.|  
  
### Поддержка таблицы индексов соответствия  
 Параметр **GenerateAndMaintainNewIndex** устанавливает триггеры на ссылочную таблицу для синхронизации ссылочной таблицы и таблицы индекса соответствия. Если необходимо удалить установленный триггер, нужно запустить хранимую процедуру **sp_FuzzyLookupTableMaintenanceUnInstall** и ввести в качестве входного параметра имя, определенное в свойстве MatchIndexName.  
  
 Нельзя удалять поддерживаемую таблицу индекса соответствия перед запуском хранимой процедуры **sp_FuzzyLookupTableMaintenanceUnInstall**. Если таблица индекса соответствия удалена, то триггеры в ссылочной таблице будут работать неправильно. Все последующие обновления ссылочной таблицы будут выдавать ошибку до тех пор, пока вручную не будут сброшены триггеры в ссылочной таблице.  
  
 Команда SQL TRUNCATE TABLE не запускает триггеры DELETE. Если ссылочная таблица была обработана командой TRUNCATE TABLE, то синхронизация между ссылочной таблицей и индексом соответствия нарушается и преобразование «Нечеткий уточняющий запрос» перестает работать. Если триггеры, поддерживающие таблицу индекса соответствия, установлены на ссылочную таблицу, необходимо использовать команду SQL DELETE вместо команды TRUNCATE TABLE.  
  
> [!NOTE]  
>  Если выбрать параметр **Поддерживать хранимый индекс** в **редакторе преобразования «Нечеткий уточняющий запрос»** на вкладке **Ссылочная таблица**, представление будет поддерживать хранимый индекс с помощью управляемых хранимых процедур. Эти управляемые хранимые процедуры используют функцию интеграции со средой CLR, доступную в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. По умолчанию в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] отключена интеграция со средой CLR. Чтобы использовать функцию **Поддерживать хранимый индекс** , необходимо включить интеграцию со средой CLR. Дополнительные сведения см. в статье [Enabling CLR Integration](../Topic/Enabling%20CLR%20Integration.md).  
>   
>  Поскольку для параметра **Поддерживать хранимый индекс** необходима интеграция со средой CLR, эта функция работает, только если ссылочная таблица выбрана на экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на котором включена интеграция со средой CLR.  
  
## Сравнение строк  
 При настройке преобразования «Нечеткий уточняющий запрос» можно определить алгоритм сравнения, который преобразование применяет для поиска записей в ссылочной таблице. Если свойству Exhaustive присвоено значение **True**, преобразование будет сравнивать каждую строку на входе с каждой строкой в ссылочной таблице. Этот алгоритм сравнения может дать более точные результаты, но, вероятнее всего, данное преобразование будет выполняться довольно долго в том случае, если число строк в ссылочной таблице велико. Если свойству Exhaustive присвоено значение **True**, то вся ссылочная таблица будет загружена в память. Чтобы избежать проблем с производительностью, желательно установить свойство Exhaustive в значение **True** только на время развертывания пакета.  
  
 Если свойство Exhaustive имеет значение **False**, преобразование "Нечеткий уточняющий запрос" возвращает только результаты, в которых есть, по крайней мере, один индексированный токен или подстрока (подстрока называется *q-gram*), похожая на входную запись. Для повышения эффективности уточняющих запросов в инвертированном индексе, используемом преобразованием «Нечеткий уточняющий запрос» для поиска совпадений, индексируется только подмножество токенов в каждой строке таблицы. Если входных данных мало, свойству Exhaustive можно задать значение **True**, чтобы среди результирующих совпадений были и те, для которых в таблице индексов нет похожих токенов.  
  
## Кэширование индексов и ссылочных таблиц  
 При настройке преобразования «Нечеткий уточняющий запрос» можно определить, будет ли преобразование производить частичное кэширование индексов и ссылочных таблиц перед началом работы. Если свойству WarmCaches присвоено значение **True**, то индексы и ссылочная таблица будут загружены в память. Когда на вход подается большое количество строк, присвоением свойству WarmCaches значения **True** можно добиться увеличения производительности преобразования. Когда на вход подается небольшое количество строк, присвоением свойству WarmCaches значения **False** можно ускорить процесс повторного использования больших индексов.  
  
## Временные таблицы и индексы  
 В процессе выполнения преобразование «Нечеткий уточняющий запрос» создает временные объекты, такие как таблицы и индексы в базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , с которой соединяется данное преобразование. Размер временных таблиц и индексов пропорционален числу строк и токенов в ссылочной таблице и числу токенов, которые создает преобразование «Нечеткий уточняющий запрос», поэтому они потенциально могут занимать существенный объем места на диске. Также преобразование выполняет запросы к этим временным таблицам. Поэтому необходимо учитывать то, что преобразование "Нечеткий уточняющий запрос" должно быть соединено с экземпляром базы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], который не связан с рабочим сервером, особенно если место на диске на рабочем сервере ограниченно.  
  
 Производительность этого преобразования может повышаться путем размещения используемых им таблиц и индексов на локальном компьютере. Если используемая преобразованием «Нечеткий уточняющий запрос» ссылочная таблица находится на рабочем сервере, необходимо рассмотреть возможность копирования таблицы на отладочный сервер и настройки доступа преобразования «Нечеткий уточняющий поиск» к этой копии. С помощью этого можно предотвратить использование ресурсов рабочего сервера запросами поиска. Кроме того, если преобразование "Нечеткий уточняющий запрос" поддерживает индекс соответствия, то есть если свойству MatchIndexOptionsis присвоено значение **GenerateAndMaintainNewIndex**, то преобразование может заблокировать ссылочную таблицу на время проведения операции по очистке данных и предотвратить доступ к ней других пользователей и приложений.  
  
## Настройка преобразования «Нечеткий уточняющий запрос»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно настроить при помощи диалогового окна **Редактор преобразования «Нечеткий уточняющий запрос»** , см. в следующих разделах:  
  
-   [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Ссылочная таблица")](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Столбцы")](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
-   [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Дополнительно")](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
 Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Связанные задачи  
 Дополнительные сведения о настройке свойств для компонента потока данных см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## См. также раздел  
 [Преобразование «Уточняющий запрос»](../../../integration-services/data-flow/transformations/lookup-transformation.md)   
 [Преобразование «Нечеткое группирование»](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Преобразования служб Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  