---
title: "Настройка свойств выполнения для отчета (диспетчер отчетов) | Microsoft Docs"
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
helpviewer_keywords: 
  - "свойства выполнения отчета [службы Reporting Services]"
  - "отчеты [службы Reporting Services], свойства"
  - "отчеты [службы Reporting Services], параметры выполнения"
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
caps.latest.revision: 41
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 41
---
# Настройка свойств выполнения для отчета (диспетчер отчетов)
  Параметры обработки отчета можно настроить для указания получения данных для отчета. Планирование обработки данных для отчета становится целесообразным, если обновление внешнего источника данных происходит в определенные моменты времени (пример: хранилище данных, которое обновляется ежедневно или еженедельно) и необходимо избежать издержек, связанных с выборкой одних и тех же данных при каждом запросе отчета. Планирование обработки данных становится также необходимым, если требуется управлять рабочей нагрузкой сервера внешней базы данных или обеспечить предоставление согласованных результатов для многочисленных пользователей, которым приходится работать с идентичными наборами данных. Для быстро изменяющихся данных отчеты по требованию могут каждую минуту выдавать различные результаты. Моментальный снимок отчета, напротив, позволяет сопоставить данные различных отчетов и средств аналитики, действительные на один и тот же момент времени.  
  
 Моментальный снимок отчета — это отчет, содержащий инструкции макета и результаты запроса, полученные в определенный момент времени. В отличие от отчетов по требованию, при открытии которых производится получение актуальных, действительных на текущий момент данных, моментальные снимки отчета выполняются по расписанию и сохраняются на сервере отчетов. Если для просмотра выбирается моментальный снимок отчета, сервер отчетов извлекает сохраненный отчет из базы данных сервера отчетов и отображает макет и данные, которые были действительны на момент создания моментального снимка.  
  
 Моментальные снимки отчета не сохраняются в каком-то определенном формате отображения, а преобразуются в него (например, в HTML) только при запросе пользователя или приложения. Отложенное форматирование делает моментальные снимки отчетов переносимыми, поскольку отчет может быть сформирован для просмотра в формате, необходимом для веб-браузера или другого устройства отображения.  
  
### Настройка параметров обработки отчета  
  
1.  Запустите [диспетчер отчетов (службы SSRS в собственном режиме)](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Перейдите и откройте отчет, для которого необходимо настроить параметры обработки.  
  
 Подведите курсор к отчету и щелкните стрелку раскрывающегося списка.  
  
1.  В раскрывающемся меню выберите **Управление**, а затем вкладку **Параметры обработки**.  
  
2.  Щелкните **Подготовить этот отчет для просмотра, используя снимок состояния выполнения отчета**, а затем выберите один из следующих параметров.  
  
    -   Если необходимо создать моментальный снимок, выберите **Использовать следующее расписание создания снимков состояния выполнения отчета** и либо определите расписание для отчета, либо выберите расписание из списка **Общее расписание**.  
  
    -   Если нужно создать моментальный снимок немедленно, выберите **Создать моментальный снимок отчета при нажатии кнопки «Применить» на этой странице**.  
  
3.  Нажмите кнопку **Применить**.  
  
## См. также  
 [Установка свойств обработки отчетов](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Открытие и закрытие отчетов (диспетчер отчетов)](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Страница "Содержимое" (диспетчер отчетов)](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Управление содержимым сервера отчетов (службы Reporting Services в основном режиме)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Страница "Свойства параметров обработки" (диспетчер отчетов)](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md)  
  
  