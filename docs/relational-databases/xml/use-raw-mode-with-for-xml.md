---
title: "Использование режима RAW для FOR XML | Документация Майкрософт"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4dc589a00b05bfcd7f3e414f7580014b4e0654f2
ms.lasthandoff: 04/11/2017

---
# <a name="use-raw-mode-with-for-xml"></a>Использование с RAW Mode для FOR XML
  Режим RAW преобразует каждую строку из результирующего набора запроса в элемент XML и присваивает ему универсальный идентификатор \<row> или необязательное имя элемента. По умолчанию каждое значение столбца в наборе строк, отличное от NULL, сопоставляется с определенным атрибутом элемента \<row>. Если директива ELEMENTS добавляется в предложение FOR XML, то каждому значению столбца сопоставляется дочерний элемент элемента \<row>. Вместе с директивой ELEMENTS можно дополнительно определить параметр XSINIL для сопоставления значений NULL столбца в результирующем наборе с элементом, обладающим атрибутом xsi:nil=`"`true`"`.  
  
 Есть возможность сделать запрос схемы итогового XML. При определении параметра XMLDATA возвращается встроенная схема XDR. При задании параметра XMLSCHEMA возвращается встроенная XSD-схема. Схема появляется в начале данных. В итоге ссылка на пространство имен схемы будет повторяться для каждого элемента высшего уровня.  
  
 Параметр BINARY BASE64 необходимо определить в предложении FOR XML для возвращения двоичных данных в base64-кодированном формате. В режиме RAW извлечение двоичных данных без определения параметра BINARY BASE64 приводит к ошибке.  
  
## <a name="in-this-section"></a>В этом разделе  
 Этот раздел содержит следующие примеры.  
  
-   [Пример. Получение сведений о модели продукта в формате XML](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [Пример. Указание XSINIL с директивой ELEMENTS](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [Пример: запросы к схемам как к результатам с помощью параметров XMLDATA и XMLSCHEMA](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [Пример. Получение двоичных данных](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [Пример. Переименование элемента &#60;row&#62;](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [Пример. Задание корневого элемента для XML-документа, сформированного предложением FOR XML](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [Пример. Запросы к столбцам XMLType](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>См. также:  
 [Добавление пространств имен в запросы с WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Использование режима AUTO совместно с FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [Использование с EXPLICIT Mode для FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [Использование с PATH Mode для FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)  
  
  