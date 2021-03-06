---
title: Применение функций прогнозирования к модели | Документация Майкрософт
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 192f55c8194bfb9b85b3e0bfad51d8261e45ab0a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540662"
---
# <a name="apply-prediction-functions-to-a-model"></a>Применение функций прогнозирования к модели
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Чтобы создать прогнозирующий запрос в службах интеллектуального анализа данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо сначала выбрать модель интеллектуального анализа данных, на которой будет основан этот запрос. Можно выбрать любую модель интеллектуального анализа данных, существующую в текущем проекте.  
  
 Выбрав модель, добавьте в запрос *прогнозирующую функцию* . Её можно использовать для получения прогноза. Кроме того, в запросы можно добавлять прогнозирующие функции, которые возвращают соответствующие статистические данные, например вероятность получения прогнозируемого значения, или информацию, на основе которой быть составлен прогноз.  
  
 Прогнозирующие функции могут возвращать следующие типы значений.  
  
-   Имя прогнозируемого атрибута и значение, которое прогнозируется.  
  
-   Статистика по распределению и дисперсии предсказанных значений.  
  
-   Вероятность заданного результата или всех возможных результатов.  
  
-   Верхние или нижние оценки или значения.  
  
-   Значения, связанные с заданным узлом, объектом или атрибутом.  
  
 Тип доступных прогнозирующих функций зависит от типа модели, с которой вы работаете. Например, прогнозирующие функции, применяемые к моделям дерева принятия решений, могут возвращать правила и описания узлов, а прогнозирующие функции для моделей временных рядов — временной промежуток и другие сведения, связанные с временными рядами.  
  
 Список прогнозирующих функций, поддерживаемых почти всеми типами моделей, см. в разделе [Общие функции прогнозирования (расширения интеллектуального анализа данных)](../../dmx/general-prediction-functions-dmx.md).  
  
 Примеры запросов к модели интеллектуального анализа данных определенного типа см. в справочнике по алгоритмам, в разделе [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>Выберите модель интеллектуального анализа данных, которая должна использоваться для прогноза.  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]щелкните модель правой кнопкой мыши и выберите пункт **Построить прогнозирующий запрос**.  
  
     --ИЛИ--  
  
     В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]щелкните вкладку **Прогнозирование моделей интеллектуального анализа данных**, а затем щелкните **Выбрать модель** в таблице  **Модель интеллектуального анализа данных** .  
  
2.  В диалоговом окне **Выбор модели интеллектуального анализа данных** выберите модель интеллектуального анализа данных и нажмите кнопку **ОК**.  
  
     Можно выбрать любую модель в текущей базе данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Для создания запроса с помощью модели, расположенной в другой базе данных, необходимо открыть новое окно запроса в контексте этой базы данных или открыть файл решения, который содержит эту модель.  
  
### <a name="add-prediction-functions-to-a-query"></a>Добавление прогнозирующих функций в запрос  
  
1.  В **построителе прогнозирующих запросов**задайте входные данные для прогнозирования, указав значения в диалоговом окне **Ввод одноэлементного запроса** или связав модель с внешним источником данных.  
  
     Дополнительные сведения см. в разделе [Выбор и сопоставление входных данных для прогнозирующего запроса](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  Для создания прогнозов вводить данные необязательно. Если входных данных нет, алгоритм обычно возвращает наиболее вероятное прогнозируемое значение для всех возможных входных значений.  
  
2.  Щелкните столбец **Источник** и выберите значение в списке.  
  
    |||  
    |-|-|  
    |**\<Имя модели >**|Выберите этот параметр для включения значений из модели интеллектуального анализа данных в выходные данные. Можно добавить только прогнозируемые столбцы.<br /><br /> Если добавляется столбец из модели, возвращаемый результат представляет собой список значений этого столбца, которые могут повторяться.<br /><br /> Столбцы, добавляемые с помощью этого параметра, включаются в предложение SELECT результирующей инструкции DMX.|  
    |**Prediction Function**|Выберите этот параметр для просмотра списка прогнозирующих функций.<br /><br /> Значения выбранных функций добавляются в предложение SELECT результирующей инструкции DMX.<br /><br /> Список прогнозирующих функций не фильтруется и не ограничивается выбранным типом модели. Поэтому, если вы сомневаетесь, поддерживается ли функция для текущего типа модели, можно просто добавить функцию в список и посмотреть, возникла ли ошибка.<br /><br /> Элементы списка с символом доллара в начале (например, $AdjustedProbability) представляют столбцы вложенной таблицы, получаемой при использовании функции **PredictHistogram**. Это сочетания клавиш, которые можно использовать, чтобы получить один столбец, а не вложенную таблицу.|  
    |**Пользовательское выражение**|Выберите этот параметр для ввода пользовательского выражения, а затем назначьте псевдоним выходным данным.<br /><br /> Пользовательское выражение добавляется в предложение SELECT конечного прогнозирующего запроса DMX.<br /><br /> Этот параметр полезен, если нужно добавить текст для вывода с каждой строкой, вызывать функции VB или пользовательские хранимые процедуры.<br /><br /> Сведения об использовании функций VBA и Excel из DMX см. в разделе [Функции VBA в DAX и многомерных выражениях](../../mdx/vba-functions-in-mdx-and-dax.md).|  
  
3.  После добавления каждой функции или выражения перейдите в представление DMX, чтобы посмотреть, как функция добавляется в инструкцию DMX.  
  
    > [!WARNING]  
    >  Построитель прогнозирующих запросов не проверяет DMX до нажатия кнопки **Результаты**. Часто оказывается, что выражение, созданное построителем запросов, не является допустимой инструкцией DMX. Типичные случаи — это указание столбца, не связанного с прогнозируемым столбцом, или попытка прогнозирования столбца во вложенной таблице, что требует вложенной инструкции SELECT. В этот момент можно переключиться в представление DMX и продолжить редактирование инструкции.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>Пример Создание запроса на основе модели кластеризации  
  
1.  Если у вас нет модели кластеризации для создания этого образца запроса, создайте модель [TM_Clustering] с помощью [Учебника по основам интеллектуального анализа данных](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
2.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]щелкните правой кнопкой мыши модель [TM_Clustering] и выберите пункт **Построить прогнозирующий запрос**.  
  
3.  В меню **Модель интеллектуального анализа данных** выберите пункт **Одноэлементный запрос**.  
  
4.  В диалоговом окне **Ввод одноэлементного запроса** задайте следующие значения как входные:  
  
    -   Gender = M  
  
    -   Расстояние до работы = 5—10 миль  
  
5.  В сетке запросов в списке столбца **Источник**выберите модель интеллектуального анализа данных TM_Clustering и добавьте столбец [Bike Buyer] ("Покупатель велосипеда").  
  
6.  В списке столбца **Источник**выберите значение **Прогнозирующая функция**и добавьте функцию **Cluster**.  
  
7.  В списке столбца **Источник**выберите значение **Прогнозирующая функция**, добавьте функцию **PredictSupport**и перетащите столбец модели [Bike Buyer] в поле **Критерий или аргумент** . В столбце **Псевдоним** введите **Support** (Поддержка).  
  
     Скопируйте выражение, представляющее прогнозирующую функцию, и ссылку на столбец из поля **Критерий или аргумент** .  
  
8.  В качестве **Источника**выберите **Пользовательское выражение**, введите псевдоним, а затем укажите функцию CEILING Excel с помощью следующего синтаксиса:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Вставьте ссылку на столбец в качестве аргумента функции.  
  
     Например, следующее выражение возвращает значение CEILING для значения поддержки.  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     В столбце **Псевдоним** введите CEILING.  
  
9. Щелкните **Переключиться в представление текста запроса** , чтобы увидеть созданную инструкцию DMX, а затем щелкните **Переключиться в представление результатов запроса** , чтобы увидеть выходные столбцы прогнозирующего запроса.  
  
     В следующей таблице показаны ожидаемые результаты.  
  
    |Покупатель велосипеда|$Cluster|Псевдоним|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Кластер 8|954|953.948638926372|  
  
 Если вы хотите добавить другие предложения в другом месте в операторе-например, если вы хотите добавить предложение WHERE-не удается добавить его с помощью сетки; Переключитесь в режим DMX-сначала.  
  
## <a name="see-also"></a>См. также  
 [Запросы интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
