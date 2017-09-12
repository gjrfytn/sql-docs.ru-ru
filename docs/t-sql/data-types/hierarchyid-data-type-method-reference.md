---
title: "HierarchyID (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>Справочник по методам типа данных HierarchyID
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**Hierarchyid** имеет тип данных переменной длины, системный тип данных. Используйте **hierarchyid** для представления позицию в иерархии. Столбец типа **hierarchyid** не принимает древовидную структуру автоматически. Приложение должно создать и назначить значения **hierarchyid** таким образом, чтобы они отражали требуемые связи между строками.
  
Значение типа данных **hierarchyid** представляет позицию в древовидной иерархии. Значения **hierarchyid** обладают следующими свойствами.
  
-   Исключительная компактность  
     Среднее число бит, необходимое для представления узла в древовидной структуре с *n* узлами, зависит от среднего количества потомков у узла. Для небольших уровней ветвления (0-7) размер равен примерно 6\*logA *n*  бит, где A — среднее ветвление. Для представления узла в иерархии организации, насчитывающей 100 000 человек со средним уровнем ветвления 6, необходимо около 38 бит. Эта величина округляется до 40 бит (5 байт), которые необходимы для хранения.  
-   Сравнение проводится в порядке приоритета глубины  
     Если заданы два значения **hierarchyid** — **a** и **b**, **a<b** означает, что значение a появляется раньше значения b, если проходить по дереву с приоритетным направлением в глубину. Индексы для типов данных **hierarchyid** располагаются в порядке приоритета глубины, а узлы, встречающиеся рядом при проходе по дереву с приоритетным направлением глубины, хранятся рядом друг с другом. Например, потомки некоторой записи хранятся рядом с этой записью. Дополнительные сведения см. в разделе [иерархических данных &#40; SQL Server &#41; ](../../relational-databases/hierarchical-data-sql-server.md).  
-   Поддержка произвольных вставок и удалений  
     С помощью метода [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) можно в любой момент создать одноуровневый элемент, расположенный справа от заданного узла, слева от заданного узла или между любыми двумя другими одноуровневыми элементами. Свойство сравнения сохраняется, если произвольное число узлов вставляется в иерархию или удаляется из нее. Большинство операций вставки и удаления сохраняют свойство компактности. Однако операции вставки между двумя узлами приводят к созданию значений hierarchyid, обладающих менее компактным представлением.  
-   Кодировка, используемая в **hierarchyid** типа ограничена 892 байтами. Следовательно, не может быть представлен узлы, имеющие слишком много уровней, чтобы уместиться в 892 байта **hierarchyid** типа.  
  
**Hierarchyid** тип доступен клиентам среды CLR в качестве **SqlHierarchyId** тип данных.
  
## <a name="remarks"></a>Замечания  
**Hierarchyid** тип логически кодирует сведения об одном узле в дереве иерархии, кодируя путь от корня дерева к узлу. Такой путь логически представлен в виде последовательности меток всех посещенных дочерних узлов, начиная с корня. Представление начинается косой чертой, а путь к корню представлен одной косой чертой. Для уровней ниже корня каждая метка кодируется в виде последовательности целых чисел, разделенных точками. Сравнения дочерних узлов выполняется путем сравнения этих целочисленных последовательностей, разделенных точками, в лексикографическом порядке. Уровни разделяются косой чертой. То есть косая черта отделяет родительский узел от дочернего. Например, допустимы следующие **hierarchyid** пути с длиной 1, 2, 2, 3 и 3 уровня соответственно:
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
Узлы можно вставлять в любое место. Узлы, вставленные после **/1/2/** перед вызовом **/1/3/** можно представить в виде **/1/2.5/**. Узлы, вставленные после 0, логически представлены в виде отрицательных чисел. Например, узел, который предшествует **/1/1/** можно представить в виде **/1/1 /**. Узлы не должны начинаться с нулей. Например **/1/1.1/** является допустимым, но **/1/1.01/** является недопустимым. Чтобы избежать ошибок, вставляйте узлы с помощью [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) метод.
  
## <a name="data-type-conversion"></a>Преобразование типов данных
**Hierarchyid** тип данных может быть преобразован в другие типы данных следующим образом:
-   Используйте [ToString()](../../t-sql/data-types/tostring-database-engine.md) метод преобразования **hierarchyid** значение в логическое представление **nvarchar(4000)** тип данных.  
-   Используйте [чтения ()](../../t-sql/data-types/read-database-engine.md) и [Write ()](../../t-sql/data-types/write-database-engine.md) для преобразования **hierarchyid** для **varbinary**.  
-   Для передачи **hierarchyid** параметры с помощью SOAP сначала преобразовать их в строки.  
  
## <a name="upgrading-databases"></a>Обновление баз данных
При обновлении базы данных до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], новую сборку и **hierarchyid** будет автоматически установлен тип данных. Помощник по обновлению обнаружит все пользовательские типы данных или сборки с конфликтующими именами. Помощник по обновлению посоветует переименовать все конфликтующие сборки и либо переименовать все конфликтующие типы данных, либо использовать в программном коде двухкомпонентные имена для ссылок на существующие определяемые пользователем типы данных.
  
Если при обновлении базы данных обнаружится пользовательская сборка с конфликтующим именем, эта сборка автоматически переименуется, а база данных переведется в подозрительный режим.
  
Если во время обновления обнаруживается пользовательский тип данных с конфликтующим именем, никаких специальных шагов не предпринимается. После обновления будут существовать как старый пользовательский тип, так и новый системный тип данных. Пользовательский тип данных будет доступен только с применением двухкомпонентных имен.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>Использование столбцов типа данных hierarchyid в реплицированных таблицах
Столбцы типа **hierarchyid** может использоваться во всех реплицированных таблицах. Требования к приложению ограничиваются способом репликации, однонаправленным или двунаправленным, и версией [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
### <a name="one-directional-replication"></a>Однонаправленная репликация
Однонаправленная репликация включает репликацию моментальных снимков, репликацию транзакций и репликацию слиянием, в которой изменения не выполняются на подписчике. Как **hierachyid** столбцы работать с одним однонаправленной репликации зависит от версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на подписчике.
-   Объект [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] издатель может реплицировать **hierachyid** столбцы для [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] подписчика без дополнительных условий.  
-   Объект [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] издателя, необходимо преобразовать **hierarchyid** столбцы, чтобы реплицировать их на подписчик, на котором выполняется [!INCLUDE[ssEW](../../includes/ssew-md.md)] или более ранней версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)]и более ранних версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживают **hierarchyid** столбцов. При использовании одной из этих версий все равно можно реплицировать данные на подписчик. Для этого следует установить параметр схемы или уровень совместимости репликации (для репликации слиянием), чтобы столбец можно было преобразовать в совместимый тип данных.  
  
Фильтрация столбцов поддерживается в обоих случаях. Это производится фильтрация **hierarchyid** столбцов. Фильтрация строк поддерживается до тех пор, пока фильтр не поддерживает **hierarchyid** столбца.
  
### <a name="bi-directional-replication"></a>Двунаправленная репликация
Двунаправленная репликация включает репликацию транзакций с обновляемыми подписками, одноранговую репликацию транзакций и репликацию слиянием, при которых изменения выполняются на подписчике. Репликация позволяет настраивать таблицу со **hierarchyid** столбцы для двунаправленной репликации. Обратите внимание на следующие требования и рекомендации.
-   На издателе и подписчике должен работать [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
-   Репликация реплицирует данные в виде байтов, не выполняя проверки целостности иерархии.  
-   Иерархия изменений источника (на подписчике или издателе) не поддерживается при репликации этих изменений.  
-   Значения хэша для **hierarchyid** столбцы являются специфичными для базы данных, в которой они создаются. Поэтому на подписчике и издателе могут создаваться одинаковые значения, но применяются они к разным строкам. Репликация не проверяет это условие, и никак не встроенных в секцию **hierarchyid** значений в столбце имеется для столбцов ИДЕНТИФИКАТОРОВ. Чтобы избежать подобных необнаруживаемых конфликтов, приложения должны использовать ограничения или другие механизмы проверки.  
-   Возможно, что строки, вставленные на подписчике, окажутся потерянными. Родительскую строку на издателе могут удалить. Это приводит к необнаруживаемому конфликту, если строка из подписчика вставляется на издателе.  
-   Фильтры столбцов не могут отфильтровывать не допускающим **hierarchyid** столбцы: вставка из подписчика завершится ошибкой, так как нет значения по умолчанию для **hierarchyid** столбца на издателе.  
-   Фильтрация строк поддерживается до тех пор, пока фильтр не поддерживает **hierarchyid** столбца.  
  
## <a name="see-also"></a>См. также:
[Иерархические данные (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[Справочник по методам типа данных hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
