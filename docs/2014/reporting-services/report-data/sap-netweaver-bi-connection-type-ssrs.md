---
title: Тип соединения SAP NetWeaver BI (службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b05c961fcd9d3a4a64715f6bc96754000969a6ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216884"
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>Тип соединения SAP NetWeaver BI (службы SSRS)
  Чтобы включить данные из внешнего источника данных SAP NetWeaver® Business Intelligence в отчет, необходимо иметь набор данных, основанный на источнике данных отчета типа [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]. Этот встроенный тип источника данных основан на модуле обработки данных для поставщика данных [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 1.0 для [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Этот модуль обработки данных позволяет получать многомерные данные из контейнеров InfoCube, MultiProvider (виртуальных контейнеров InfoCube) и запросов с поддержкой веб-доступа к внешнему источнику данных [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
 Используйте сведения в этом разделе для создания источника данных. Пошаговые инструкции см. в разделе [Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="support"></a> Поддерживаемые версии  
 Поставщик данных был разработан и проверен для работы с SAP BW 3.5 и 7.0.  
  
-   Поддержка пакета 20 для SAP BW 3.5 и 7.0  
  
 Для встроенной проверки подлинности Windows был разработан и протестирован поставщик для следующих систем.  
  
-   Пакет поддержки порталов 6.40 20 SAP  
  
-   Пакет поддержки 11 порталов SAP 7.0  
  
-   SAP Duet 1.0  
  
##  <a name="Connection"></a> Строка подключения  
 Свяжитесь с администратором базы данных, чтобы получить сведения о соединении и учетные данные, необходимые для соединения с источником данных. Приведенный ниже пример строки соединения задает подключение через Интернет с использованием протокола SOAP к источнику данных [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] на сервере, использующем порт 8000 и XML для аналитики:  
  
```  
DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 Дополнительные примеры строк соединения см. в разделе [Подключения к данным, источники данных и строки подключения в построителе отчетов](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a> Учетные данные  
 Учетные данные необходимы для запуска запросов, локального предварительного просмотра отчетов, а также для предварительного просмотра отчетов на сервере отчетов.  
  
 После публикации отчета может понадобиться изменить учетные данные источника данных, чтобы разрешения, необходимые для получения данных при запуске отчета на сервере отчетов, были допустимыми.  
  
 Дополнительные сведения см. в разделе [подключения к данным, источники данных и строки подключения в службах Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) или [указание учетных данных в построителе отчетов](../specify-credentials-in-report-builder.md).  
  
  
  
##  <a name="Query"></a> Запросы  
 Для построения запроса многомерного выражения с помощью просмотра базовых структур данных в источнике данных можно использовать графический конструктор запросов в режиме конструктора или в режиме запроса. Чтобы увидеть результаты запроса во время конструирования, его можно запустить из конструктора запросов в интерактивном режиме. Построенный запрос определяет поля в наборе данных. Во время выполнения источник данных возвращает действительные данные. Для выполнения следующих действий используйте графический конструктор запросов.  
  
-   Для построения запроса многомерного выражения в режиме конструктора перетащите измерения, элементы, свойства элементов и ключевые числа из источника данных в панель «Данные». Перетащите вычисляемые элементы с панели «Вычисляемые элементы» на панель «Данные», чтобы определить дополнительные поля наборов данных.  
  
-   В режиме запроса перетащите измерения, элементы, свойства элементов и ключевые числа в панель «Запрос» или непосредственно введите в ней текст многомерного выражения. Перетащите вычисляемые элементы с панели «Вычисляемые элементы» на панель «Данные», чтобы определить дополнительные поля наборов данных.  
  
 При построении запросов конструктор запросов автоматически добавляет к запросу многомерных выражений свойства по умолчанию. Чтобы помимо свойств по умолчанию включить другие свойства, запрос многомерных выражений нужно изменить вручную.  
  
 Дополнительные сведения о соответствующем конструкторе запросов см. в разделе [Пользовательский интерфейс конструктора запросов SAP NetWeaver BI (построитель отчетов)](../sap-netweaver-bi-query-designer-user-interface-report-builder.md).  
  
  
  
##  <a name="Extended"></a> Расширенные свойства поля  
 Источник данных [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] поддерживает расширенные свойства полей. Расширенные свойства полей — свойства в дополнение к `Value` и `IsMissing` , заданные для поля набора данных с помощью модуля обработки данных. Расширенные свойства включают стандартные свойства и пользовательские. Стандартные свойства — это свойства, общие для многих источников данных. Пользовательские свойства уникальны для каждого источника данных.  
  
### <a name="working-with-field-properties"></a>Работа со свойствами полей  
 Расширенные свойства полей не отображаются в области данных отчета как элементы, которые можно перетащить в макет отчета. Вместо этого вы перетаскиваете в отчет родительское поле свойства и затем меняете свойство по умолчанию с `Value` к свойству, вы хотите использовать. Например, если имя поля **Calendar Year/Month Level 01** создается в конструкторе запросов многомерных выражений путем перетаскивания из панели метаданных в панель запросов, в каком-то выражении вы ссылаетесь на дополнительное пользовательское свойство **Длинное имя** с помощью следующего синтаксиса:  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 Имя расширенного свойства поля появляется в подсказке, когда вы наводите курсор мыши на любое поле в панели метаданных. Дополнительные сведения о конструкторах запросов, можно использовать для просмотра базовых данных, см. в разделе [пользовательский интерфейс конструктора запросов SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Значения для расширенных свойств полей существуют только в случае, если источник данных предоставляет их в то время, когда создается отчет и извлекаются данные для наборов данных. Затем можно ссылаться на эти `Field` значения свойств из любого выражения с помощью синтаксиса, описанного ниже. Но поскольку эти поля относятся только к этому поставщику данных и не являются частью языка определения отчетов, изменения в этих значениях не сохраняются вместе с определением отчета.  
  
 Для ссылки на стандартные расширенные свойства используйте одно из следующих выражений:  
  
-   *Fields!ИмяПоля.ИмяСвойства*  
  
-   *Fields!ИмяПоля("ИмяСвойства")*  
  
 Для обращения к пользовательским расширенным свойствам в выражении применяется следующий синтаксис:  
  
-   *Fields!ИмяПоля("ИмяСвойства")*  
  
  
  
### <a name="predefined-field-properties"></a>Стандартные свойства полей  
 В следующей таблице представлен список стандартных свойств поля, которые можно использовать для источника данных [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
|**Свойство**|**Тип**|**Описание или ожидаемое значение**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Указывает значение данных поля.|  
|`IsMissing`|`Boolean`|Указывает, найдено ли поле в результирующем наборе данных.|  
|`FormattedValue`|`String`|Возвращает форматированное значение для ключевой цифры.|  
|`BackgroundColor`|`String`|Возвращает цвет фона, заданный в базе данных для этого поля.|  
|`Color`|`String`|Возвращает цвет переднего плана, заданный в базе данных для этого элемента.|  
|`Key`|`Object`|Возвращает ключ для уровня.|  
|`LevelNumber`|`Integer`|Для иерархий типа «родители-потомки» возвращает номер уровня или измерения.|  
|`ParentUniqueName`|`String`|Для иерархий типа «родители-потомки» это свойство возвращает полное имя родительского уровня.|  
|`UniqueName`|`String`|Возвращает полное имя уровня. Например `UniqueName` значение для сотрудника может быть *[0D_Company]. [ 10D_Department]. [11]* .|  
  
 Дополнительные сведения об использовании полей и свойств полей в выражении см. в разделе [Встроенные коллекции в выражениях (построитель отчетов и службы SSRS)](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
  
##  <a name="Remarks"></a> Замечания  
 Этот поставщик данных поддерживает не все режимы доставки отчетов. Доставка отчетов с помощью управляемых данными подписок для этого модуля обработки данных не предусмотрена. Дополнительные сведения см. в разделе [Использование внешнего источника данных для данных подписчика (управляемая данными подписка)](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Дополнительные сведения см. в разделе [Использование служб SQL Server 2008 Reporting Services совместно с SAP NetWeaver Business Intelligence](http://go.microsoft.com/fwlink/?LinkId=167352).  
  
  
  
##  <a name="HowTo"></a> Инструкции  
 В этом разделе содержатся пошаговые инструкции по работе с подключениями к данным, источниками данных и наборами данных.  
  
 [Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Добавление фильтра к набору данных (построитель отчетов и службы SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> См. также  
 В этих разделах документации содержатся подробные сведения о данных отчетов, а также методические сведения об определении, настройке и использовании элементов отчетов, связанных с данными.  
  
 [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-datasets-ssrs.md)  
 Предоставляет общие сведения о доступе к данным отчета.  
  
 [Подключения к данным, источники данных и строки подключения в построителе отчетов](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Предоставляет сведения о подключениях к данным и источникам данных.  
  
 [Внедренные и общие наборы данных отчета (построитель отчетов и службы SSRS)](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Предоставляет сведения об общих и внедренных наборах данных.  
  
 [Коллекция полей набора данных (построитель отчетов и службы SSRS)](dataset-fields-collection-report-builder-and-ssrs.md)  
 Предоставляет сведения о коллекции полей набора данных, создаваемой запросом.  
  
 [Источники данных, поддерживаемые службами Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
 Предоставляет подробные сведения о поддержке платформ и версий для каждого модуля обработки данных.  
  
 
  
## <a name="see-also"></a>См. также  
 [Параметры отчета (построитель отчетов и конструктор отчетов)](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Фильтрация, группирование и сортировка данных (построитель отчетов и службы SSRS)](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Выражения (построитель отчетов и службы SSRS)](../report-design/expressions-report-builder-and-ssrs.md)  
  
  