---
title: "Автоматическое сопоставление синтаксических пар | Документация Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a86f4ede8645a7346234ab1bbfd3a45e3d01393a
ms.lasthandoff: 04/11/2017

---
# <a name="automatic-matching-of-syntax-pairs"></a>Автоматическое сопоставление синтаксических пар
  Автоматическая проверка соответствия синтаксических пар позволяет немедленно убедиться в том, что парные элементы синтаксиса в коде правильно объединены в пары. В редакторе запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] такая проверка называется «соответствием разделителей», в редакторе запросов XMLA служб Analysis Services — «соответствием фигурных скобок», а в редакторах многомерных выражений и расширений интеллектуального анализа данных — «соответствием круглых скобок».  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>Проверка соответствия разделителей в редакторе запросов к компоненту Database Engine  
 Редактор запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] проверяет соответствие разделителей, обозначающих границы блоков кода. Проверка соответствия осуществляется двумя способами.  
  
-   Редактор выделяет оба разделителя, составляющих пару, в момент ввода второго из них.  
  
-   Когда курсор мыши оказывается над одним из разделителей, составляющих пару, с помощью сочетания клавиш CTRL + ] можно переместиться ко второму разделителю.  
  
### <a name="delimiter-pairs"></a>Пары разделителей  
 Автоматическая проверка соответствия разделителей распознает следующие наборы разделителей.  
  
|Открывающий разделитель|Закрывающий разделитель|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 Автоматическая проверка соответствия разделителей не распознает разделители идентификаторов в скобках ([ObjectName]) или в кавычках ("ObjectName"). Проверка соответствия пар не сопоставляет одиночные кавычки-разделители для строковых литералов ('string'), поскольку выделение цветом само по себе обеспечивает визуальное отображение строкового значения.  
  
### <a name="delimiter-highlighting"></a>Выделение разделителей цветом  
 При проверке соответствия выделяются одновременно открывающий и закрывающий элемент пары разделителей. Это позволяет визуально отделить блоки кода и проверить наличие неполных пар.  
  
 Разделители выделяются при вводе последнего символа, завершающего пару. Например, когда после разделителя BEGIN вводится разделитель END, то выделение включается после ввода последней буквы в разделителе END. Чтобы включить выделение, не обязательно вводить сначала открывающий разделитель, а затем закрывающий. Если ввести сначала закрывающий разделитель END, пролистать скрипт назад и ввести открывающий разделитель BEGIN, то выделение будет включено после ввода последней буквы в разделителе BEGIN. Последняя набранная буква не обязательно должна быть последней буквой разделителя. Например, если открывающий разделитель был ошибочно введен как BEIN вместо BEGIN, то пара разделителей BEGIN END будет выделена при вставке буквы G.  
  
 Пара разделителей остается выделенной до тех пор, пока курсор мыши не будет перемещен в другое место. Выделение отключается при перемещении курсора мыши даже в том случае, если новое положение курсора находится в пределах того же разделителя. Выделение можно включить повторно, удалив и заново введя любую букву в любом из разделителей, составляющих пару.  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Проверка соответствия фигурных скобок в редакторе запросов XMLA служб Analysis Services  
 Проверка соответствия фигурных скобок в редакторе запросов XMLA позволяет убедиться в том, все ли элементы закрыты, с помощью выделения открывающих и закрывающих фигурных скобок. Можно также по сочетанию клавиш CTRL + ] перемещаться от одной фигурной скобки из пары ко второй.  
  
 Редактор запросов XMLA осуществляет проверку соответствия фигурных скобок для следующих элементов.  
  
-   Совпадающие открывающий и закрывающий теги.  
  
-   Любая пара угловых скобок "\<" и ">".  
  
-   Начало и конец комментария.  
  
-   Начало и конец инструкций по обработке.  
  
-   Начало и конец блока CDATA.  
  
-   Начало и конец DTD-декларации.  
  
-   Открывающие и закрывающие кавычки атрибутов.  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>Проверка соответствия круглых скобок в редакторах многомерных выражений и расширений интеллектуального анализа данных  
 Редакторы многомерных выражений и выражений интеллектуального анализа данных автоматически выполняют проверку соответствия пар круглых скобок в функциях.  
  
  