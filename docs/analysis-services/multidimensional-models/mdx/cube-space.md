---
title: "Пространство куба | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
caps.latest.revision: 6
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 6
---
# Пространство куба
  Пространство куба — это совокупность элементов иерархий атрибутов куба с мерами куба. Поэтому пространство куба определяется комбинаторным сочетанием всех элементов иерархии атрибута в кубе и мер куба и определяет максимальный размер куба. Важно иметь ввиду, что это пространство включает все возможные сочетания элементов иерархии атрибута, даже сочетания, которые могут показаться невозможными в реальном мире, например сочетания, где городом является Париж, а странами — Англия, Испания, Япония или Индия, и т. д.  
  
## Автоматическая проверка существования и пространство куба  
 Понятие *автоматическая проверка существования* ограничивает пространство куба ячейками, которые действительно существуют. Элементы иерархии атрибута в измерении могут не существовать с элементами другой иерархии атрибута в том же измерении.  
  
 Например, пространство куба, содержащего иерархию атрибута City, иерархию атрибута Country и меру Internet Sales Amount, включает только те элементы, которые существуют друг с другом. Например, если иерархия атрибута «City» содержит элементы «New York», «London», «Paris», «Tokyo» и «Melbourne», а иерархия атрибута «Country» содержит страны «United States», «United Kingdom», «France», «Japan» и «Australia», то пространство куба не содержит ячейку на пересечении элементов «Paris» и «United States».  
  
 Запрос к несуществующим ячейкам возвращает значение NULL, то есть они не могут содержать вычисления и нельзя определить вычисления, записывающие данные в это место пространства. Например, следующая инструкция включает в себя несуществующие ячейки.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  В следующем запросе применяется функция [Members (Set) (многомерные выражения)](../../../mdx/members-set-mdx.md) для получения набора элементов иерархии атрибута Gender по оси столбцов и выполняется перекрестное соединение этого набора с заданным набором элементов из иерархии атрибута Customer по оси строк.  
  
 При выполнении предыдущего запроса ячейка на пересечении элементов [Aaron A. Allen] и [Female] отображает значение NULL. Аналогично, значение NULL отображается в ячейке на пересечении элементов [Abigail Clark] и [Male]. Эти ячейки не существуют и не могут содержать значение, но запрос может вернуть несуществующие ячейки.  
  
 При использовании функции [Crossjoin (многомерные выражения)](../../../mdx/crossjoin-mdx.md) для получения перекрестного произведения элементов иерархий атрибутов из иерархий атрибутов одного измерения автоматическое существование ограничивает возвращаемые кортежи набором действительно существующих кортежей, а не возвращает все декартово произведение. Выполните следующий запрос и изучите его результаты.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Обратите внимание, что 0 используется для обозначения оси столбцов, это сокращение для оси(0), являющейся осью столбцов.  
  
 В предыдущем запросе возвращаются только ячейки для элементов каждой иерархии атрибута в запросе, которые существуют друг с другом. Предыдущий запрос можно записать, используя новую версию функции — [* (Crossjoin) (многомерные выражения)](../../../mdx/crossjoin-mdx.md).  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 Предыдущий запрос можно переписать следующим образом:  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 Значения ячеек будут совпадать, хотя метаданные в результирующем наборе будут разными. Например, в предыдущем запросе иерархия Country перемещена на ось среза (в предложении WHERE) и поэтому не представлена явно в результирующем наборе.  
  
 Каждый из перечисленных запросов демонстрирует поведение функции автоматического существования в службах [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## Пользовательские иерархии и пространство куба  
 В предыдущих примерах этого раздела позиции внутри пространства куба определялись с помощью иерархий атрибутов. Позицию в пространстве куба можно также определить с помощью пользовательских иерархий, определенных на основе иерархий атрибутов в измерении. Пользовательской называется иерархия иерархий атрибутов, сконструированная для упрощения обзора данных в кубе.  
  
 Например, запрос **CROSSJOIN** в предыдущем разделе можно переписать следующим образом:  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 В предыдущем запросе пользовательская иерархия Customer Geography в измерении Customer используется для определения позиции в пространстве куба, которая ранее определялась с помощью иерархии атрибута. С помощью иерархий атрибутов и пользовательских иерархий можно определить одинаковую позицию в пространстве куба.  
  
##  <a name="AttribRelationships"></a> Связи атрибутов и пространство куба  
 Определение связи атрибутов между связанными атрибутами увеличивает производительность запросов (облегчая создание соответствующих статистических обработок) и влияет на элемент связанной иерархии атрибута, который появляется с элементом иерархии атрибута. Например, если определяется кортеж, содержащий элемент из иерархии атрибута City, и в кортеже не определен явно элемент иерархии атрибута Country, можно предположить, что элементом иерархии атрибута Country по умолчанию будет связанный элемент иерархии атрибута Country. Тем не менее, это действительно так, только если определена связь атрибутов между иерархиями атрибутов City и Country.  
  
 В следующем примере возвращается элемент из иерархии связанных атрибутов, который не включен явно в запрос.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Обратите внимание, что для создания вычисляемого элемента в запросе используется ключевое слово **WITH** с функциями [CurrentMember (многомерные выражения)](../../../mdx/currentmember-mdx.md) и [Name (многомерные выражения)](../../../mdx/name-mdx.md). Дополнительные сведения см. в разделе [Базовый запрос многомерных выражений (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-query-mdx.md).  
  
 В предыдущем запросе возвращалось имя элемента иерархии атрибута Country, связанного с каждым элементом иерархии атрибута State. Возвращается ожидаемый элемент Country (поскольку определена связь атрибутов City и Country). Тем не менее, если в этом измерении не определена связь атрибутов между иерархиями атрибутов, возвращается элемент «(Все)», как продемонстрировано в следующем запросе.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 В предыдущем запросе возвращается элемент «(Все)» ("All Customers"), поскольку связь между атрибутами Education и City не определена. Таким образом, элемент «(Все)» иерархии атрибута Education будет ее элементом по умолчанию, используемым в любом кортеже, где участвует иерархия атрибута City, в которой элемент Education явно не указан.  
  
## Контекст вычисления  
  
## См. также  
 [Основные понятия многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Кортежи](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Автоматическая проверка существования](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Работа с элементами, кортежами и наборами (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Визуальные и невизуальные итоги](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [Справочник по языку многомерных выражений (многомерные выражения)](../../../mdx/mdx-language-reference-mdx.md)   
 [Справочник по многомерным выражениям (многомерные выражения)](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  