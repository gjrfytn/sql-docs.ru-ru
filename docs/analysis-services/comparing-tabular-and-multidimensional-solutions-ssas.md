---
title: "Сравнение табличных и многомерных решений (службы SSAS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# Сравнение табличных и многомерных решений (службы SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] предоставляет несколько подходов для создания семантической модели бизнес-аналитики: многомерный, табличный и Power Pivot.  
  
 Это позволяет использовать процессы моделирования, адаптированные для разных пользовательских и бизнес-требований. Многомерный подход — это надежная технология, основанная на открытых стандартах, которая используется множеством поставщиков программного обеспечения бизнес-аналитики, но овладеть ей не так просто. Табличный подход использует реляционные модели, которые многим разработчикам кажутся более понятными. Power Pivot еще проще — эта технология предоставляет возможности визуального моделирования данных в Excel с поддержкой серверов через SharePoint.  
  
 Все модели развертываются как базы данных, которые работают в экземпляре служб Analysis Services. Они доступны клиентским средствам с помощью единого набора поставщиков данных и визуализируются в интерактивных и статических отчетах с помощью Excel, служб Reporting Services, Power BI и средств бизнес-аналитики других поставщиков.  
  
 Из-за различия в архитектуре памяти и метаданных ни один из типов моделей не являются взаимозаменяемым, хотя вы очень легко можете обновить табличную модель 1050–1103 до табличной модели 1200, а также сможете импортировать Power Pivot для создания абсолютно новой модели в виде табличного проекта.  
  
 Табличные и многомерные решения создаются с помощью среды [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] и предназначены для корпоративных проектов бизнес-аналитики, которые выполняются на автономном экземпляре [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Оба типа решений предоставляют высокопроизводительные аналитические базы данных, которые легко интегрируются с клиентами бизнес-аналитики. При этом каждое решение различается способом создания, использования и развертывания. Большая часть этого раздела посвящена сравнению данных двух типов, чтобы вы могли выбрать подходящий вам подход.  
  
 Для новых проектов разработки мы рекомендуем табличный тип. Он будет быстрее в проектировании, тестировании и развертывании, а также будет лучше работать с новыми приложениями бизнес-аналитики с самообслуживанием и облачными службами Майкрософт.  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a> Обзор типов моделирования  
 Нет опыта работы со службами Analysis Services? В следующей таблице описаны различные модели, подход и первоначальный выпуск.  
  
||||  
|-|-|-|  
|**Тип**|**Описание моделирования**|**Выпущено**|  
|Multidimensional|Конструкции моделирования OLAP (кубы, измерения, меры).|SQL Server 2000 и более поздние версии|  
|Табличный|Реляционные конструкции моделирования (модели, таблицы, столбцы).<br /><br /> На внутреннем уровне метаданные наследуются от OLAP конструкций моделирования (кубы, измерения, меры). Код и сценарии используют метаданные OLAP.|SQL Server 2012 и более поздние версии (уровни совместимости 1050–1103) <sup>1</sup>|  
|Табличные решения в SQL Server 2016|Реляционные конструкции моделирования (модели, таблицы, столбцы) задаются в определениях объектов табличных метаданных в сценариях и коде.|SQL Server 2016 (уровень совместимости 1200)|  
|Power Pivot|Изначально надстройка, которая теперь полностью интегрирована с Excel. Только визуальное моделирование по внутренней табличной инфраструктуре. Вы можете импортировать модель Power Pivot в SSDT для создания новой табличной модели, которая выполняется в экземпляре служб Analysis Services.|с помощью Excel и Power Pivot BI Desktop|  
  
 <sup>1</sup> Уровни совместимости, представленные в SQL Server 2012, учитываются в текущем выпуске из-за нового механизма табличных метаданных, а поддержка возможностей для реализации этого сценария доступна только на более высоком уровне. Значительные улучшения, в том числе DirectQuery, скриптов и программирования. Дополнительные сведения см. в разделе [What's New in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) .  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a> Функции модели  
  В следующей таблице приведена сводка доступности функций на уровне моделей. Просмотрите этот список, чтобы убедиться, что возможность, которую вы хотите использовать, доступна в создаваемой модели.  
  
|||||  
|-|-|-|-|  
||Multidimensional|Табличный|Power Pivot|  
|Действия|Да|Нет|Нет|  
|Aggregations|Да|Нет|Нет|  
|Вычисляемый столбец|Нет|Да|Да|  
|Вычисляемые меры|Да|Да|Да|  
|Вычисляемые таблицы|Нет|Да <sup>1</sup>|Нет|  
|Пользовательские сборки|Да|Нет|Нет|  
|Пользовательские свертки|Да|Нет|Нет|  
|элемент по умолчанию;|Да|Нет|Нет|  
|Отображение папок|Да|Да <sup>1</sup>|Нет|  
|Количество различных|Да|Да (посредством DAX)|Да (посредством DAX)|  
|Детализация|Да|Да (подробности открываются на отдельном листе)|Да|  
|Иерархии|Да|Да|Да|  
|Ключевые показатели эффективности|Да|Да|Да|  
|Связанные объекты|Да|Да (связанные таблицы)|Нет|  
|Связи «многие ко многим»|Да|Нет (но на уровне совместимости 1200 есть [двунаправленные кросс-фильтры](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md))|Нет|  
|Именованные наборы|Да|Нет|Нет|  
|Иерархии типа «родители-потомки»|Да|Да (посредством DAX)|Да (посредством DAX)|  
|Секции|Да|Да|Да|  
|Перспективы|Да|Да|Да|  
|Полуаддитивные меры|Да|Да|Да|  
|Переводы|[Да](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Да|[Да](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|Пользовательские иерархии|Да|Да|Да|  
|Обратная запись|Да|Нет|Нет|  
  
 <sup>1</sup> В разделе [Уровень совместимости табличных моделей в службах Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) описываются функциональные различия в табличных решениях.  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a> Вопросы работы с данными  
 В многомерных и табличных моделях применяются импортированные данные из внешних источников. Объем и тип данных, которые необходимо импортировать, может быть главным вопросом при выборе подходящей модели.  
  
 **Сжатие**  
  
 Как в табличных, так и в многомерных решениях используется сжатие данных, уменьшающее размер базы данных служб Analysis Services по отношению к хранилищу данных, из которого импортируются данные. Поскольку фактическое сжатие различается в зависимости от характеристик базовых данных, невозможно узнать точно, сколько места на диске и в памяти понадобится решению после обработки данных и использования их в запросах.  
  
 По оценкам многих разработчиков, для служб Analysis Services размер основного хранилища многомерной базы данных составляет около одной третьей размера исходных данных. В табличных базах данных иногда можно добиться большей степени сжатия, около одной десятой от исходного размера, особенно если большая часть данных импортируется из таблиц фактов.  
  
 **Размер модели и смещение ресурсов (в памяти или на диске)**  
  
 Размер базы данных служб Analysis Services ограничивается только ресурсами, доступными для ее запуска. Тип модели и режим хранения, помимо прочего, влияют на возможный размер базы данных.  
  
 Табличные базы данных выполняются в памяти или в режиме DirectQuery, который позволяет передать задачи выполнения запроса внешней базе данных. Для табличной выполняющейся в памяти аналитики база данных хранится в памяти, т. е. необходим достаточный объем памяти не только для загрузки всех данных, но и дополнительных структур данных, созданных для поддержки запросов.  
  
 Режим DirectQuery, улучшенный в этом выпуске, теперь накладывает меньше ограничений, а его производительность повышена. Использование серверной реляционной базы данных для хранения и выполнения запросов упрощает создание крупных табличных моделей.  
  
 В прошлом самыми крупными базами данных [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] были многомерные базы данных, в которых рабочие нагрузки обработки и запросов выполнялись независимо друг от друга на выделенном оборудовании, которое было оптимизировано для соответствующей задачи.  Табличные базы данных быстро догоняют эти типы баз данных, а улучшения DirectQuery помогают сократить зазор между ними.  
  
 Для многомерных баз данных разгрузка хранения данных и выполнения запросов доступна через ROLAP.   На сервере запросов наборы строк могут кэшироваться, а устаревшие могут удаляться из кэша. Эффективное и сбалансированное использование памяти и дисковых ресурсов часто приводит клиентов к многомерным решениям.  
  
 Под нагрузкой ожидается увеличение требований как к объему на диске, так и к объему памяти для каждого типа решения при выполнении кэширования, хранения, просмотра и запроса данных службами Analysis Services. Дополнительные сведения о параметрах подкачки памяти см. в разделе [Memory Properties](../analysis-services/server-properties/memory-properties.md). Дополнительные сведения о масштабе см. в разделе [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 В PowerPivot для Excel установлено искусственное ограничение размера файла в 2 гигабайта, цель которого состоит в том, чтобы книги, созданные в PowerPivot для Excel, можно было передавать в SharePoint, где устанавливается ограничение максимального размера передаваемых файлов. Одной из основных причин для переноса книги PowerPivot в табличное решение на автономном экземпляре служб Analysis Services является обход ограничения размера файла. Дополнительные сведения о настройке максимального размера передаваемого файла см. в разделе [Настройка максимального размера передаваемого файла (PowerPivot для SharePoint)](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Поддерживаемые источники данных**  
  
 Многомерные решения могут импортировать данные из реляционных источников данных, используя собственные и управляемые поставщики OLE DB.  
  
 В табличные модели можно импортировать данные из реляционных источников данных, веб-каналов данных и документов некоторых форматов. Кроме того, можно использовать поставщики OLE DB и ODBC с табличными моделями.  
  
 Список внешних источников данных, которые можно импортировать в модель каждого типа, см. в следующих разделах:  
  
-   [Поддерживаемые источники данных &#40;службы SSAS — многомерные базы данных&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [Поддерживаемые источники данных &#40;табличные службы SSAS&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a> Поддержка языков запросов и скриптов  
 Службы Analysis Services включают в себя языки многомерных выражений (MDX), расширений интеллектуального анализа данных (DMX), DAX, XML/A,ASSL и TMSL. Поддержка этих языков немного различается в зависимости от типа модели. Если необходимо учесть требования к языкам скриптов и запросов, просмотрите следующий список.  
  
-   В книгах Power Pivot для вычислений используется DAX, а для запросов — DAX или MDX.  
  
-   Табличный шаблон баз данных поддерживает вычисления DAX, запросы DAX и запросы многомерных выражений (MDX). Это справедливо на всех уровнях совместимости. Языки сценариев — ASSL (через XMLA) для уровней совместимости 1050–1103 и TMSL (через XMLA) для уровня совместимости 1200.  
  
-   Шаблоны базы данных многомерной модели поддерживают вычисления многомерных выражений и запросы многомерных выражений (MDX), а также ASSL.  
  
-   Модели интеллектуального анализа данных поддерживают расширения интеллектуального анализа данных и язык ASSL.  
  
-   Средство PowerShell для служб Analysis Services поддерживается в табличных и многомерных моделях и базах данных.  
  
 Все базы данных поддерживают XML/A. Дополнительные сведения см. в разделах [Справочник по языку запросов и выражений (службы Analysis Services)](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) и [Документация для разработчика служб Analysis Services](../analysis-services/analysis-services-developer-documentation.md).  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a> Функции безопасности  
 Все решения служб Analysis Services могут быть защищены на уровне базы данных. Более гранулярные параметры безопасности различаются в зависимости от режима. Если для вашего решения требуется точная настройка безопасности, просмотрите следующий список, чтобы убедиться, что нужный уровень защиты поддерживается в этом типе решения:  
  
-   Книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] защищаются на уровне файлов с использованием разрешений SharePoint.  
  
-   Табличный шаблон баз данных может использовать безопасность на уровне строк с применением разрешений на основе ролей в службах Analysis Services.  
  
-   В шаблонах баз данных многомерной модели может использоваться безопасность на уровне измерений и ячеек с использованием разрешений на основе ролей в службах Analysis Services.  
  
 Книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] могут быть восстановлены на сервер в табличном режиме. После восстановления файла он отсоединяется от SharePoint, что позволяет использовать все функции табличного моделирования, включая безопасность на уровне строк.  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a> Средства проектирования  
 Пользователи, задачей которых является построение аналитических моделей, могут обладать весьма разными навыками моделирования данных и техническим опытом. Если в конкретном решении имеет значение уровень владения тем или иным инструментом или опыт пользователя, сравните следующие направления подготовки в создании моделей.  
  
|Средство моделирования|Способ использования|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Используется для создания табличных, многомерных решений и решений интеллектуального анализа данных. В этой среде разработки используется оболочка Visual Studio для предоставления рабочих областей, панелей свойств и навигации по объектам. Технические специалисты, которые уже используют Visual Studio, скорее всего предпочтут этот инструмент для построения приложений бизнес-аналитики.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для Excel|Используется для создания книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , которую в дальнейшем можно развернуть на ферме SharePoint, содержащей установленный экземпляр [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для Excel обладает отдельной рабочей областью приложения, которая открывается поверх Excel. В ней используются те же визуальные метафоры (страницы со вкладками, макет сетки и строка формулы), что и в Excel. Пользователи, хорошо владеющие Excel, предпочтут этот инструмент среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a> Поддержка клиентских приложений  
 При использовании служб Reporting Services доступность функций отчетов различается в зависимости от выпусков и режимов сервера. По этой причине на выбор режима сервера для установки может повлиять то, отчеты какого типа вы намереваетесь строить.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], средство разработки для служб Reporting Services, которое работает в SharePoint, доступно на сервере отчетов, развернутом на ферме SharePoint 2010. Единственными типами источников данных, которые могут использоваться с этим отчетом, является табличный шаблон базы данных служб Analysis Services или книга [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Это значит, что для размещения источника данных, используемого этим типом отчета, необходим сервер, работающий в табличном режиме, или сервер [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint. Использовать многомерную модель в качестве источника данных для отчета [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] нельзя. Необходимо создать соединение с семантической моделью бизнес-аналитики [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] или общий источник данных служб Reporting Services в качестве источника данных для отчета [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 Построитель отчетов и конструктор отчетов могут использовать любую базу данных служб Analysis Services, включая книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , которые хранятся в [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint.  
  
 Отчеты в виде сводных таблиц Excel поддерживаются всеми базами данных служб Analysis Services. Функциональные возможности Excel аналогичны при использовании табличной базы данных, многомерной базы данных или книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , но обратная запись поддерживается только для многомерных баз данных.  
  
 Панели мониторинга PerformancePoint позволяют подключаться ко всем базам данных служб Analysis Services, включая книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Дополнительные сведения см. в разделе [Создание подключений к данным (службы PerformancePoint)](http://go.microsoft.com/fwlink/?linkdID=218155).  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a> Режимы развертывания сервера для многомерных и табличных решений  
 Экземпляр служб Analysis Services устанавливается в одном из трех режимов, которые задают контекст работы сервера. Режимом, в котором установлен сервер, определяется тип решений, которые могут быть развернуты на этом сервере. Основное различие между режимами состоит в архитектуре организации хранилища и использования памяти, но существуют также и другие различия. Три режима сервера кратко описаны в следующей таблице. Дополнительные сведения см. в разделе [Определение режима работы сервера экземпляра служб Analysis Services](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Режим развертывания|Описание|  
|---------------------|-----------------|  
|0 — многомерный режим и интеллектуальный анализ данных|Запуск многомерных решений и решений интеллектуального анализа данных, развертываемых вами на экземпляре служб Analysis Services по умолчанию. Режим развертывания 0 используется по умолчанию для установки служб Analysis Services.|  
|1 — [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint|В отношении доступа к данным [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] службы Analysis Services являются внутренним компонентом установки [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint. Службы Analysis Services устанавливается в режиме развертывания 1 и используются исключительно службами [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] в среде SharePoint.|  
|2 — табличные|Запуск табличных решений на автономном экземпляре служб Analysis Services, настроенном для режима развертывания 2.|  
  
 Подробнее см. в разделе [Установка служб Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md).  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a> Требования к SharePoint  
 SQL Server обеспечивает интеграцию с SharePoint, добавляя поддержку доступа к данным [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] и табличным данным. Затраты на интеграцию SharePoint и SQL Server растут при максимизации числа используемых функций каждого из продуктов. При наличии SharePoint можно установить SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для SharePoint, чтобы обеспечить доступ к данным [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] и получать BISM-файлы подключений [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , используемые для доступа к табличным базам данных, запущенным на внешнем экземпляре служб Analysis Services на сетевом сервере.  
  
 Отчеты Power View, в которых в качестве источника данных используются базы данных [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] и табличные базы данных, являются как компонентом SharePoint, предоставляемым SQL Server, так и встроенной функцией Excel. Хотя табличные базы данных выполняются на экземпляре служб Analysis Services за пределами SharePoint, эти данные потребляются отчетами Power View, работающими в SharePoint.  
  
 Если SharePoint не используется, для создания книг [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] можно по-прежнему использовать [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для Excel, но целостного процесса работы с представлением данных не будет. Каждый пользователь, работающий с книгой, должен скачать и просмотреть каждую из книг в Excel с помощью надстройки [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] для Excel, чтобы получить возможность взаимодействия с данными и их исследования с помощью срезов, фильтров и сведений. В противном случае представление книги будет ограничено статическими данными, как при открытии книги.  
  
 Табличные, многомерные решения и решения для интеллектуального анализа данных выполняются на экземплярах служб Analysis Services, при этом они не зависят от SharePoint.  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a> Поддержка программируемости и расширяемости  
 Хотя существует поддержка разработчиков для Power BI, ее нет для книг [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . При использовании книг [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] необходимо включить в решение встроенные клиентское и серверное приложения. Программирование Excel и программирование SharePoint — единственные варианты.  
  
 Сведения о Power BI см. в разделе [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/).  
  
 Табличные решения поддерживают только один файл model.bim на одно решение, а это означает, что вся работа должна быть выполнена в одном файле. При построении общего табличного решения группам разработки, привыкшим работать с несколькими проектами в одном решении, необходимо будет пересмотреть свой способ работы.  
  
 Табличные решения на уровне совместимости 1200 сопоставляются с новый объектной моделью, которая использует табличные метаданные. Старые табличные и многомерные модели используют многомерные метаданные как дескрипторы. Рекомендуется обновить старые табличные модели до уровня совместимости 1200, чтобы вы могли использовать табличные пространства имен в AMO для пользовательского кода и сценариев.  
  
 Дополнительные сведения см. в [документации служб Analysis Services для разработчиков](https://msdn.microsoft.com/library/bb500153.aspx) .  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a> Следующий шаг. Построение решения  
 Теперь, когда вы ознакомились с основными сведениями о сравнительных параметрах решений, попробуйте поработать со следующими учебниками для изучения этапов создания каждого из них. Далее приведены ссылки на учебники, в которых описываются нужные шаги.  
  
-   Создание модели [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]. Ознакомьтесь с разделом о [начале работы с Power Pivot в Microsoft Excel](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b).  
  
-   Создание табличной модели. См. раздел [Табличное моделирование &#40;учебник по Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
-   Создание многомерной модели. См. раздел [Многомерное моделирование &#40;учебник по Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Создание модели интеллектуального анализа данных. См. раздел [Учебник по основам интеллектуального анализа данных](../Topic/Basic%20Data%20Mining%20Tutorial.md).  
  
## <a name="see-also"></a>См. также  
 [Управление экземплярами служб Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Новые возможности в службах Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     
 [Новые возможности Power Pivot](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [Соединение семантической модели бизнес-аналитики PowerPivot &#40;BISM-файлы&#41;](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Создание общих источников данных и управление ими &#40;службы Reporting Services в режиме интеграции с SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  