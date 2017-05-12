---
title: "Занятие&#160;5. Проектирование родительского отчета с использованием мастера отчетов | Microsoft Docs"
ms.custom: ""
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# Занятие&#160;5. Проектирование родительского отчета с использованием мастера отчетов
После создания подключения к данным и таблицы данных для дочернего отчета следующий шаг состоит в проектировании дочернего отчета в конструкторе отчетов с помощью мастера отчетов. Дополнительные сведения о конструкторе отчетов см. в разделе [Разработка отчетов с использованием конструктора отчетов (SSRS)](../reporting-services/tools/design-reports-with-report-designer-ssrs.md).  
  
### Проектирование дочернего отчета с использованием мастера отчетов  
  
1.  Обязательно выберите в **обозревателе решений** веб-сайт верхнего уровня.  
  
2.  Щелкните правой кнопкой мыши веб-сайт и выберите пункт **Добавить новый элемент**.  
  
3.  В диалоговом окне **Добавление нового элемента** щелкните **Мастер отчетов**, введите имя файла отчета, а затем нажмите кнопку **Добавить**.  
  
    Запустится мастер отчетов.  
  
4.  На странице **Свойства набора данных** в поле **Источник данных** щелкните **DataSet2**.  
  
    Значение, указанное в поле **Доступные наборы данных**, автоматически изменится. В нем будет указана созданная ранее таблица данных.  
  
5.  Выберите **Далее**.  
  
6.  На странице **Размещение полей** выполните указанные ниже действия.  
  
    1.  Перетащите элементы **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty** и **StockedQty** из области **Доступные поля** в поле **Значения**.  
  
    2.  Щелкните стрелку рядом с элементами **Sum(ProductID)**, **Sum(PurchaseOrderID)**, **Sum(PurchaseOrderDetailID)**, **Sum(OrderQty)**, **Sum(ReceivedQty)**, **Sum(RejectedQty)** и **Sum(StockedQty)** и снимите выделение с **Sum**.  
  
7.  Дважды нажмите кнопку **Далее**, а затем нажмите кнопку **Готово**, чтобы закрыть окно **Мастер отчетов**.  
  
    В результате создается RDLC-файл. Файл откроется в конструкторе отчетов. Спроектированный вами табликс появится в области конструктора.  
  
8.  Добавьте в открытый RDLC-файл параметр, выполнив следующие действия.  
  
    1.  На панели **Данные отчета** щелкните **Параметры** правой кнопкой мыши, а затем нажмите кнопку **Добавить параметры**.  
  
    2.  Введите **productid** в поле **Имя**.  
  
    3.  В списке **Тип данных** должно быть выбрано значение **Integer**.  
  
    4.  Нажмите кнопку **ОК**.  
  
9. Сохраните RDLC-файл.  
  
## Следующая задача  
Тем самым с помощью мастера отчетов был успешно спроектирован дочерний отчет. Затем в приложение для веб-сайта необходимо добавить элемент управления ReportViewer. См. [Занятие 6. Добавление в приложение элемента управления ReportViewer](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md).  
  
  
  