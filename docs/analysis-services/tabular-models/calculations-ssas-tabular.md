---
title: Вычисления в табличных моделях служб Analysis Services | Документация Майкрософт
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 53455f542e10e816aa55272026a875cf3cf87107
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2018
ms.locfileid: "52984075"
---
# <a name="calculations-in-tabular-models"></a>Вычисления в табличных моделях
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  После импорта данных в модель можно добавить вычисления для агрегации, фильтрации, расширения, объединения и защиты этих данных. В табличных моделях используется язык выражений анализа данных (DAX) — новый язык формул для создания пользовательских вычислений. В табличных моделях вычисления, которые можно создать с помощью формул DAX, используются в *вычисляемых столбцах*, *мерах*и *фильтрах строк*.  
  
## <a name="in-this-section"></a>В этом разделе  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Основные сведения о DAX в табличных моделях](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Описывает язык формул выражений анализа данных (DAX), используемый для создания вычислений для вычисляемых столбцов, мер и фильтров строк в табличных моделях.|  
|[Совместимость формул в режиме DirectQuery](http://msdn.microsoft.com/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Описывает различия, перечисляет функции, неподдерживаемые в режиме DirectQuery, а также функции, которые поддерживаются, но могут возвратить отличающиеся результаты.|  
|[Справочник по выражениям анализа данных (DAX)](http://msdn.microsoft.com/70a82136-0926-4a91-bcb3-e18e82593b0d)|Этот раздел содержит подробное описание синтаксиса языка выражений анализа данных (DAX), операторов и функций.|  
  
> [!NOTE]  
>  В этом разделе не содержатся пошаговые примеры создания вычислений. Так как вычисления задаются в вычисляемых столбцах, мерах и фильтрах строк (в ролях), указания по созданию формул DAX приведены в связанных с этими элементами задачах. Дополнительные сведения см. в разделе [Создание вычисляемого столбца](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [Создание и управление меры](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md), и [Создание и управление ролями](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Хотя выражения DAX могут использоваться для осуществления запросов к табличной модели служб, тематика этого раздела связана именно с использованием формул DAX при создании вычислений.  
  
  
