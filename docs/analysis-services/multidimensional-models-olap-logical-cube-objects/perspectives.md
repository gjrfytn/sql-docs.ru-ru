---
title: Перспективы | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d093d3991c41f35c16742c80e279754a1d650827
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027341"
---
# <a name="perspectives"></a>Перспективы
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Перспективой называется определение, позволяющее пользователям рассматривать куб с помощью более простого способа. Перспектива — это подмножество средств куба. Перспектива позволяет администраторам создавать представление куба и помогает пользователям сосредоточиться на данных, имеющих для них наибольшую значимость. Перспектива содержит подмножества множества всех объектов куба. Перспектива не может включать элементы, которые не определены в родительском кубе.  
  
 Простой объект <xref:Microsoft.AnalysisServices.Perspective> состоит из основной информации, измерений, групп мер, вычислений, ключевых показателей эффективности и действий. Основная информация включает имя и меру перспективы по умолчанию. Измерения — это подмножество измерений куба. Группы мер — это подмножество групп мер куба. Вычисления — это подмножество вычислений куба. Ключевые показатели эффективности представляют собой подмножество ключевых показателей производительности куба. Действия — это подмножество действий куба.  
  
 Вначале должны быть проведены обновление и обработка куба, и только после этого появляется возможность использовать перспективу.  
  
 Кубы могут быть очень сложные объекты для исследования в [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Один куб может представлять содержимое целого хранилища данных, при этом несколько групп мер в кубе будут представлять несколько таблиц фактов и несколько измерений, основанных на нескольких таблицах измерений. Такой куб представляет собой очень сложную конструкцию с высокоразвитой структурой, что может отпугнуть пользователей, которым для удовлетворения своих запросов в области бизнес-аналитики и отчетности зачастую необходимо взаимодействовать только с небольшой частью куба.  
  
 В [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], можно использовать перспективу для упрощения восприятия куба в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Перспектива определяет просматриваемое подмножество куба, которое предоставляет точки зрения на данные куба, учитывающие особенности предприятия и приложения. Перспектива контролирует видимость объектов, содержащихся в кубе. В перспективе можно отображать или скрывать следующие объекты:  
  
-   Измерения  
  
-   Атрибуты  
  
-   Иерархии  
  
-   Группы мер  
  
-   меры  
  
-   Ключевые показатели эффективности  
  
-   Вычисления (вычисляемые элементы, именованные наборы и команды скриптов)  
  
-   Действия  
  
 Например **Adventure Works** кубе [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] пример [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] база данных содержит одиннадцать групп мер и двадцать одно различное измерение куба, представляющая продажи, прогнозы продаж и финансовые данные. Клиентское приложение может напрямую указывать весь куб, но такая точка зрения может быть перегружена для пользователя, пытающегося извлечь основные сведения о прогнозах продаж. Вместо этого можно использовать тот же пользователь **цели продаж** перспективы, чтобы ограничить представление **Adventure Works** куба объектами, относящимися к прогнозированию продаж.  
  
 Даже те объекты куба, которые не видны пользователю в перспективе, могут быть указаны напрямую и извлечены с помощью инструкций XML для аналитики, многомерных выражений или расширений интеллектуального анализа данных. Перспективы не ограничивают доступ к объектам в кубе и не должны использоваться с такой целью. Перспективы используются для улучшения качества работы пользователя с кубом.  
  
 Перспектива является представлением куба в режиме только для чтения. Перспективу нельзя использовать для переименования или изменения объектов в кубе. Также с помощью перспективы нельзя изменить поведение или возможности куба, например использование визуальных итогов.  
  
## <a name="security"></a>безопасность  
 Перспективы предназначены для использования не в качестве механизма обеспечения безопасности, а как средство улучшения качества работы пользователя в приложениях бизнес-аналитики. Все параметры безопасности перспективы наследуются из базового куба. Например, перспективы не могут обеспечить доступ к объектам куба, к которым пользователь еще не имеет доступа. Безопасность куба должна быть разрешена прежде, чем будет предоставлен доступ к объектам в кубе через перспективу.  
  
  
