---
title: "обработать модель интеллектуального анализа данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "модели интеллектуального анализа данных [службы Analysis Services], обработка"
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# обработать модель интеллектуального анализа данных
  На вкладке «Модели интеллектуального анализа данных» конструктора интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]можно либо обработать конкретную модель, которая связана со структурой интеллектуального анализа данных, либо обработать все модели, связанные с этой структурой.  
  
 Обработка модели интеллектуального анализа данных производится с помощью следующих инструментов.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Для обработки также можно использовать команду XMLA Process. Дополнительные сведения см. в разделе [Средства и способы обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### Обработка отдельной модели интеллектуального анализа данных с помощью SQL Server Data Tools  
  
1.  На вкладке **Модели интеллектуального анализа данных** конструктора интеллектуального анализа данных выберите модель интеллектуального анализа данных из одного или нескольких столбцов моделей в сетке.  
  
2.  В меню **Модель интеллектуального анализа данных** выберите пункт **Обработать модель**.  
  
     При внесении изменений в структуру интеллектуального анализа данных будет выдано приглашение к повторному развертыванию структуры перед обработкой модели. Нажмите кнопку **Да**.  
  
3.  В диалоговом окне **Обработка модели интеллектуального анализа данных — \<модель>** нажмите кнопку **Выполнить**.  
  
     Откроется диалоговое окно **Развитие процесса** , отображающее подробные сведения об обработке модели.  
  
4.  После успешного завершения обработки модели нажмите кнопку **Закрыть** в диалоговом окне **Развитие процесса** .  
  
5.  Нажмите кнопку **Закрыть** в диалоговом окне **Обработка модели интеллектуального анализа данных — \<модель>**.  
  
 Были обработаны только структура интеллектуального анализа данных и выбранная модель интеллектуального анализа данных.  
  
### Обработка всех моделей интеллектуального анализа данных, которые связаны со структурой интеллектуального анализа данных  
  
1.  На вкладке **Модели интеллектуального анализа данных** конструктора интеллектуального анализа данных выберите команду **Обработать структуру интеллектуального анализа данных и все модели** из меню **Модель интеллектуального анализа данных** .  
  
2.  При внесении изменений в структуру интеллектуального анализа данных будет выдано приглашение к повторному развертыванию структуры перед обработкой моделей. Нажмите кнопку **Да**.  
  
3.  В диалоговом окне **Обработка структуры интеллектуального анализа данных — \<структура>** нажмите кнопку **Выполнить**.  
  
4.  Откроется диалоговое окно **Развитие процесса** , отображающее подробные сведения об обработке модели.  
  
5.  После успешного завершения обработки моделей нажмите кнопку **Закрыть** в диалоговом окне **Развитие процесса** .  
  
6.  Нажмите кнопку **Закрыть** в диалоговом окне **Обработка \<модель>**.  
  
 Были обработаны структура интеллектуального анализа данных и все связанные с ней модели интеллектуального анализа данных.  
  
## См. также  
 [Задачи и инструкции по модели интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  