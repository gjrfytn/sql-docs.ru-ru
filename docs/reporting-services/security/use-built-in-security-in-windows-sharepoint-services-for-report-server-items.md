---
title: "Использование встроенных средств безопасности служб Windows SharePoint Services при работе с элементами сервера отчетов | Microsoft Docs"
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
  - "разрешения [Reporting Services], режим интеграции с SharePoint "
  - "интеграция с SharePoint [Reporting Services], разрешения"
  - "безопасность [Reporting Services], режим интеграции с SharePoint"
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 14
---
# Использование встроенных средств безопасности служб Windows SharePoint Services при работе с элементами сервера отчетов
  Службы SharePoint предоставляют встроенные функции безопасности, которые можно использовать для доступа к элементам сервера отчетов с сайтов и из библиотек SharePoint. Если пользователям уже назначены разрешения на сайты и списки, они получат доступ к элементам и операциям сервера отчетов сразу после настройки параметров интеграции служб SharePoint и сервера отчетов.  
  
## Защищаемые элементы  
 Разрешения, определенные для веб-сайта или библиотеки, могут быть использованы, чтобы предоставить доступ к элементам сервера отчетов. Однако, если требуется защитить отдельные элементы, можно назначить разрешения для следующих типов содержимого.  
  
|Тип файла|Description|  
|---------------|-----------------|  
|RDL|Файл определения отчета, который определяет макет отчета и команды, используемые для получения данных. В определении отчета сведения о соединении с источником данных используются для получения данных при обработке отчета. Если определение отчета является нерегламентированным отчетом, созданным с помощью построителя отчетов, то этот отчет объединяется с SMDL-файлом модели отчета, который задает область просмотра данных в отчете, готовом для просмотра.|  
|SMDL|Файл модели отчета, в котором описаны структуры данных и их связи. Используется для подготовки и запуска отчетов построителя отчетов.|  
|RSDS|Общий источник данных, который определяет сведения о соединении с внешним источником данных. Он используется RDL-файлами определения отчета и SMDL-файлами модели отчета. Модели отчета всегда используют RSDS-файлы, чтобы получить сведения о соединении с базовым источником данных. Определения отчетов могут использовать RSDS-файлы или сведения о соединении, которые определены в свойствах источника данных отчета.|  
|RSC|Файл части отчета, который определяет макет и структуру элемента отчета или области данных. Используется для публикации элемента отчета на сервере, чтобы обеспечить повторное использование элемента другими авторами отчетов через галерею элементов отчетов.|  
|RSD|Файл общего набора данных, в котором определен синтаксис запросов и свойства для набора данных. Общие наборы данных могут совместно использоваться, храниться, обрабатываться и кэшироваться отдельно от отчета.|  
  
 Расписания, подписки и журнал отчета не являются защищаемыми элементами. Можно назначить разрешения на веб-сайт или библиотеки, которые определяют право пользователя создавать или использовать расписания, подписки и журнал отчета, но защитить эти элементы напрямую нельзя.  
  
 Чтобы защитить отдельные элементы, выберите элемент библиотеки, нажмите кнопку со стрелкой вниз и выберите пункт **Управление разрешениями**. В меню **Действия** выберите команду **Изменить разрешения**.  
  
## Использование встроенных групп и уровней разрешений для доступа к элементам сервера отчетов  
 Используя наследование разрешений и стандартные группы SharePoint, можно получить доступ к большинству операций сервера отчетов сразу после настройки параметров интеграции на сервере отчетов и в экземплярах служб SharePoint.  
  
 Службы SharePoint предоставляют стандартные группы, соответствующие заранее установленным уровням разрешений, которые определяют способы доступа к документам и страницам на сайте SharePoint. Если используются стандартные группы и уровни разрешений по умолчанию и сайты настроены для наследования разрешений, то использовать функции служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] можно следующими способами:  
  
|**Группы SharePoint**|**Уровень разрешений**|**Сводка**|**Доступ к серверу отчетов**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**Владельцы**|Полный доступ|Владельцы имеют полный набор разрешений на создание, управление и защиту элементов и операций сервера отчетов.|Устанавливают разрешения, которые управляют доступом ко всем элементам сервера отчетов, сохраненным во всех библиотеках веб-сайта. Устанавливают разрешения в модели отчета (также называются защитой элементов модели). Настраивают веб-часть «Средство просмотра отчетов». Добавляют отчеты и другие элементы в библиотеки. Изменяют свойства элементов для отчетов и других документов. Удаляют отчеты и другие элементы. Просмотр отчетов, в том числе отчетов, в которых для просмотра данных используются модели отчетов. Задание параметров отчетов. Задание параметров обработки отчета. Создают модели отчетов. Создают отчеты с помощью построителя отчетов. Создают и управляют общими источниками данных. Создают, изменяют и удаляют подписки, которыми владеют любые пользователи. Создают общие расписания веб-сайта и управляют ими. Создают версии документа и управляют ими, в том числе журналом отчета. Загружают файл источника для определения отчета или модели отчета. Заменяют определение отчета, модель отчета, общий источник данных или ресурс (с сохранением свойств и разрешений элемента).|  
|**Члены**|Участие|Члены могут создавать новые элементы и публиковать элементы отчетов и моделей из средств конструирования в библиотеке SharePoint.|Добавляют отчеты и другие элементы в библиотеки. Изменяют свойства элементов для отчетов и других документов. Удаляют отчеты и другие элементы. Просмотр отчетов, в том числе отчетов, в которых для просмотра данных используются модели отчетов. Просмотр предыдущих версий документа, а также моментальных снимков журнала отчета (при этом пользователю необходимо также разрешение на открытие отчета, для которого создан журнал отчета). Задание параметров отчетов. Задание параметров обработки отчета. Создают модели отчетов. Создают отчеты с помощью построителя отчетов. Создают и управляют общими источниками данных. Создают, изменяют и удаляют подписки, которыми владеют пользователи. Используют общие расписания с подпиской. Создают версии документа и управляют ими, в том числе журналом отчета. Загружают файл источника для определения отчета или модели отчета. Заменяют определение отчета, модель отчета, общий источник данных или ресурс (с сохранением свойств и разрешений элемента).|  
|**Посетители** и **Наблюдатели**|Чтение|Посетители могут просматривать отчеты|Просмотр отчетов, в том числе отчетов, в которых для просмотра данных используются модели отчетов.|  
  
 Если встроенные группы и уровни разрешений не используются, то для доступа к компонентам служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] необходимо назначить специальные разрешения. Дополнительные сведения см. в статье [Задание разрешений для работы сервера отчетов в веб-приложении SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## См. также  
 [Предоставление разрешений для элементов сервера отчетов на сайте SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Сравнение ролей и задач служб Reporting Services с группами и разрешениями SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Задание разрешений для работы сервера отчетов в веб-приложении SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Предоставление разрешений для элементов сервера отчетов на сайте SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  