---
title: Примеры запросов к модели временных рядов | Документация Майкрософт
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f839b7e108f6398f96c302016cfc45c82a110c6d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526502"
---
# <a name="time-series-model-query-examples"></a>Примеры запросов моделей временных рядов
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  К модели интеллектуального анализа данных можно создать два вида запросов: запросы содержимого, возвращающие подробные сведения о закономерностях, обнаруженных при анализе, и прогнозирующие запросы, использующие закономерности, содержащиеся в модели, для прогнозирования новых данных. Например, запрос содержимого для модели временных рядов может возвратить дополнительные сведения о найденных периодических структурах; прогнозирующий запрос может выполнить прогнозы для следующих 5 — 10 временных срезов. Запрос также позволяет получить метаданные, описывающие модель.  
  
 В этом разделе описывается процесс создания этих двух типов запросов к моделям, основанным на алгоритме временных рядов (Майкрософт).  
  
 **Запросы содержимого**  
  
 [Получение подсказок периодичности для модели](#bkmk_Query1)  
  
 [Получение выражения для модели ARIMA](#bkmk_Query2)  
  
 [Получение выражения для модели ARTxp](#bkmk_Query3)  
  
 **Прогнозирующие запросы**  
  
 [Основные сведения о выборе между заменой и расширением данных временных рядов](#bkmk_ReplaceExtend)  
  
 [Прогнозирование с помощью EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [Прогнозирование с помощью REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
 [Подстановка отсутствующего значения в моделях временных рядов](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>Получение сведений о модели временных рядов  
 Запрос содержимого модели может предоставить основные сведения о модели, например параметры, которые были использованы при создании модели, или время последней обработки модели. В следующем примере показывается основной синтаксис, используемый для создания запросов к содержимому модели при помощи набора строк схемы интеллектуального анализа данных.  
  
###  <a name="bkmk_Query1"></a> Образец запроса 1. Получение подсказок периодичности для модели  
 Периодичности, найденные во временных рядах, можно получить, создав запросы к дереву ARIMA или ARTXP. Однако периодичности в завершенной модели могут не совпадать с периодами, указанными в качестве подсказок при создании модели. Для получения подсказок, которые были предоставлены в качестве параметров при создании модели, можно создать запрос к набору строк схемы содержимого модели, используя следующую инструкцию расширений интеллектуального анализа данных.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 Частичные результаты:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0,1, MINIMUM_SUPPORT = 10, PERIODICITY_HINT ={1,3},...|  
  
 Указание периодичности по умолчанию {1} появляется во всех моделях. Данный образец модели был создан с дополнительным указанием, которое может отсутствовать в окончательной модели.  
  
> [!NOTE]  
>  Результаты были усечены для удобства чтения.  
  
  
###  <a name="bkmk_Query2"></a> Образец запроса 2. Получение выражения для модели ARIMA  
 Получить выражение для модели ARIMA можно, создав запрос к любому узлу в отдельном дереве. Следует помнить, что у каждого дерева в модели ARIMA своя периодичность. При наличии нескольких рядов данных у каждого из них будет свой собственный набор деревьев периодичности. Следовательно, для получения выражения для определенного ряда данных вначале необходимо выделить дерево.  
  
 Например, префикс TA означает, что узел является частью дерева ARIMA, тогда как префикс TS используется для деревьев ARTXP. Деревья корня ARIMA можно найти с помощью запроса к содержимому модели для узлов со значением NODE_TYPE, равным 27. Значение ATTRIBUTE_NAME можно использовать для поиска корневого узла ARIMA для конкретных рядов данных. В этом примере запроса выполняется поиск узлов ARIMA, представляющих значения объема продаж модели R250 в Европе.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 С помощью идентификатора этого узла можно получить подробные данные об уравнении ARIMA для этого дерева. Приведенная ниже инструкция DMX извлекает краткую форму уравнения ARIMA для рядов данных. Она также возвращает пересечение из вложенной таблицы — NODE_DISTRIBUTION. В этом примере уравнение получается по ссылке на уникальный идентификатор TA00000007 узла. Однако при использовании идентификатора другого узла можно получить от модели несколько другие результаты.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 Пример результатов:  
  
|Краткое выражение|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24...|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 Дополнительные сведения об интерпретации этой информации см. в разделе [Содержимое моделей интеллектуального анализа данных для моделей временных рядов (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
  
###  <a name="bkmk_Query3"></a> Образец запроса 3. Получение выражения для модели ARTXP  
 В моделях ARTxp на каждом уровне дерева хранится разная информация. Дополнительные сведения о структуре модели ARTxp и о том, как следует интерпретировать сведения в выражении, см. в разделе [Содержимое моделей интеллектуального анализа данных для моделей временных рядов (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 Приведенная ниже инструкция DMX извлекает данные для части дерева ARTxp, представляющей объем продаж модели R250 в Европе.  
  
> [!NOTE]  
>  Имя столбца вложенной таблицы — VARIANCE — должно быть заключено в скобки, чтобы отличаться от зарезервированного ключевого слова с таким же именем. Столбцы вложенной таблицы — PROBABILITY и SUPPORT — не включаются, поскольку у большинства вариантов они пустые.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 Дополнительные сведения об интерпретации этой информации см. в разделе [Содержимое моделей интеллектуального анализа данных для моделей временных рядов (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
  
## <a name="creating-predictions-on-a-time-series-model"></a>Создание прогнозов на модели временных рядов  
 Начиная с [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], можно добавлять новые данные в модель временных рядов и автоматически встраивать новые данные в эту модель. Добавить новые данные в модель интеллектуального анализа данных временных рядов можно одним из двух способов.  
  
-   Использовать **PREDICTION JOIN** для соединения данных из внешнего источника с обучающими данными.  
  
-   Использовать одноэлементный прогнозирующий запрос для предоставления каждый раз данных только одного среза. Сведения о том, как создать одноэлементный прогнозирующий запрос, см. в разделе [Средства запросов интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
###  <a name="bkmk_ReplaceExtend"></a> Основные сведения о работе операций замены и расширения  
 Добавляя новые данные в модель временных рядов, можно указать, что делать с прежними обучающими данными — расширить или заменить их.  
  
-   **Расширить:** При расширении ряда данных службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] добавляют новые данные в конец существующего набора данных для обучения. Также увеличивается число обучающих вариантов.  
  
     Увеличение количества обучающих вариантов полезно, чтобы модель постоянно обновлялась новыми данными. Например, если необходимо создать растущий с течением времени обучающий набор, можно просто дополнить модель.  
  
     Чтобы расширить данные, создайте **PREDICTION JOIN** для модели временных рядов, определите источник новых данных и используйте аргумент **EXTEND_MODEL_CASES** .  
  
-   **Замените:** При замене данных в ряду данных [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] сохраняют обученную модель, но используют новые значения данных для замены некоторых или всех существующих обучающих вариантов. Таким образом, размер обучающих данных никогда не меняется, но варианты постоянно заменяются более новыми данными. При достаточном количестве новых данных можно полностью заменить обучающие данные новой последовательностью.  
  
     Замена вариантов полезна в том случае, если необходимо обучить модель на одном наборе вариантов, а затем применить эту модель к другому ряду данных.  
  
     Для замены данных создайте **PREDICTION JOIN** в модели временных рядов, определите источник новых данных и используйте аргумент **REPLACE_MODEL_CASES** .  
  
> [!NOTE]  
>  Когда добавляются новые данные, исторические прогнозы невозможны.  
  
 Независимо от того, дополняются обучающие данные или замещаются, прогнозы всегда начинаются с момента времени, в который завершается использование исходного набора данных для обучения. Иными словами, если новые данные содержат n временных срезов и запрашиваются прогнозы для временных шагов с 1 по n, то период прогнозирования совпадет с периодом новых данных и новые прогнозы не создадутся.  
  
 Чтобы получить новые прогнозы для периодов времени, не перекрывающихся с новыми данными, необходимо либо начать прогнозирование с временного среза n+1, либо запросить дополнительные временные срезы.  
  
 Предположим, что существующая модель имеет данные за шесть месяцев. Необходимо расширить эту модель данными о продажах за последние три месяца. Одновременно требуется прогноз на следующие три месяца. Чтобы получить только новые прогнозы при добавлении новых данных, задайте в качестве начальной точки временной срез 4, а в качестве конечной — срез 7. Можно также запросить общую сумму шести прогнозов, но временные срезы для первых трех будут перекрыты только что добавленными данными.  
  
 Дополнительные сведения о синтаксисе инструкций **REPLACE_MODEL_CASES** и **EXTEND_MODEL_CASES**, а также примеры запросов см. в статье [PredictTimeSeries (расширения интеллектуального анализа данных)](../../dmx/predicttimeseries-dmx.md).  
  
  
###  <a name="bkmk_EXTEND"></a> Прогнозирование с помощью EXTEND_MODEL_CASES  
 Прогноз зависит от того, добавляются новые обучающие варианты к существующим или замещают их. При расширении модели новые данные добавляются в конец последовательности и размер обучающего набора увеличивается. Но временные срезы, используемые для прогнозирующих запросов, всегда начинаются в конце исходной последовательности. Следовательно, если добавляется три новые точки данных и запрашивается шесть прогнозов, первые три возвращенных прогноза перекрываются новыми данными. В этом случае службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] возвращают вместо прогноза фактические новые точки данных до тех пор, пока все новые точки данных не будут использованы. Затем службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] делают прогнозы на основе составных последовательностей.  
  
 Такое поведение позволяет добавлять новые данные и отображать на диаграмме прогнозов реальные объемы продаж, а не данные прогнозов.  
  
 Например, чтобы добавить три новые точки данных и сделать три новых прогноза, необходимо сделать следующее.  
  
-   Создать **PREDICTION JOIN** для модели временных рядов и определить источник новых данных за три месяца.  
  
-   Запросить прогнозирование для шести временных срезов. Для этого задайте шесть временных срезов, указав в качестве начальной точки временной срез 1, а конечной — временной срез 7. Это справедливо только для параметра EXTEND_MODEL_CASES.  
  
-   Чтобы получить только новые прогнозы, задайте начальную точку как 4 и конечную точку как 7.  
  
-   Необходимо использовать аргумент **EXTEND_MODEL_CASES**.  
  
     Для первых трех временных срезов возвращаются графики фактических продаж, а для следующих трех временных срезов — прогнозы, основанные на расширенной модели.  
  
  
###  <a name="bkmk_REPLACE"></a> Прогнозирование с помощью REPLACE_MODEL_CASES  
 Если варианты в модели замещаются, размер модели остается прежним, но службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] заменяют отдельные варианты в ней. Это полезно для перекрестного прогнозирования и сценариев, где важно согласовывать постоянный размер набора обучающих данных.  
  
 Например, у одного из магазинов недостаточно данных о продажах. Можно создать общую модель с усреднением продаж для всех магазинов в регионе и последующим обучением модели. Затем, чтобы получить прогноз для магазина с недостаточными данными о продажах, создайте **PREDICTION JOIN** с новыми данными о продажах только для этого магазина. В этом случае службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] сохраняют закономерности, извлеченные из региональной модели, но заменяют существующие обучающие варианты данными из конкретного магазина. В результате прогнозируемые значения будут ближе к линиям тренда для отдельного магазина.  
  
 Если используется аргумент **REPLACE_MODEL_CASES** , службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] постоянно добавляют новые случаи в конец набора вариантов и удаляют соответствующий номер из начала набора вариантов. Если новых данных больше, чем было в исходном обучающем наборе, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] стирают самые старые данные. Если ввести достаточно новых значений, прогнозы могут быть полностью основаны на новых данных.  
  
 Например, модель была обучена на наборе данных, состоящем из 1000 строк. Затем добавляется 100 строк новых данных. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] удаляют первые 100 строк из обучающего набора и добавляют 100 строк новых данных в конец набора, что в сумме дает 1000 строк. Если добавляется 1100 строк новых данных, будет использоваться только 1000 самых последних.  
  
 Вот еще один пример. Чтобы добавить новые данные за три месяца и создать три новых прогноза, необходимо выполнить следующие действия.  
  
-   Создать **PREDICTION JOIN** для модели временных рядов и использовать аргумент **REPLACE_MODEL_CASE** .  
  
-   Задать источник новых данных за три месяца. Эти данные могут быть совершенно не из того источника, откуда были взяты исходные обучающие данные.  
  
-   Запросить прогнозирование для шести временных срезов. Для этого укажите шесть временных срезов либо укажите в качестве начальной точки временной срез 1, а конечной — временной срез 7.  
  
    > [!NOTE]  
    >  В отличие от **EXTEND_MODEL_CASES**, невозможно вернуть те значения, которые были добавлены в качестве входных данных. Все шесть возвращаемых значений являются прогнозами, основанными на обновленной модели, которая содержит как старые, так и новые данные.  
  
    > [!NOTE]  
    >  При работе с параметром REPLACE_MODEL_CASES, начиная с метки времени 1 пользователь будет получать новые прогнозы, основываясь на новых данных, которые будут заменять старые обучающие данные.  
  
 Дополнительные сведения о синтаксисе инструкций **REPLACE_MODEL_CASES** и **EXTEND_MODEL_CASES**, а также примеры запросов см. в статье [PredictTimeSeries (расширения интеллектуального анализа данных)](../../dmx/predicttimeseries-dmx.md).  
  
  
###  <a name="bkmk_MissingValues"></a> Подстановка отсутствующего значения в моделях временных рядов  
 Если новые данные добавляются в модель временных рядов с помощью инструкции **PREDICTION JOIN** , в новом наборе данных не может быть отсутствующих значений. В любой неполной последовательности модель должна подставить вместо отсутствующих значений NULL среднее значение, конкретное числовое значение или прогнозируемое значение. Если используется **EXTEND_MODEL_CASES**, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] замещают отсутствующие значения прогнозами, основанными на исходной модели. Если используется **REPLACE_MODEL_CASES**, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] замещают отсутствующие значения значением, указанным в параметре *MISSING_VALUE_SUBSTITUTION* .  
  
## <a name="list-of-prediction-functions"></a>Список прогнозирующих функций  
 Все алгоритмы [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживают общий набор функций. Однако алгоритм временных рядов ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) поддерживает дополнительные функции, перечисленные в следующей таблице.  
  
|||  
|-|-|  
|прогнозирующую функцию|Использование|  
|[Lag (расширения интеллектуального анализа данных)](../../dmx/lag-dmx.md)|Возвращает несколько временных срезов между датой текущего варианта и последней датой обучающего набора.<br /><br /> Типичное применение этой функции — идентификация недавних обучающих вариантов с целью получения подробных данных о них.|  
|[PredictNodeId (расширения интеллектуального анализа данных)](../../dmx/predictnodeid-dmx.md)|Возвращает идентификатор узла для заданного прогнозируемого столбца.<br /><br /> Типичное применение этой функции — определение узла, формирующего конкретное прогнозируемое значение, чтобы просмотреть варианты, связанные с узлом, или получить формулу и другие сведения.|  
|[PredictStdev (расширения интеллектуального анализа данных)](../../dmx/predictstdev-dmx.md)|Возвращает стандартное отклонение прогнозов для заданного прогнозируемого столбца.<br /><br /> Эта функция заменяет аргумент INCLUDE_STATISTICS, который не поддерживается моделями временных рядов.|  
|[PredictVariance (расширения интеллектуального анализа данных)](../../dmx/predictvariance-dmx.md)|Возвращает дисперсию прогнозов для заданного прогнозируемого столбца.<br /><br /> Эта функция заменяет аргумент INCLUDE_STATISTICS, который не поддерживается моделями временных рядов.|  
|[PredictTimeSeries (расширения интеллектуального анализа данных)](../../dmx/predicttimeseries-dmx.md)|Возвращает прогнозируемые будущие или исторические значения для временного ряда.<br /><br /> Модели временных рядов также можно запрашивать с помощью общей прогнозирующей функции [Predict (расширения интеллектуального анализа данных)](../../dmx/predict-dmx.md).|  
  
 Список функций, общих для всех алгоритмов [!INCLUDE[msCoName](../../includes/msconame-md.md)], см. в статье [Общие функции прогнозирования (расширения интеллектуального анализа данных)](../../dmx/general-prediction-functions-dmx.md). Синтаксис отдельных функций см. в статье [Справочник по функциям расширений интеллектуального анализа данных (расширения интеллектуального анализа данных)](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
  
## <a name="see-also"></a>См. также  
 [Запросы интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-queries.md)   
 [Алгоритм временных рядов (Майкрософт)](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Технический справочник по алгоритму временных рядов (Майкрософт)](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Содержимое моделей интеллектуального анализа данных для моделей временных рядов (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
