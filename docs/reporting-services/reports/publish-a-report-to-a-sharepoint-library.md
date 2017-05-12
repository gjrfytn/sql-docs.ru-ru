---
title: "опубликовать отчет в библиотеке SharePoint | Microsoft Docs"
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
helpviewer_keywords: 
  - "развертывание [службы Reporting Services], отчеты в режиме интеграции с SharePoint"
  - "интеграция с SharePoint [службы Reporting Services], публикация в библиотеке"
  - "публикация отчетов [службы Reporting Services], в библиотеке SharePoint"
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# опубликовать отчет в библиотеке SharePoint
  Чтобы опубликовать отчет на сайте SharePoint, настроенном для интеграции с SharePoint, необходимо задать свойства проекта в конструкторе отчетов. В свойствах проекта все ссылки на серверы, отчеты и общие источники данных следует указывать в виде полных URL-адресов. В определении отчета все ссылки на вложенные отчеты, детализированные отчеты и такие ресурсы, как изображения, расположенные в Интернете, должны представлять собой полные URL-адреса.  
  
 Необходимо обладать разрешением **Член** или **Владелец** на сайте SharePoint для задания свойств проекта. Дополнительные сведения см. в разделе [Примеры URL-адресов для элементов опубликованного отчета на сервере отчетов в режиме SharePoint (службы SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### Публикация отчета на сайте SharePoint  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте существующий или новый проект сервера отчетов.  
  
2.  В меню **Проект** выберите пункт **Свойства**. Открывается диалоговое окно **Страницы свойств***\<проект>*.  
  
3.  В списке **Конфигурация** выберите имя конфигурации сборки решения, предназначенной для формирования и публикации отчета. Текущая конфигурация представлена в списке как **Активная**(*\<configuration>*).  
  
4.  Если в проекте публикуются общие источники данных и перезаписываются ранее опубликованные общие источники данных, присвойте свойству **OverwriteDataSources** значение **True**.  
  
5.  В качестве значения свойства **TargetDataSourceFolder** введите URL-адрес библиотеки SharePoint или папки библиотеки (например, *http://Тестовый_сервер/Тестовый_сайт/Документы/Источники_данных*) (необязательно).  
  
     Если значение не указано, то будет использовано значение свойства **TargetReportFolder** .  
  
6.  В качестве значения свойства **TargetReportFolder** введите URL-адрес библиотеки или папки библиотеки (например, *http://Тестовый_сервер/Тестовый_сайт/Документы/Отчеты*).  
  
7.  В поле **TargetServerURL** введите URL-адрес сайта SharePoint верхнего уровня или дочернего сайта. Если сайт не указан, используется сайт верхнего уровня по умолчанию (например, *http://имя_сервера*, *http://имя_сервера/сайт* или *http://имя_сервера/сайт/вложенный_сайт*).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. В обозревателе решений щелкните правой кнопкой мыши отчет, который необходимо опубликовать, и выберите команду **Развернуть**. Отчет будет опубликован в местоположении, которое указано в свойстве **TargetReportFolder**. Ошибки развертывания появляются в окне «Вывод».  
  
## См. также  
 [Диалоговое окно страниц свойств проекта](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Задание свойства развертывания (службы Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Публикация отчетов на сервере отчетов](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Примеры URL-адресов для элементов опубликованного отчета на сервере отчетов в режиме SharePoint (службы SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Использование ODC-файла подключения к данным Office в отчетах (службы Reporting Services в режиме интеграции с SharePoint)](../../reporting-services/report-data/use an office data connection (.odc) with reports.md)  
  
  