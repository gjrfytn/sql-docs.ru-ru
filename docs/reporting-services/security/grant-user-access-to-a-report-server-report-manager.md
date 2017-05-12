---
title: "Предоставление пользователям доступа к серверу отчетов (диспетчер отчетов) | Microsoft Docs"
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
  - "удаление назначений ролей"
  - "разрешения [службы Reporting Services], предоставление доступа к серверу отчетов"
  - "роли [службы Reporting Services], назначения"
  - "изменение назначений ролей"
  - "удаление назначений ролей"
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: 54
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 54
---
# Предоставление пользователям доступа к серверу отчетов (диспетчер отчетов)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для предоставления пользователям доступа к серверу отчетов используют безопасность на основе ролей. При новой установке сервера отчетов только пользователи, являющиеся членами локальной группы администраторов, имеют разрешения на доступ с содержимому и операциям сервера отчетов. Чтобы сделать сервер отчетов доступным для других пользователей, необходимо создать назначения ролей, которые будут сопоставлять учетную запись пользователя или группы с конкретной стандартной ролью, определяющей некоторый набор задач.  
  
 **Серверы отчетов в режиме интеграции с SharePoint.** Для сервера отчетов, настроенного для работы в режиме интеграции с SharePoint, доступ к веб-сайту SharePoint настраивается с помощью разрешений SharePoint. Уровни разрешений на сайте SharePoint определяют доступ к содержимому и операциям сервера отчетов. Для предоставления разрешений на веб-сайте SharePoint необходимо быть администратором веб-сайта. Дополнительные сведения см. в разделе [Предоставление разрешений для элементов сервера отчетов на сайте SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
 **Серверы отчетов в основном режиме.** Эта статья посвящена серверу отчетов, настроенному для работы в основном режиме, и назначению пользователей ролям с помощью диспетчера отчетов. Существует два типа ролей.  
  
-   Роли на уровне элементов используются для просмотра, добавления и управления содержимым сервера отчетов, подписками, обработкой отчетов и журналами отчетов. Роли на уровне элементов определяются в корневом узле (корневой папке) или в заданных папках или последующих элементах иерархии.  
  
-   Системные роли предоставляют доступ к операциям на уровне веб-сайта, не привязанным к конкретным элементам. Примером может служить использование построителя отчетов и общих расписаний.  
  
     Эти два типа ролей дополняют друг друга и должны использоваться вместе. По этой причине добавление пользователя к серверу отчетов является двусоставной операцией. Если пользователь присваивается роли на уровне элементов, его также следует присвоить системной роли. При присвоении пользователя роли необходимо выбирать уже определенную роль. Создание, изменение и удаление ролей производится в среде [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Дополнительные сведения см. в разделе [Создание, удаление и изменение ролей (среда Management Studio)](../../reporting-services/security/create-delete-or-modify-a-role-management-studio.md).  
  
## Перед началом  
 Перед добавлением пользователя к серверу отчетов, работающему в собственном режиме, ознакомьтесь со следующим списком.  
  
-   Необходимо быть членом локальной группы администраторов на компьютере сервера отчетов. Если службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] разворачиваются в [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] или Windows Server 2008, требуется дополнительная настройка перед тем, как можно будет локально администрировать сервер отчетов. Дополнительные сведения см. в статье [Настройка сервера отчетов, работающего в собственном режиме, для локального администрирования (SSRS)](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
-   Чтобы делегировать эту задачу другим пользователям, создайте назначения ролей, сопоставляющие учетные записи пользователей с ролями «Диспетчер содержимого» и «Системный администратор». Пользователи, имеющие разрешения диспетчера содержимого и системного администратора, могут добавлять пользователей к серверу отчетов.  
  
-   В среде [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]просмотрите стандартные системные и пользовательские роли, чтобы ознакомиться с задачами, которые они могут выполнять. Описания задач скрыты в диспетчере отчетов, поэтому перед тем, как начать добавлять пользователей, нужно знать задачи ролей.  
  
-   При необходимости настройте роли или добавьте дополнительные роли для включения набора нужных задач. Например, если для отдельных элементов планируется применять пользовательские параметры безопасности, можно создать новое определение роли, позволяющей пользователям просматривать папки.  
  
### Добавление пользователя или группы к системной роли  
  
1.  Запустите [диспетчер отчетов (службы SSRS в собственном режиме)](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Щелкните элемент **Настройки сайта**.  
  
3.  Перейдите на вкладку **Безопасность**.  
  
4.  Нажмите кнопку **Создать назначения ролей**.  
  
5.  В поле **Имя группы или пользователя** введите учетную запись пользователя или группы домена Windows в следующем формате: \<домен>\\<учетная_запись\>. Если используется проверка подлинности с помощью форм или пользовательский модуль безопасности, задайте учетную запись пользователя или группы в формате, допустимом для развертывания.  
  
6.  Выберите системную роль и нажмите кнопку **ОК**.  
  
     Роли обладают качеством совокупности, поэтому, если одновременно выбрать роли системного администратора и системного пользователя, группа или пользователь смогут выполнять задачи обеих ролей.  
  
7.  Создайте назначения для остальных пользователей и групп.  
  
### Добавление пользователя или группы к роли на уровне элементов  
  
1.  Запустите **Диспетчер отчетов** и найдите элемент отчетов, для которого необходимо добавить пользователя или группу.  
  
2.  Подведите курсор к элементу и щелкните стрелку раскрывающегося списка.  
  
3.  В раскрывающемся меню выберите **Безопасность**.  
  
4.  Нажмите кнопку **Создать назначения ролей**.  
  
    > [!NOTE]  
    >  Если элемент в настоящий момент наследует настройки безопасности от родительского элемента, выберите пункт **Изменить параметры безопасности элемента** на панели инструментов для изменения настроек безопасности. Затем нажмите кнопку **Создать назначения ролей**.  
  
5.  В поле **Имя группы или пользователя** введите учетную запись пользователя или группы домена Windows в следующем формате: \<домен>\\<учетная_запись\>. Если используется проверка подлинности с помощью форм или пользовательский модуль безопасности, задайте учетную запись пользователя или группы в формате, допустимом для развертывания.  
  
6.  Выберите одно или более определений роли, которые описывают, как пользователь или группа должны обращаться к элементу, и затем нажмите кнопку **ОК**.  
  
7.  Создайте назначения для остальных пользователей и групп.  
  
## См. также раздел  
 [Создание назначений ролей и управление ими](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Страница "Создание назначения ролей": "Изменение назначения ролей" (диспетчер отчетов)](../Topic/New%20Role%20Assignment:%20Edit%20Role%20Assignment%20Page%20\(Report%20Manager\).md)   
 [Страница "Свойства безопасности", элементы (диспетчер отчетов)](../Topic/Security%20Properties%20Page,%20Items%20\(Report%20Manager\).md)   
 [Назначения ролей](../../reporting-services/security/role-assignments.md)   
 [Определение ролей](../../reporting-services/security/role-definitions.md)  
  
  