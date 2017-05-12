---
title: "Установка свойств обработки отчетов | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "отчеты по требованию"
  - "обработка отчетов [службы Reporting Services], свойства выполнения"
  - "моментальные снимки [службы Reporting Services], выполнение отчетов"
  - "кэшированные отчеты [службы Reporting Services]"
  - "моментальные снимки отчетов [службы Reporting Services], выполнение отчетов"
  - "моментальные снимки выполнения отчета [службы Reporting Services]"
ms.assetid: b5cbc453-5986-423e-af44-1f243ef3edb1
caps.latest.revision: 43
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 43
---
# Установка свойств обработки отчетов
  Свойства выполнения отчета определяют, как отчет обрабатывается. Свойства выполнения должны быть установлены для каждого отчета отдельно.  
  
 Чтобы настроить свойства выполнения отчета, откройте отчет в диспетчере отчетов, а затем перейдите к странице свойств «Выполнение». Дополнительные сведения см. в статье [Страница "Обработка свойств параметров" (диспетчер отчетов)](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md). Установить свойства можно также с помощью среды [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], см. статью [Страница "Свойства параметров обработки" (диспетчер отчетов)](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md).  
  
## Режимы выполнения отчета  
 Отчет можно запустить либо по требованию, либо как моментальный снимок. Далее описываются оба этих подхода.  
  
### Выполнение отчетов по требованию  
 Можно определить, что отчет запрашивает источник данных каждый раз, когда пользователь выполняет отчет, что приведет к созданию отчетов по требованию, содержащих наиболее свежие данные. Для каждого пользователя, открывающего или запрашивающего отчет, создается новый экземпляр отчета; каждый из них содержит результаты нового запроса. При таком подходе, если отчет одновременно откроют десять пользователей, источнику данных будет отправлено для обработки десять запросов.  
  
### Выполнение отчетов по требованию из кэша  
 Для лучшей производительности можно указать, что отчет (и данные) должны временно кэшироваться, когда пользователь выполняет отчет. В дальнейшем кэшированная копия будет доступна для других пользователей, обращающихся к тому же отчету. При таком подходе, если отчет одновременно откроют десять пользователей, только первый запрос приведет к обработке отчета. Затем отчет будет кэширован, и остальные девять пользователей увидят кэшированный отчет.  
  
 Отчеты удаляются из кэша через заданные интервалы. Интервал можно указывать в минутах или задать определенную дату и время очистки кэша. Дополнительные сведения см. в разделе [Кэширование отчетов (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### Выполнение отчетов из моментальных снимков  
 Моментальный снимок отчета представляет собой отчет, который содержит сведения о макете отчета и данные, полученные в определенный момент времени. Отчет можно выполнять как моментальный снимок отчета, чтобы предотвратить его выполнение в произвольные моменты времени (например, во время резервного копирования по расписанию). Обычно моментальный снимок отчета создается и в дальнейшем обновляется по расписанию, что позволяет точно планировать время, когда будет выполняться обработка отчета и данных. Если отчет основан на запросах, требующих длительного выполнения, или на запросах, использующих данные из источника данных, доступ к которому в определенные часы желательно запретить, отчет следует выполнять как моментальный снимок.  
  
 Моментальный снимок отчета сохраняется в базе данных сервера отчетов и в дальнейшем, когда пользователь или процесс (например, подписка) запрашивает его, получается из этой базы данных. При обновлении моментального снимка отчета происходит запись нового экземпляра поверх старого. Сервер отчетов не сохраняет предыдущих версий моментальных снимков отчетов, за исключением случая, когда параметры специально настроены, чтобы добавлять его в журнал отчета. Дополнительные сведения см. в статье [Создание, изменение и удаление моментальных снимков в журнале отчетов](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
  
 Не все запросы можно настроить для выполнения в режиме моментального снимка. Невозможно создать моментальный снимок для отчета, запрашивающего учетные данные у пользователя или использующего для этого встроенную безопасность Windows для получения данных отчета. Если необходимо выполнить в режиме моментального снимка параметризованный отчет, следует указать параметр по умолчанию, чтобы он использовался при создании моментального снимка. В отличие от отчетов, выполняемых по запросу, невозможно после открытия отчета указать другое значение параметра. Выбор иного значения параметра приведет к новому запросу на обработку отчета, что не допускается.  
  
 В некоторых случаях можно настроить отчет по требованию, чтобы он выполнялся в режиме моментального снимка, может привести к отключению подписок. Сервер отчетов отключит существующие подписки, определенные в то время, когда отчет был настроен для выполнения по требованию, если возникнет следующее условие.  
  
-   В отчете используются параметры запросов, поэтому, чтобы выполнить требования для выполнения отчета в режиме моментального снимка, в качестве параметра по умолчанию выбрано конкретное значение.  
  
-   Существующие подписки настроены так, что используют значения параметров, отличные от заданного для моментального снимка значения параметра по умолчанию.  
  
 Если выполняется это условие, сервер отчетов отключит подписку в следующий раз, когда она должна выполняться по расписанию. Для повторного включения подписки откройте, а затем сохраните ее. При открытии подписки сервер отчетов обновляет значения параметров подписки теми, что указаны для моментального снимка. Дополнительные сведения о подписках см. в разделе [Подписки и доставка (службы Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## См. также  
 [Установка параметров обработки (службы Reporting Services в режиме интеграции с SharePoint)](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Настройка свойств выполнения для отчета (диспетчер отчетов)](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Основные понятия служб Reporting Services (SSRS)](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Добавление моментального снимка в журнал отчета](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Задание учетных данных и сведениях о соединении для источников данных отчета](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  