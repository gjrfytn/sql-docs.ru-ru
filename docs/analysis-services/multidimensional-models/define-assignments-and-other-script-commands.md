---
title: "Определение назначений и других команд скриптов | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "пустые скрипты [службы Analysis Services]"
  - "вычисления [службы Analysis Services], скрипты"
  - "многомерные выражения [службы Analysis Services], скрипты"
  - "скрипты [службы Analysis Services], вычисления"
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Определение назначений и других команд скриптов
  На вкладке **Вычисления** конструктора кубов щелкните значок **Создать команду скрипта** на панели инструментов для создания пустого скрипта. После создания новый скрипт отображается с пустым именем на панели **Организатор скриптов** на вкладке «Вычисления». Символы, вводимые на панели «Выражения вычисления», отображаются как имя элемента на панели **Организатор скриптов**. Следовательно, можно в первую строку ввести имя с комментарием для упрощения определения скрипта на панели **Организатор скриптов** . Дополнительные сведения см. в разделе [Введение в сценарии многомерных выражений в Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Дополнительные сведения о производительности запросов многомерных выражений и вычислений см. в разделе «Написание эффективных многомерных выражений» [Руководства по производительности служб SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
> [!IMPORTANT]  
>  Затем перейдите на вкладку **Вычисления** конструктора кубов, на панели **Организатор скриптов** содержится один скрипт с командой CALCULATE. Команда CALCULATE управляет статистическим вычислением ячеек куба, ее следует изменять только в том случае, если планируется вручную определять статистическое вычисление ячеек куба.  
  
 Для создания выражений с синтаксисом многомерных выражений можно использовать панель «Выражения вычисления». При создании выражения с панели **Средства вычисления** можно перетаскивать или копировать компоненты куба, функции и шаблоны на панель «Выражения вычисления». При этом скрипт добавляется для элемента на панели «Выражения вычисления» в то место, куда элемент перемещается или вставляется. Замените аргументы и их разделители (« и ») соответствующими значениями.  
  
> [!IMPORTANT]  
>  При написании выражения, содержащего несколько инструкций, с помощью панели «Выражения вычисления» убедитесь, что все строки скрипта многомерных выражений, за исключением последней, заканчиваются точкой с запятой (;). Вычисления объединяются в отдельный скрипт многомерных выражений, и к каждому скрипту добавляется точка с запятой. Если добавить точку с запятой к последней строке скрипта на панели «Вычисления выражения», то куб будет создан и развернут правильно, но к нему нельзя будет применять запросы.  
  
## См. также  
 [Вычисления в многомерных моделях](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  