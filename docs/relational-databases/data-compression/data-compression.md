---
title: "Сжатие данных | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-compression
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- page compression [Database Engine]
- indexes [SQL Server], compressed
- compressed indexes [SQL Server]
- storage compression [Database Engine]
- tables [SQL Server], compressed
- storage [SQL Server], compressed
- compression [SQL Server]
- row compression [Database Engine]
- compression [SQL Server], about compressed tables and indexes
- data compression [Database Engine]
- compressed tables [SQL Server]
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 686f793e6579b54278a4d43e11e764efda84972e
ms.lasthandoff: 04/11/2017

---
# <a name="data-compression"></a>Data Compression
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] и [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] поддерживают сжатие строк и страниц для таблиц и индексов rowstore, а также поддерживают columnstore и архивное сжатие columnstore для таблиц и индексов columnstore.  
  
 Для таблиц и индексов rowstore используйте функцию сжатия данных, чтобы уменьшить размер базы данных. Помимо экономии места, сжатие данных позволяет повысить производительность при рабочих нагрузках с интенсивным вводом-выводом, поскольку данные хранятся в меньшем количестве страниц и в запросах требуется считывать меньше страниц с диска. Однако для сжатия и распаковки данных при обмене данными с приложениями требуются дополнительные ресурсы ЦП на сервере баз данных. Можно настроить сжатие строк и страниц для следующих объектов баз данных:  
  
-   Для полной таблицы, хранящейся в виде кучи.  
  
-   Для полной таблицы, хранящейся в виде кластеризованного индекса.  
  
-   Для полного некластеризованного индекса.  
  
-   Для полного некластеризованного представления.  
  
-   Для секционированных таблиц и индексов параметры сжатия можно задавать для каждой секции, и разные секции объекта могут иметь различные параметры.  
  
 Для таблиц и индексов columnstore все таблицы и индексы columnstore всегда используют сжатие columnstore, и этот режим не настраивается пользователем. Используйте архивное сжатие columnstore, чтобы еще больше сократить размер данных в случаях, когда можно предоставить дополнительное время и ресурсы ЦП для хранения и извлечения данных.  Можно настроить архивное сжатие columnstore для следующих объектов базы данных:  
  
-   Вся таблица columnstore или весь кластеризованный индекс columnstore.  Таблица columnstore хранится в виде кластеризованного индекса columnstore, поэтому оба подхода приносят одинаковые результаты.  
  
-   Весь некластеризованный индекс columnstore.  
  
-   Для секционированных таблиц columnstore и индексов columnstore можно задать параметр архивного сжатия для каждой секции, и разным секциям не обязательно назначать одинаковый параметр архивного сжатия.  
  
> [!NOTE]  
>  Данные могут быть сжаты с использованием формата алгоритма GZIP. Этот дополнительный шаг лучше всего подходит для сжатия фрагментов данных при архивации старых данных для долговременного хранения. Данные, сжатые с помощью этой функции COMPRESS, невозможно проиндексировать. Дополнительные сведения см. в статье [COMPRESS (Transact-SQL)](../../t-sql/functions/compress-transact-sql.md).  
  
## <a name="considerations-for-when-you-use-row-and-page-compression"></a>Замечания по использованию сжатия строк и страниц  
 При использовании сжатия строк и страниц следует учитывать следующее.  
  
-   Подробности сжатия данных могут меняться без предварительного уведомления в пакетах обновлений или в последующих версиях.

-   Сжатие доступно в [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]  
  
-   Сжатие поддерживается не во всех выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в разделе [Функции, поддерживаемые различными выпусками SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Для системных таблиц сжатие недоступно.  
  
-   С помощью сжатия можно хранить больше строк в странице, максимальный размер строки таблицы или индекса при этом не изменяется.  
  
-   Для таблицы нельзя включить сжатие, если сумма максимального размера строки и служебных данных сжатия превышает максимальный размер строки в 8060 байт. Например, таблица со столбцами c1**char(8000)** и c2**char(53)** не может быть сжата из-за дополнительного объема служебных данных. При использовании формата хранения vardecimal выполняется проверка размера строки (когда формат включен). При использовании сжатия строк и страниц проверка размера строки выполняется при первичном сжатии объекта, а также при всех последующих вставках и изменениях строк. При использовании сжатия обеспечивается выполнение следующих двух правил.  
  
    -   Обновление для типа с фиксированной длиной должно всегда завершаться успешно.  
  
    -   Отключение сжатия данных должно всегда выполняться успешно. Даже если сжатая строка умещается на странице (что означает, что она имеет размер меньше 8060 байт), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не допустит выполнения обновлений, которые не поместятся в строке без сжатия.  
  
-   Если указан список секций, для каждой отдельной секции можно установить тип сжатия ROW, PAGE или NONE. Если список секций не был указан, для всех секций устанавливается свойство сжатия данных, указанное в инструкции. При создании индекса или таблицы для свойства сжатия устанавливается значение NONE, если не было указано другое значение. При изменении таблицы сохраняется существующее сжатие, если не было указано иное.  
  
-   При указании списка секций или секции, выходящей за пределы диапазона, будет сформирована ошибка.  
  
-   Некластеризованные индексы не наследуют свойство сжатия таблицы. Чтобы сжать индексы, необходимо явно задать для них свойство сжатия. По умолчанию при создании индексов для них устанавливается режим сжатия NONE.  
  
-   При создании кластеризованного индекса в куче кластеризованный индекс наследует состояние сжатия кучи, если не указано другое состояние сжатия.  
  
-   Если для кучи было настроено сжатие уровня страницы, для страниц такое сжатие будет реализовываться только следующими методами.  
  
    -   Массовый импорт данных осуществляется со включенными массовыми оптимизациями.  
  
    -   Вставка данных с помощью синтаксиса INSERT INTO ... Синтаксис WITH (TABLOCK) и таблица не содержат некластеризованный индекс.  
  
    -   Перестройка таблицы с помощью инструкции ALTER TABLE ... REBUILD с параметром сжатия PAGE.  
  
-   В новых страницах, размещенных в куче в процессе выполнения операций DML, сжатие страниц не будет использоваться до тех пор, пока куча не будет перестроена. Перестройте кучу. Для этого удалите и повторно примените сжатие либо создайте и удалите кластеризованный индекс.  
  
-   Чтобы изменить параметры сжатия кучи, необходимо перестроить все некластеризованные индексы в таблице. Это обеспечивает наличие в них указателей на новые расположения в куче.  
  
-   Включить или отключить сжатие типа ROW или PAGE можно в оперативном или режиме вне  сети. Включение сжатия для кучи является однопоточным для операции в сети.  
  
-   Чтобы включить или отключить сжатие строки или страницы, необходимо столько же места на диске, как и для создания или перестройки индекса. Для секционированных данных объем пространства, необходимый для включения или отключения сжатия, можно сократить, выполняя включение или отключение сжатия последовательно для каждой секции.  
  
-   Чтобы определить состояние сжатия секций в секционированной таблице, выполните запрос столбца data_compression из представления каталога sys.partitions.  
  
-   При сжатии индексов страницы конечного уровня можно сжать как сжатием строк, так и сжатием страниц. Для страниц, расположенных не на конечном уровне, нельзя использовать сжатие страниц.  
  
-   Ввиду их размера, типы данных больших значений иногда хранятся отдельно от нормальных данных строк на страницах для особых целей. Сжатие данных недоступно для данных, хранящихся отдельно.  
  
-   Таблицы, для которых в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] был реализован формат хранения vardecimal, сохранят эту настройку и после обновления. К таблице, в которой присутствует формат хранения vardecimal, можно применить сжатие строк. Однако, поскольку сжатие строк является надмножеством формата хранения vardecimal, причин для сохранения данного формата нет. Для десятичных значений не происходит никакого дополнительного сжатия при сочетании формата хранения vardecimal и сжатия строк. Сжатие страниц можно применить к таблице, в которой присутствует формат хранения vardecimal, однако для столбцов данного формата дополнительного сжатия, скорее всего, не произойдет.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] поддерживает формат хранения vardecimal, однако сжатие на уровне строк достигает тех же целей, поэтому данный формат является устаревшим. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="using-columnstore-and-columnstore-archive-compression"></a>Использование Columnstore и архивного сжатия Columnstore  
  
||  
|-|  
|**Область применения**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (начиная с[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] до [текущей версии](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)].|  
  
### <a name="basics"></a>Основы  
 Таблицы и индексы Columnstore всегда сохраняются со сжатием columnstore. Можно еще более уменьшить размер данных columnstore, настроив дополнительное сжатие, именуемое архивным сжатием.  Чтобы выполнить архивное сжатие, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] применяет к данным алгоритм сжатия XPress корпорации Майкрософт. Добавьте или удалите архивное сжатие, используя следующие типы сжатия данных.  
  
-   Используйте сжатие данных **COLUMNSTORE_ARCHIVE** для сжатия данных columnstore с помощью архивного сжатия.  
  
-   Используйте сжатие данных **COLUMNSTORE** для распаковки архивного сжатия. Эти результирующие данные по-прежнему будут сжаты с использованием сжатия columnstore.  
  
 Чтобы добавить архивное сжатие, используйте команды [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) или [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) с параметром REBUILD и DATA COMPRESSION = COLUMNSTORE.  
  
 Примеры:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
  
```  
  
 Чтобы удалить архивное сжатие и восстановление данных для сжатия columnstилиe, используйте [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) или [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) с параметром REBUILD и DATA COMPRESSION = COLUMNSTORE.  
  
 Примеры:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
  
```  
  
 В следующем примере устанавливается сжатие данных columnstore в некоторых секциях и архивное сжатие columnstore в других секциях.  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### <a name="performance"></a>Производительность  
 Сжатие индексов columnstore с использованием архивного сжатия приводит к увеличению времени обработки индекса по сравнению с индексами columnstore, к которым не применяется архивное сжатие.  Используйте архивное сжатие только при наличии дополнительного времени и ресурсов ЦП для сжатия и получения данных.  
  
 При снижении производительности удается уменьшить объем хранилища, что полезно для данных, доступ к которым выполняется нечасто. Например, если имеется секция для данных за каждый месяц и основная часть активности пришлась на последние месяцы, то можно архивировать предыдущие месяцы, чтобы уменьшить требования к хранилищу.  
  
### <a name="metadata"></a>Метаданные  
 Следующие системные представления содержат сведения о сжатии данных для кластеризованных индексов.  
  
-   [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) — столбцы **type** и **type_desc** включают параметры CLUSTERED COLUMNSTORE и NONCLUSTERED COLUMNSTORE.  
  
-   [sys.partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) — столбцы **data_compression** и **data_compression_desc** включают параметры COLUMNSTORE и COLUMNSTORE_ARCHIVE.  
  
 Процедура [sp_estimate_data_compression_savings (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) не применяется к индексам columnstore.  
  
## <a name="how-compression-affects-partitioned-tables-and-indexes"></a>Влияние сжатия на секционированные таблицы и индексы  
 При использовании сжатия данных в секционированных таблицах или индексах следует учитывать следующее.  
  
-   При разбиении секций с помощью инструкции ALTER PARTITION обе секции наследуют атрибут сжатия данных исходной секции.  
  
-   При слиянии двух секций результирующая секция унаследует атрибут сжатия данных секции назначения.  
  
-   Для переключения секции свойство сжатия данных секции должно совпадать со свойством сжатия таблицы.  
  
-   Существуют две вариации синтаксиса, которые можно использовать для изменения сжатия секционированной таблицы или индекса.  
  
    -   Следующий синтаксис перестраивает только упоминаемую секцию:  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
  
    -   Следующий синтаксис перестраивает всю таблицу, используя существующий режим сжатия для всех неупоминаемых секций:  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     Для секционированных индексов действуют те же принципы, но используется инструкция ALTER INDEX.  
  
-   При удалении кластеризованного индекса соответствующие секции кучи сохраняют настройки сжатия данных, если только не была изменена схема секционирования. Если схема секционирования подверглась изменениям, все секции перестраиваются в распакованное состояние. Чтобы удалить кластеризованный индекс и изменить схему секционирования, необходимо выполнить следующие шаги.  
  
     1. Удалить кластеризованный индекс.  
  
     2. Изменить таблицу с помощью параметра REBUILD ... инструкции ALTER TABLE ..., в котором указывается режим сжатия.  
  
     Удаление кластеризованного индекса в режиме вне сети происходит очень быстро, поскольку удаляются только верхние уровни кластеризованных индексов. При удалении кластеризованного индекса в режиме в сети [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен перестроить кучу два раза — один для первого шага, один для второго.  
  
## <a name="how-compression-affects-replication"></a>Влияние сжатия на репликацию 
||  
|-|  
|**Область применения**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] до [текущей версии](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|   
 При использовании сжатия данных с репликацией следует учитывать следующее.  
  
-   Если агент моментальных снимков формирует первичный скрипт схемы, в новой схеме для таблицы и ее индексов будет использован один и тот же режим сжатия. Сжатие нельзя включить только для таблицы, но не для индекса.  
  
-   При репликации транзакций параметр схемы статьи определяет, какие из зависимых объектов или свойств должны быть добавлены в сценарий. Дополнительные сведения см. в разделе [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
     Агент распространителя не проверяет наличие подписчиков низкого уровня при применении скриптов. При выборе репликации сжатия создание таблицы у подписчиков низкого уровня завершится неудачно. При наличии смешанной топологии не следует включать репликацию сжатия.  
  
-   Для репликации слиянием уровень совместимости публикаций переопределяет параметры схемы и определяет, какие из объектов схемы будут внесены в сценарий.  
  
     При наличии смешанной топологии для уровня совместимости публикации следует установить значение версии подписчика низкого уровня, если поддержка новых параметров сжатия не является обязательной. Если поддержка необходима, после создания таблиц их сжатие следует осуществить на подписчике.  
  
 В следующей таблице показываются настройки репликации, управляющие сжатием в процессе репликации.  
  
|Намерение пользователя|Выполнить репликацию схемы секционирования для таблицы или индекса|Выполнить репликацию настроек сжатия|Действия со сценариями|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|Выполнить репликацию схемы секционирования и включить сжатие на подписчике для этой секции.|True|True|Создать скрипты для схемы секционирования и для настроек сжатия.|  
|Выполнить репликацию схемы секционирования, но не сжимать данные на подписчике.|True|False|Создать скрипт для схемы секционирования, но не создавать его для настроек сжатия секции.|  
|Не выполнять репликацию схемы секционирования и не сжимать данные на подписчике.|False|False|Не создавать скрипты для настроек секций или сжатия.|  
|Выполнить сжатие таблицы на подписчике при условии, что на издателе были сжаты все секции, но не выполнять репликацию схемы секционирования.|False|True|Проверить, что для всех секций включено сжатие.<br /><br /> Создать скрипт сжатия на уровне таблицы.|  
  
## <a name="how-compression-affects-other-sql-server-components"></a>Влияние сжатия на другие компоненты SQL Server 
||  
|-|  
|**Область применения**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] до [текущей версии](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|
   
 Сжатие происходит в подсистеме хранилища, и данные предоставляются большинству других компонентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в распакованном состоянии. Это ограничивает влияние сжатия на другие компоненты следующим.  
  
-   Операции массового импорта и экспорта  
  
     При экспорте данных, даже в собственном формате, данные выводятся в распакованном формате строк. Поэтому размер экспортированного файла данных может значительно превысить размер исходных данных.  
  
     При импорте данных, если для целевой таблицы было включено сжатие, данные будут преобразованы подсистемой хранилища в сжатый формат строк. По сравнению с импортом данных в распакованную таблицу такой импорт может потребовать больше ресурсов ЦП.  
  
     Если массовый импорт данных производится в кучу с включенным сжатием страниц, то при вставке данных операция массового импорта попытается применить к ним сжатие страниц.  
  
-   Сжатие не затрагивает резервное копирование и восстановление.  
  
-   Сжатие не затрагивает доставку журналов.  
  
-   Сжатие данных несовместимо с разреженными столбцами. Поэтому таблицы, содержащие разреженные столбцы, нельзя сжать, а разреженные столбцы нельзя добавить в сжатую таблицу.  
  
-   Включение сжатия может вызвать изменение планов запросов, поскольку данные будут занимать при хранении другое число страниц с другим числом строк на страницу.  
  
## <a name="see-also"></a>См. также:  
 [Реализация сжатия строк](../../relational-databases/data-compression/row-compression-implementation.md)   
 [Реализация сжатия страниц](../../relational-databases/data-compression/page-compression-implementation.md)   
 [Реализация сжатия Юникода](../../relational-databases/data-compression/unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION (Transact-SQL)](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

