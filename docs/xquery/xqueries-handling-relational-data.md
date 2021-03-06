---
title: Запросы XQuery, обработку реляционным данным | Документация Майкрософт
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- relational data [XQuery]
- XQuery, relational data
ms.assetid: 9812b71a-52ec-48a0-92f3-016a93660229
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9aa8b150a26e64d4a61efe80ab635110e540af33
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291023"
---
# <a name="xqueries-handling-relational-data"></a>Запросы XQuery, обрабатывающие реляционные данные
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Задать запрос XQuery для **xml** столбце или переменной с помощью одного из типа [методов типа данных XML](../t-sql/xml/xml-data-type-methods.md). К ним относятся **query()**, **value()**, **exist()**, или **modify()**. Запрос XQuery выполняется для экземпляра XML, указанного в запросе, создающем XML-код.  
  
 XML-код, созданный в результате выполнения запроса XQuery, может включать значения, полученные от других переменных Transact-SQL или столбцов набора строк. Для связи реляционных данных в формате, отличном от XML, с итоговым XML-кодом в SQL Server в форме расширений XQuery реализованы следующие псевдофункции:  
  
-   **SQL: column()** функции  
  
-   **SQL: variable()** функции  
  
 Можно использовать эти расширения XQuery при указании запроса XQuery в **query()** метод **xml** тип данных. В результате **query()** метод может создать XML, в котором объединяются данные из XML и не-**xml** типов данных.  
  
 Можно также использовать эти функции, при использовании **xml** методов типа данных **modify()**, **value()**, **query()**, и  **exist()** для получения реляционного значения внутри XML.  
  
 Дополнительные сведения см. в разделе [функция SQL: column() (XQuery)](../xquery/xquery-extension-functions-sql-column.md) и [функции SQL: variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="see-also"></a>См. также  
 [Данные XML (SQL Server)](../relational-databases/xml/xml-data-sql-server.md)   
 [Справочник по языку XQuery (SQL Server)](../xquery/xquery-language-reference-sql-server.md)   
 [Построение XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
