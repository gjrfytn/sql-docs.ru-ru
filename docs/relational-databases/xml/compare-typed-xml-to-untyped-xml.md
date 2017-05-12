---
title: "Сравнение типизированного и нетипизированного XML | Документация Майкрософт"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27533bcc63a8df64597db4529b16a26f1fb5a009
ms.lasthandoff: 04/11/2017

---
# <a name="compare-typed-xml-to-untyped-xml"></a>Сравнение типизированного и нетипизированного XML
  Можно создать переменные, параметры и столбцы типа **xml** . При необходимости можно связать коллекцию схем XML с переменной, параметром или столбцом типа **xml** . В данном случае экземпляр типа данных **xml** называется *типизированным*. В противном случае экземпляр XML называется *нетипизированным*.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>XML-документы правильного формата и тип данных XML  
 Тип данных **xml** соответствует типу данных **xml** стандарта ISO. Таким образом, он позволяет хранить синтаксически корректные документы XML 1.0, а также так называемые фрагменты XML-содержимого с текстовыми узлами и произвольным числом элементов верхнего уровня в нетипизированном XML-столбце. Система, осуществляющая проверку правильности формата данных, не требует, чтобы столбец был связан с XML-схемами, и отклоняет данные, имеющие неправильный формат в общепринятом смысле. Это также верно для нетипизированных переменных и параметров типа XML.  
  
## <a name="xml-schemas"></a>XML-схемы  
 XML-схема предоставляет следующее.  
  
-   **Ограничения проверки.** SQL Server проверяет типизированный экземпляр XML после каждой операции присвоения или изменения.  
  
-   **Сведения о типе данных.** Схемы предоставляют сведения о типах атрибутов и элементов в экземпляре типа данных **xml** . Сведения о типе позволяют более точно определить семантику операций над значениями, содержащимися в экземпляре, по сравнению с нетипизированным **xml**. Например, десятичные арифметические действия могут выполняться над десятичными значениями, но не могут выполняться над строками. По этой причине типизированное XML-хранилище может занимать значительно меньше места, чем нетипизированное.  
  
## <a name="choosing-typed-or-untyped-xml"></a>Выбор между типизированным и нетипизированным XML  
 В перечисленных ниже ситуациях следует использовать нетипизированный тип данных **xml** .  
  
-   Нет схемы XML-данных.  
  
-   Есть схемы, но нежелательно, чтобы сервер проверял данные. Это может иметь место в тех случаях, когда приложение перед сохранением данных на сервере проверяет их на стороне клиента или если приложение временно сохраняет XML-данные, которые не соответствуют схеме, или использует компоненты схемы, не поддерживаемые сервером.  
  
 В перечисленных ниже ситуациях следует использовать типизированный тип данных **xml** .  
  
-   есть схемы XML-данных и требуется, чтобы сервер проверял соответствие данных этим схемам;  
  
-   требуется оптимизировать хранение данных и обработку запросов на основе информации о типах;  
  
-   требуется в более полной мере использовать информацию о типах при компиляции запросов.  
  
 В типизированных XML-столбцах, параметрах и переменных можно хранить XML-документы или содержимое. Во время объявления необходимо указать при помощи флага, что хранится: документ или содержимое. Кроме того, необходимо предоставить системе коллекцию XML-схем. Укажите флаг DOCUMENT, если каждый экземпляр XML имеет ровно один элемент верхнего уровня. В противном случае укажите флаг CONTENT. Компилятор запросов использует флаг DOCUMENT при проверке типов во время компиляции запросов для определения одинарных элементов верхнего уровня.  
  
## <a name="creating-typed-xml"></a>Создание типизированного XML  
 Перед созданием типизированных переменных, параметров или столбцов **xml** сначала необходимо зарегистрировать коллекцию схем XML, как описано в разделе [CREATE XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/create-xml-schema-collection-transact-sql.md). Затем коллекцию схем XML можно связать с переменными, параметрами или столбцами типа **xml**.  
  
 В следующих примерах для указания имени коллекции XML-схем используется обозначение, состоящее из двух частей. Первая часть — это имя схемы, вторая часть — имя коллекции XML-схем.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>Пример. Связывание коллекции схем с переменными типа xml  
 В приведенном ниже примере создается переменная типа**xml** , с которой затем связывается коллекция схем. Коллекция схем, указанная в примере, уже импортирована в базу данных **AdventureWorks** .  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>Пример. Указание схемы для столбца типа xml  
 В приведенном ниже примере создается таблица со столбцом типа **xml** и указывается схема для этого столбца.  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>Пример. Передача параметра типа xml в хранимую процедуру  
 В приведенном ниже примере параметр типа **xml** передается хранимой процедуре и указывается схема для переменной.  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 Обратите внимание на следующие сведения о коллекции XML-схем.  
  
-   Коллекция схем XML доступна только в базе данных, в которой она была зарегистрирована с помощью [создания коллекции схем XML](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
-   При приведении строки к типизированному **xml** во время синтаксического анализа также выполняются проверка и типизация на основе пространств имен схем XML в указанной коллекции.  
  
-   Данные можно приводить из типизированного **xml** к нетипизированному **xml** и наоборот.  
  
 Дополнительные сведения о других способах формирования XML в SQL Server см. в разделе [Создание экземпляров XML-данных](../../relational-databases/xml/create-instances-of-xml-data.md). После формирования документ XML можно связать с переменной типа **xml** или сохранить в столбце типа **xml** для дополнительной обработки.  
  
 В иерархии типов данных данные **xml** отображаются ниже **sql_variant** и определенных пользователем типов, но выше всех встроенных типов.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>Пример. Указание аспектов для ограничения типизированного XML-столбца  
 На типизированные столбцы **xml** можно наложить ограничение, допускающее в них только отдельные элементы высшего уровня для каждого сохраненного в них экземпляра. , для указания дополнительного аспекта `DOCUMENT` при создании таблицы, как показано в следующем примере:  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 По умолчанию экземпляры, хранимые в типизированном столбце **xml** , сохраняются в виде содержимого XML, а не документов XML. Это позволяет использовать:  
  
-   ноль или несколько элементов верхнего уровня;  
  
-   текстовые узлы в элементах верхнего уровня.  
  
 Также можно явно указать данное поведение, добавив аспект `CONTENT` , как показано в следующем примере.  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 Обратите внимание, что дополнительные аспекты DOCUMENT/CONTENT можно указать везде, где определен тип **xml** (типизированный XML). Например, при создании типизированной переменной **xml** аспект DOCUMENT/CONTENT можно добавить следующим образом:  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>Определение типа документа (DTD)  
 Типизацию столбцов, переменных и параметров типа **xml** можно выполнять с использованием схемы XML, но без использования DTD. Однако и с нетипизированными, и с типизированными XML-данными можно использовать встроенное определение DTD для указания значений по умолчанию и замены ссылок на сущности их расширенными формами.  
  
 Можно преобразовывать определения DTD в документы схемы XML при помощи инструментов других компаний и загружать эти схемы XML в базу данных.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>Обновление типизированного XML с SQL Server 2005  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] содержит несколько расширений для поддержки схем XML, включая поддержку нестрогой проверки, улучшенную обработку данных экземпляров **xs:date**, **xs:time** и **xs:dateTime** . Кроме того, добавлена поддержка типов списков и объединений. В большинстве случаев эти изменения не влияют на вопросы обновления. Однако если в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] используется коллекция схем XML, допускающая значения типов **xs:date**, **xs:time**или **xs:dateTime** (или любых их подтипов), то при присоединении базы данных [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] к более поздней версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]потребуется выполнить указанные ниже шаги обновления.  
  
1.  Со всеми столбцами XML, введенными с коллекцией схем XML, в которой содержатся элементы или атрибуты, относящиеся к типам **xs:anyType**, **xs:anySimpleType**, **xs:date** или любым их подтипам, **xs:time** или любым его подтипам, **xs:dateTime** или любым его подтипам либо являющиеся объединениями или списками с элементами любых из перечисленных типов, происходит следующее:  
  
    1.  отключаются все XML-индексы столбца;  
  
    2.  все значения [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] продолжают отображаться в часовом поясе Z, поскольку они были нормализованы по часовому поясу Z;  
  
    3.  все значения **xs:date** или **xs:dateTime** , предшествующие дате "1 января 1 года", приведут к ошибке выполнения при перестроении индекса или применении инструкции XQuery или XML-DML к данным XML, содержащим такие значения;  
  
2.  все отрицательные значения года в аспектах **xs:date** или **xs:dateTime** или значения по умолчанию в коллекции схем XML автоматически обновляются до наименьшего значения, допустимого базовым типом **xs:date** или **xs:dateTime** (например, 0001-01-01T00:00:00.0000000Z для **xs:dateTime**).  
  
 Обратите внимание, что при помощи простой SQL-инструкции SELECT можно получить весь тип XML-данных, даже если в нем содержатся отрицательные значения года. Отрицательные значения года рекомендуется заменить значением года в обновленном поддерживаемом диапазоне; кроме того, можно изменить тип элемента или атрибута на **xs:string**.  
  
## <a name="see-also"></a>См. также:  
 [Создание экземпляров XML-данных](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Методы типа данных XML](../../t-sql/xml/xml-data-type-methods.md)   
 [Язык модификации XML-данных (XML DML)](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [Данные XML (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
  