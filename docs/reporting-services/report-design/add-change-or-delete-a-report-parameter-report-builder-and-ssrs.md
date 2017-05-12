---
title: "Добавление, изменение или удаление параметра отчета (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Добавление, изменение или удаление параметра отчета (построитель отчетов и службы SSRS)
  Параметры отчета позволяют выбирать данные отчета, соединять связанные отчеты и изменять представление отчета. Можно предоставить значения по умолчанию и список доступных значений, чтобы пользователи могли их изменять.  
  
 После публикации отчета на сервере отчетов можно изменить значения по умолчанию, доступные значения и другие свойства параметров отчета. Для параметра можно предоставить несколько наборов значений по умолчанию, создав связанные отчеты. Дополнительные сведения см. в разделе [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Эта статья содержит сведения о добавлении параметров отчета для разбитого на страницы отчета в [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] или конструктор отчетов в [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Кроме того, можно добавлять параметры отчета для мобильных отчетов в  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]. Подробнее см. в разделе [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Добавление или изменение параметра отчета  
  
1.  В области **Данные отчета** [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] или конструктора отчетов в [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] щелкните правой кнопкой мыши узел **Параметры** и выберите **Добавить параметр**. Откроется диалоговое окно **Свойства параметра отчета** .  
  
2.  В поле **Имя**введите имя параметра или примите имя по умолчанию.  
  
3.  В поле **Запрос**введите текст, отображаемый рядом с текстовым полем параметра при запуске отчета.  
  
4.  В поле **Тип данных**выберите тип данных для значения параметра.  
  
5.  Если параметр может содержать пустое значение, выберите **Разрешить пустое значение**.  
  
6.  Если параметр может содержать значение NULL, выберите **Разрешить значение NULL**.  
  
7.  Чтобы разрешить пользователю выбирать несколько значений параметра, выберите **Разрешить несколько значений**.  
  
8.  Укажите параметр видимости.  
  
    -   Чтобы отобразить параметр на панели инструментов в верхней части отчета, выберите **Видимый**.  
  
    -   Чтобы скрыть параметр и не отображать его на панели инструментов, выберите **Скрытый**.  
  
    -   Чтобы скрыть параметр и защитить его от изменений на сервере отчетов после публикации, выберите **Внутренний**. Этот параметр отчета можно будет просмотреть только в определении отчета. Для этого параметра необходимо указать значение по умолчанию или разрешить ему принимать значения NULL.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Удаление параметра отчета  
  
1.  В области **Данные отчета** разверните узел **Параметры** .  
  
2.  Щелкните правой кнопкой мыши параметр отчета и выберите команду **Удалить**.  
  
## См. также  
 [Добавление, изменение и удаление допустимых значений параметра отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add, change, or delete available values for a report parameter.md)   
 [Добавление, изменение или удаление значения по умолчанию для параметра отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add, change, or delete default values for a report parameter.md)   
 [Изменение порядка параметров отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Добавление каскадных параметров в отчет (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Учебник. Добавление параметра к отчету (построитель отчетов)](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Добавление фильтров набора данных, фильтров области данных и групповых фильтров (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add dataset filters, data region filters, and group filters.md)   
 [Ссылки на коллекцию параметров (построитель отчетов и службы SSRS)](../../reporting-services/report-design/parameters-collection-references-report-builder-and-ssrs.md)   
 [Добавление в отчет параметра с несколькими значениями](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  