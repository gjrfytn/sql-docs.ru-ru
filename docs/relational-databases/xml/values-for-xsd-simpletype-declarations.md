---
title: "Значения для объявлений &lt;xsd:simpleType&gt; | Документация Майкрософт"
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
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b5ba2b2137935919d420f2eab0349a26dc8d9c87
ms.lasthandoff: 04/11/2017

---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>Значения для объявлений &lt;xsd:simpleType>&gt;
  Следующая таблица выделяет ограничения, которые применяются, основываясь на всех распознанных простых перечислениях типа XSD.  
  
 Кроме того, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает использование значения NaN в объявлениях **\<xsd:simpleType>**. Схемы, включающие значения NaN, будут отклонены сервером.  
  
|Простой тип|Ограничение|  
|-----------------|----------------|  
|**duration**|Значение года должно задаваться в диапазоне от -2^31 до 2^31-1. Месяц, день, час, минута и секунда должны задаваться в диапазоне от 0 до 9999. Значение секунд имеет дополнительные три цифры точности справа от десятичной запятой.|  
|**dateTime**|Значение часа во вложенном поле часового пояса должно находиться в пределах принятого диапазона от -14 до +14. Значение года должно быть в диапазоне от 1 до 9999. Значение месяца должно быть в диапазоне от 1 до 12. Значение дня должно быть в пределах от 1 до 31 и быть допустимым календарным днем. Например, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вернет ошибку при обнаружении неверной даты, например 1974-02-31 (поскольку в феврале не может быть 31 день).<br /><br /> Второй компонент поддерживает точность до 10 наносекунд. Указание часового пояса является необязательным.<br /><br /> В SQL Server 2005 поддерживались годы в диапазоне от -9999 до 9999. Теперь SQL Server поддерживает более ограниченные диапазоны лет. Дополнительные сведения см. в статье [Сравнение типизированного и нетипизированного XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).|  
|**date**|Значение года должно быть в диапазоне от 1 до 9999. Значение месяца должно быть в диапазоне от 1 до 12. Значение дня должно быть в пределах от 1 до 31 и быть допустимым календарным днем. Например, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вернет ошибку при обнаружении неверной даты, например 1974-02-31 (поскольку в феврале не может быть 31 день).<br /><br /> В SQL Server 2005 поддерживались годы в диапазоне от -9999 до 9999. Теперь SQL Server поддерживает более ограниченные диапазоны лет. Дополнительные сведения см. в статье [Сравнение типизированного и нетипизированного XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).|  
|**gYearMonth**|Значение года должно быть в диапазоне от -9999 до 9999.|  
|**gYear**|Значение года должно быть в диапазоне от -9999 до 9999.|  
|**gMonthDay**|Значение месяца должно быть в диапазоне от 1 до 12. Значение дня должно задаваться в диапазоне от 1 до 31.|  
|**gDay**|Значение дня должно быть в диапазоне от 1 до 31.|  
|**gMonth**|Значение месяца должно быть в диапазоне от 1 до 12.|  
|**decimal**|Значения этого типа должны соответствовать формату числового типа SQL. Этот тип внутренне представляет поддержку чисел, имеющих до 38 десятичных разрядов, причем 10 из этих разрядов зарезервированы для точности в долях секунды.|  
|**float**|Значения этого типа должны соответствовать формату числового типа **real** языка SQL.|  
|**double**|Значения этого типа должны соответствовать формату числового типа **float** языка SQL.|  
|**строка**|Значения этого типа должны соответствовать формату числового типа SQL **nvarchar(max)** .|  
|**anyURI**|Значения этого типа не могут быть в длину больше, чем 4 000 символов Юникода.|  
  
## <a name="see-also"></a>См. также:  
 [Требования и ограничения для коллекций XML-схем на сервере](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  