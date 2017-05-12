---
title: "Использование вложенных запросов FOR XML | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], nested FOR XML
- nested FOR XML queries
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: af44fc3250f620dcaad219e67b0e414cd76974a7
ms.lasthandoff: 04/11/2017

---
# <a name="use-nested-for-xml-queries"></a>Использование вложенных запросов FOR XML
  Тип данных **xml** и директива [TYPE в запросах FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md) позволяют обрабатывать XML-документы, возвращаемые запросами FOR XML, как на сервере, так и на клиенте.  
  
## <a name="processing-with-xml-type-variables"></a>Обработка переменных типа XML  
 Результат запроса FOR XML можно присвоить переменной типа **xml** или воспользоваться языком XQuery, чтобы выполнить к нему запрос, после чего и присвоить полученный результат переменной типа **xml** для дополнительной обработки.  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 XML-данные, возвращаемые в переменной `@x`, можно дополнительно обработать с применением методов типа данных **xml** . Например, с помощью метода `ProductModelID` value() [можно получить значение атрибута](../../t-sql/xml/value-method-xml-data-type.md).  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 В следующем примере результат запроса `FOR XML` возвращается в виде типа данных **xml** , так как в предложении `TYPE` указана директива `FOR XML` .  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 Результат:  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 Поскольку результат имеет тип **xml** , непосредственно к нему можно применить один из методов типа данных **xml** , как показано в следующем запросе. В запросе [метод query() (тип данных xml)](../../t-sql/xml/query-method-xml-data-type.md) используется для получения первого дочернего элемента <`row`> элемента <`myRoot`>.  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 Результат:  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## <a name="returning-inner-for-xml-query-results-to-outer-queries-as-xml-type-instances"></a>Передача результатов внутреннего запроса FOR XML внешним запросам в виде экземпляров типа xml  
 Можно создать вложенные запросы `FOR XML` , в которых результат внутреннего запроса возвращает внешнему запросу данные типа **xml** . Например:  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 Обратите внимание на следующие данные из предыдущего запроса:  
  
-   XML-данные, сформированные внутренним запросом `FOR XML` , добавляются к XML-результату внешнего запроса `FOR XML`.  
  
-   Во внутреннем запросе указана директива `TYPE` . Таким образом, возвращаемые внутренним запросом XML-данные имеют тип **xml** . Если директива TYPE не указана, внутренний запрос `FOR XML` возвращает результат типа **nvarchar(max)** и XML-данные преобразуются в сущности.  
  
## <a name="controlling-the-shape-of-resulting-xml-data"></a>Управление формой результирующих XML-данных  
 Вложенные запросы FOR XML предоставляют больше возможностей управления формой результирующих XML-данных. При помощи вложенных запросов FOR XML можно конструировать XML-данные, сочетающие в себе атрибутивную и элементную модели.  
  
 Дополнительные сведения об указании атрибутивного и элементного XML с помощью вложенных запросов FOR XML см. в разделах [Сравнение запросов FOR XML и вложенных запросов FOR XML](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md) и [Формирование XML-кода с вложенными запросами FOR XML](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md).  
  
 С помощью вложенных запросов FOR XML в режиме AUTO можно формировать XML-иерархии, содержащие одноуровневые элементы. Дополнительные сведения см. в разделе [Формирование одноуровневых элементов с помощью вложенного запроса в режиме AUTO](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md).  
  
 Независимо от используемого режима вложенные запросы FOR XML предоставляют больший контроль при описании формата результирующих XML-данных. Их можно использовать вместо запросов в режиме EXPLICIT.  
  
## <a name="examples"></a>Примеры  
 В следующих разделах содержатся примеры использования запросов FOR XML.  
  
 [Сравнение запросов FOR XML и вложенных запросов FOR XML](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 Сравнение одноуровневого запроса FOR XML с вложенным запросом FOR XML. Данный пример включает в себя демонстрацию того, как для результата запросов можно указать и атрибутивную, и элементную модели XML.  
  
 [Формирование одноуровневых элементов с помощью вложенного запроса в режиме AUTO](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 Демонстрирует создание одноуровневых элементов с помощью вложенного запроса в режиме AUTO.  
  
 [Использование вложенных запросов FOR XML в ASP.NET](../../relational-databases/xml/use-nested-for-xml-queries-in-asp-net.md)  
 Демонстрирует использование предложения FOR XML в приложении ASPX с целью возврата XML-документа из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Формирование XML-кода с вложенными запросами FOR XML](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)  
 Показывает применение вложенных запросов FOR XML для управления структурой XML-документов, создаваемых [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  