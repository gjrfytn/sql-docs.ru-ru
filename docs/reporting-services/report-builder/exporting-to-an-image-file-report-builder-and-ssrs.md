---
title: "Экспорт в файл изображения (построитель отчетов и службы SSRS) | Microsoft Docs"
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
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
caps.latest.revision: 12
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 11
---
# Экспорт в файл изображения (построитель отчетов и службы SSRS)
  Модуль подготовки отчетов изображений преобразует отчет с разбиением на страницы в битовую карту или метафайл. По умолчанию модуль подготовки изображения создает отчет в файле TIFF, который можно просматривать на нескольких страницах. Полученное изображение клиент может просмотреть в программе просмотра изображений и распечатать. В этом разделе содержатся сведения о модуле подготовки изображений и описаны исключения из правил подготовки к просмотру.  
  
 Модуль подготовки изображений способен создавать файлы в любых форматах, поддерживаемых [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG и TIFF. Если используется формат TIFF, то файлу для главного потока будет присвоено имя *имя_отчета*.tif. Для других форматов, которые формируются по принципу "одна страница в одном файле", файлу будет присвоено имя *имя_отчета_страница.ext*, где *ext* — расширение файла в зависимости от выбранного формата. Чтобы создать файл в другом поддерживаемом формате изображений, укажите в параметре **OutputFormatDeviceInfo** любую из перечисленных выше строк.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> Поддерживаемые форматы изображения  
 В следующей таблице приведены расширения имени файла и тип MIME для каждого формата модуля подготовки изображений.  
  
|**Тип**|**Расширение**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|bmp|image/bmp|  
|GIF|gif|image/gif|  
|JPEG|jpeg|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|emf|image/emf|  
|EMFPlus|emf|image/emf|  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="RenderingMultiplePages"></a> Подготовка к просмотру нескольких страниц  
 TIFF — это единственный формат, который позволяет представлять многостраничные документы в едином файле. Другие форматы, такие как JPG или PNG, выводят по одной странице одновременно и требуют отдельного вызова модуля подготовки отчетов для подготовки к просмотру каждой страницы.  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="Interactivity"></a> Интерактивность  
 Интерактивные возможности не поддерживаются ни одним из форматов изображения, формируемых этим модулем подготовки отчетов. Не обрабатываются следующие интерактивные элементы.  
  
-   Гиперссылки  
  
-   Показать или скрыть  
  
-   Схема документа  
  
-   Ссылки с детализацией или дополнительной информацией  
  
-   Сортировка конечным пользователем  
  
-   Фиксированные заголовки  
  
-   Закладки  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="DeviceInfo"></a> Настройки сведений об устройстве  
 Некоторые параметры по умолчанию для этого модуля подготовки отчетов можно изменить через настройку сведений об устройстве. Дополнительные сведения см. в разделе [Image Device Information Settings](../../reporting-services/image-device-information-settings.md).  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
## См. также раздел  
 [Разбиение на страницы в службах Reporting Services (построитель отчетов и службы SSRS)](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Поведение при подготовке к просмотру (построитель отчетов и службы SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Интерактивные возможности различных модулей подготовки отчетов к просмотру (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/interactive functionality - different report rendering extensions.md)   
 [Подготовка к просмотру элементов отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Таблицы, матрицы и списки (построитель отчетов и службы SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  