---
title: "Добавление датчика в отчет (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Добавление датчика в отчет (построитель отчетов и службы SSRS)
  Если в отчете с разбиением на страницы [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] необходимо создать сводку данных в визуальном формате, то можно использовать область данных "Датчик". После добавления области данных датчика в область конструктора можно перетаскивать поля набора данных отчета на панель данных в датчике.  
  
## Добавление датчика в отчет  
  
1.  Создайте отчет или откройте существующий отчет.  
  
2.  На вкладке «Вставка» дважды щелкните «Датчик». Откроется диалоговое окно **Выбор типа датчика** .  
  
3.  Выберите тип датчика, который нужно добавить в отчет. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  В отличие от диаграмм, для датчиков существует только два типа: линейный и радиальный. В диалоговом окне **Выбор типа датчика** представлены шаблоны этих двух типов датчиков. По этой причине нельзя производить изменение типа датчика после его добавления в отчет. Чтобы изменить его тип, нужно удалить и вновь добавить датчик.  
  
     Если в отчете нет источника данных и набора данных, то откроется диалоговое окно **Свойства источника данных** , которое поможет выполнить шаги для их создания. Дополнительные сведения см. в разделе [Добавление и проверка подключения к данным (построитель отчетов и службы SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
     Если в отчете есть источник данных, но нет набора данных, то откроется диалоговое окно **Свойства набора данных** , которое поможет выполнить шаги для его создания. Дополнительные сведения см. в разделе [Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
4.  Щелкните датчик, чтобы отобразить панель данных. По умолчанию датчик имеет один указатель, соответствующий одному значению. Можно добавить дополнительные указатели.  
  
5.  Добавьте одно поле из набора данных в область добавления поля данных. Можно добавить только одно поле. Если необходимо добавить несколько полей, необходимо добавить несколько указателей, по одному для каждого поля.  
  
     Щелкните правой кнопкой мыши шкалу датчика и выберите пункт **Свойства шкалы**. Введите для шкалы значения **Минимум** и **Максимум** . Дополнительные сведения см. в разделе [Установка минимума и максимума на датчике (построитель отчетов и службы SSRS)](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
## См. также  
 [Вложенные области данных (построитель отчетов и службы SSRS)](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Датчики (построитель отчетов и службы SSRS)](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  