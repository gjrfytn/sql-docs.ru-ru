---
title: Создание определяемых пользователем иерархий | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c35749671caabd8c6c61249d39bb3336257b1b8a
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242492"
---
# <a name="create-user-defined-hierarchies"></a>Создание пользовательских иерархий
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lets you create user-defined hierarchies. A hierarchy is a colпозволяют создавать пользовательские иерархии.rИерархия — это набор уровней на основе атрибутов.,Например, иерархия, связанная со временем, может содержать такие уровни, как «Год», «Месяц» и «День».hВ некоторых иерархиях каждый атрибут однозначно задает атрибут родительского элемента.rТакую иерархию иногда называют естественной.iКонечные пользователи могут использовать иерархии для просмотра данных в кубе. Иерархии задаются с помощью панели «Иерархии» конструктора измерений в среде разработки [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Вновь созданная пользовательская иерархия может оказаться *неровной*. Неровная иерархия — это иерархия, в которой по крайней мере у одного элемента логический родительский элемент не находится ровно на один уровень выше самого элемента. Существуют настройки, управляющие видимостью недостающих элементов в неровных иерархиях и способом их отображения. Дополнительные сведения об иерархиях см. в разделе [Неоднородные иерархии](user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Дополнительные сведения о проблемах производительности, связанных с конструированием и настройкой пользовательских иерархий, см. в [руководстве по производительности служб SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="see-also"></a>См. также  
 [Свойства пользовательской иерархии](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Свойства уровня &#91;занятого&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [«Родители потомки»](parent-child-dimension.md)  
  
  
