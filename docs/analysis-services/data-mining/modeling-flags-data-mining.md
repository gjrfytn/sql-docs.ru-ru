---
title: "Флаги моделирования (интеллектуальный анализ данных) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "атрибуты [интеллектуальный анализ данных]"
  - "типы данных [интеллектуальный анализ данных]"
  - "REGRESSOR, флаг"
  - "MODEL_EXISTENCE_ONLY, флаг"
  - "REGRESSOR, столбец"
  - "столбцы [интеллектуальный анализ данных], флаги моделирования"
  - "флаг моделирования NOT NULL"
  - "флаги моделирования [интеллектуальный анализ данных]"
  - "значения NULL [службы Analysis Services]"
  - "MODEL_EXISTENCE_ONLY, столбец"
  - "кодирование [интеллектуальный анализ данных]"
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
caps.latest.revision: 48
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 48
---
# Флаги моделирования (интеллектуальный анализ данных)
  Флаги моделирования можно использовать в службах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , чтобы включить в алгоритм интеллектуального анализа данных дополнительные сведения о данных, которые определены в таблице вариантов. Алгоритм может использовать эти сведения для создания более точной модели интеллектуального анализа данных.  
  
 Некоторые флаги модели определены на уровне структуры интеллектуального анализа данных, а другие определены на уровне столбца модели интеллектуального анализа данных. Например, флаг моделирования **NOT NULL** используется со столбцами структуры интеллектуального анализа данных. В столбцах модели интеллектуального анализа данных можно определить дополнительные флаги модели в зависимости от алгоритма, используемого при создании модели.  
  
> [!NOTE]  
>  В подключаемых модулях сторонних разработчиков могут использоваться другие флаги модели, дополняющие стандартные флаги служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## Список флагов модели  
 В следующем списке приведено описание флагов модели, которые поддерживаются в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Сведения о флагах моделирования, поддерживаемых конкретными алгоритмами, см. в разделе технического справочника для алгоритма, с помощью которого была создана модель.  
  
 **NOT NULL**  
 Указывает, что значения столбца атрибутов не должны включать значение NULL. Если службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] найдут значение NULL в данном столбце атрибутов в процессе обучения модели, будет выдана ошибка.  
  
 **MODEL_EXISTENCE_ONLY**  
 Означает, что столбец будет обрабатываться так, как будто у него два возможных состояния: **Missing** и **Existing**. Если значение составляет **NULL**, оно рассматривается как недостающее. Флаг MODEL_EXISTENCE_ONLY применяется к прогнозируемому атрибуту и поддерживается большинством алгоритмов.  
  
 Фактически установка для флага MODEL_EXISTENCE_ONLY значения **True** меняет представление значений так, что становятся возможными только два состояния: **Missing** и **Existing**. Все неотсутствующие состояния объединяются в единое значение **Existing**.  
  
 Этот флаг моделирования, как правило, используется в атрибутах, для которых состояние **NULL** имеет неявный смысл, а явно заданное значение состояния **NOT NULL** может не быть столь важным, как факт, что этот столбец имеет некоторое значение. Например, в столбце [DateContractSigned] может присутствовать значение **NULL**, если контракт не подписан, и значение **NOT NULL**, если контракт подписан. Поэтому, если назначение модели состоит в прогнозировании того, что контракт будет подписан, можно использовать флаг MODEL_EXISTENCE_ONLY для пропуска точного значения даты в вариантах со значением **NOT NULL** и проведения различия только между вариантами, в которых контракт отсутствует (**Missing**) или существует (**Existing**).  
  
> [!NOTE]  
>  Недостающее состояние — это специальное состояние, используемое алгоритмом, и его не следует путать с текстовым значением «Missing» в столбце. Дополнительные сведения см. в разделе [Отсутствующие значения (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
 **REGRESSOR**  
 Указывает, что столбец во время обработки может использоваться в качестве регрессора. Этот флаг определяется в столбце модели интеллектуального анализа данных и применим только к столбцам с непрерывным числовым типом данных. Дополнительные сведения об использовании этого флага см. в подразделе [Использование флага моделирования REGRESSOR](#bkmk_UseRegressors).  
  
## Просмотр и смена флагов модели  
 В конструкторе моделей интеллектуального анализа данных можно просматривать флаги модели, связанные со столбцом структуры интеллектуального анализа или столбцом модели, рассматривая свойства структуры или модели.  
  
 Чтобы определить, какие флаги модели применены к текущей структуре интеллектуального анализа, можно создать запрос к набору строк схемы интеллектуального анализа данных, возвращающий флаги моделирования только для столбцов структуры, наподобие следующего.  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 В конструкторе моделей интеллектуального анализа данных можно добавить или изменить флаги модели, используемые в модели, отредактировав свойства связанных столбцов. Для таких изменений требуется повторная обработка структуры или модели.  
  
 Флаги модели можно указать в новой структуре или модели интеллектуального анализа данных с помощью расширения интеллектуального анализа данных либо с помощью скриптов объектов AMO или XMLA. Однако возможность изменения флагов модели, используемых в существующей модели и структуре интеллектуального анализа данных, с помощью расширения интеллектуального анализа данных не предусмотрена. Необходимо создать новую модель интеллектуального анализа, используя синтаксис `ALTER MINING STRUCTURE….ADD MINING MODEL`.  
  
##  <a name="bkmk_UseRegressors"></a> Использование флага моделирования REGRESSOR  
 Если для столбца задан флаг модели REGRESSOR, он указывает алгоритму, что столбец содержит потенциальные регрессоры. Фактические регрессоры, используемые в модели, определяются алгоритмом. Потенциальный регрессор может быть отброшен, если он не моделирует прогнозируемый атрибут.  
  
 При создании модели с использованием мастера интеллектуального анализа данных все непрерывные входные столбцы отмечаются как возможные регрессоры. Поэтому, даже если пользователь не задает явно флаг REGRESSOR для какого-либо столбца, может оказаться, что этот столбец используется как регрессор в модели.  
  
 Можно определить, какие регрессоры фактически использовались в обрабатываемой модели, выполнив запрос к набору строк схемы, относящемуся к модели интеллектуального анализа данных, как показано в следующем примере.  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **Примечание** Если внесены изменения в модель интеллектуального анализа данных и тип содержимого какого-то столбца изменен с непрерывного на дискретный, необходимо вручную изменить указанный флаг для этого столбца интеллектуального анализа, а затем повторно обработать модель.  
  
### Регрессоры в моделях линейной регрессии  
 Модели линейной регрессии основаны на алгоритме дерева принятия решений [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Даже если не используется алгоритм линейной регрессии [!INCLUDE[msCoName](../../includes/msconame-md.md)] , любая модель дерева принятия решений может содержать дерево или узлы, представляющие регрессию применительно к какому-то непрерывному атрибуту.  
  
 Поэтому в таких моделях не обязательно указывать, что непрерывный столбец представляет собой регрессор. Алгоритм дерева принятия решений [!INCLUDE[msCoName](../../includes/msconame-md.md)] секционирует набор данных на области со значимыми шаблонами, даже если для столбца не задан флаг REGRESSOR. Различие между указанными случаями состоит в том, что если пользователем задан флаг моделирования, то алгоритм попытается найти регрессионные уравнения в следующей форме для подгонки шаблонов к узлам дерева.  
  
 a*C1 + b\*C2 +...  
  
 Далее вычисляется сумма остатков, и, если отклонение слишком велико, принудительно выполняется разбиение дерева.  
  
 Например, если осуществляется прогноз поведения клиента в процессе покупки с использованием дохода, **Income** , в качестве атрибута и на соответствующем столбце **Income** устанавливается флаг модели REGRESSOR, то в алгоритме вначале предпринимается попытка выполнить подгонку значений Income с применением стандартной формулы регрессии. Если отклонение слишком велико, то происходит отказ от применения формулы регрессии и разбиение дерева осуществляется по какому-то другому атрибуту. Затем в алгоритме дерева принятия решений предпринимается попытка подгонки регрессора к доходу в каждой из ветвей, полученных после разбиения.  
  
 Можно применить параметр FORCE_REGRESSOR для обеспечения того, чтобы в алгоритме использовался конкретный регрессор. Этот параметр может применяться с алгоритмом дерева принятия решений и алгоритмом линейной регрессии.  
  
## Связанные задачи  
 Следующие ссылки помогут узнать больше об использовании флагов модели.  
  
|Задача|Раздел|  
|----------|-----------|  
|Редактирование флагов моделирования с помощью конструктора интеллектуального анализа данных|[Просмотр или изменение флагов моделирования (интеллектуальный анализ данных)](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Определение указания для алгоритма с рекомендацией вероятных регрессоров|[Указание столбца, который будет использоваться в модели в качестве регрессора](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Просмотр флагов модели, поддерживаемых конкретными алгоритмами (в подразделе «Флаги моделирования») каждого раздела справки по алгоритму)|[Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|Дополнительные сведения о столбцах структуры интеллектуального анализа и свойствах, которые для них можно задать|[Столбцы структуры интеллектуального анализа данных](../../analysis-services/data-mining/mining-structure-columns.md)|  
|Дополнительные сведения о столбцах модели интеллектуального анализа данных и флагах моделирования, которые можно применить на уровне модели|[Столбцы модели интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-columns.md)|  
|Просмотр синтаксиса для работы с флагами модели в инструкциях расширений интеллектуального анализа данных|[Флаги моделирования (расширения интеллектуального анализа данных)](../../dmx/modeling-flags-dmx.md)|  
|Понятие отсутствующих значений и работа с ними|[Отсутствующие значения (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)|  
|Сведения об управлении моделями и структурами, а также о задании свойств использования|[Перемещение объектов интеллектуального анализа данных](../../analysis-services/data-mining/moving-data-mining-objects.md)|  
  
  