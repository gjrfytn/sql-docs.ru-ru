---
title: "Проверка подлинности с использованием сервера отчетов | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "соединения [службы Reporting Services], настройка"
  - "соединения [службы Reporting Services], учетные записи"
  - "проверка подлинности Windows [службы Reporting Services]"
  - "проверка подлинности [службы Reporting Services]"
  - "проверка подлинности с помощью форм"
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# Проверка подлинности с использованием сервера отчетов
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) предлагает несколько настраиваемых параметров для проверки подлинности клиентов и клиентских приложений для сервера отчетов. По умолчанию сервер отчетов использует встроенную проверку подлинности Windows и предполагает доверительные связи, когда клиент и сетевые источники находятся в одном и том же домене или в надежном домене. В зависимости от топологии сети и потребностей организации можно задать протокол проверки подлинности, который применяется для встроенного средства проверки подлинности Windows, использовать обычную проверку подлинности или модуль проверки подлинности на основе пользовательских форм. Каждый способ проверки подлинности можно включать и отключать отдельно. Можно включить одновременно несколько типов проверки подлинности, если сервер отчетов должен принимать запросы разных типов.
  
 Подлинность всех пользователей и приложений, запрашивающих доступ к содержимому сервера отчетов или операциям, должна быть проверена до предоставления доступа.  
  
## Типы проверки подлинности  
 Подлинность всех пользователей и приложений, запрашивающих доступ к содержимому сервера отчетов или операциям, должна быть проверена до предоставления доступа способом, заданным для сервера отчетов. В следующей таблице описываются типы проверки подлинности, поддерживаемые службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Имя типа проверки подлинности|Значение уровня проверки подлинности HTTP|Используется по умолчанию|Description|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Согласование|Да|В этом режиме сначала делается попытка встроенной проверки подлинности по протоколу Kerberos, но если служба каталогов Active Directory не может предоставить серверу отчетов билет для клиентского запроса, используется NTLM. Проверка подлинности Negotiate возвращается к NTLM только в том случае, если не удалось получить билет. Если первая попытка завершилась ошибкой, а не отсутствием билета, то сервер отчетов вторую попытку не предпринимает.|  
|RSWindowsNTLM|NTLM|Да|Использует NTLM для встроенной проверки подлинности Windows.<br /><br /> Делегирование и олицетворение учетных данных при выполнении других запросов не производится. Последующие запросы выполняются по новой последовательности вызов-ответ. В зависимости от того, как настроена безопасность сети, запрос проверки подлинности будет обрабатываться прозрачно либо пользователю может быть предложено ввести учетные данные.|  
|RSWindowsKerberos|Kerberos|Нет|Использует Kerberos для встроенной проверки подлинности Windows. Необходимо настроить Kerberos, задав имена участников служб (SPN) для учетных записей, для чего потребуются права администратора домена. Если разрешено делегирование идентификатора с использованием Kerberos, токен пользователя, запрашивающего отчет, может использоваться и для дополнительного соединения с внешними источниками данных, поставляющими данные для этого отчета.<br /><br /> Прежде чем указывать RSWindowsKerberos, убедитесь, что применяемый браузер действительно поддерживает этот тип проверки подлинности. При использовании браузера Microsoft Edge или Internet Explorer проверка подлинности по протоколу Kerberos поддерживается только через согласование. Microsoft Edge или Internet Explorer не сможет сформулировать запрос проверки подлинности, в котором протокол Kerberos задан напрямую.|  
|RSWindowsBasic|Basic|Нет|Обычная проверка подлинности определена протоколом HTTP и может применяться только для проверки подлинности HTTP-запросов к серверу отчетов.<br /><br /> Учетные данные передаются в HTTP-запросе в кодировке Base 64. Если применяется обычная проверка подлинности, то необходимо обеспечить шифрование данных об учетных записях пользователя по протоколу SSL, прежде чем передавать их по сети. Протокол SSL обеспечивает защищенный канал для передачи запроса на соединение от клиента к серверу отчетов через TCP/IP-соединение. Дополнительные сведения см. в разделе [Использование SSL для шифрования конфиденциальных данных](http://go.microsoft.com/fwlink/?LinkId=71123) на сайте [!INCLUDE[msCoName](../../includes/msconame-md.md)] TechNet.|  
|Другой|(Анонимная)|Нет|Анонимная проверка подлинности предписывает серверу отчетов пропускать проверки подлинности в заголовках HTTP-запросов. Сервер отчетов принимает все запросы, но вызывает пользовательскую проверку подлинности пользователя через формы [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .<br /><br /> Режим **Custom** следует выбирать только при наличии пользовательского модуля проверки подлинности, который будет обрабатывать все запросы проверки подлинности на сервере отчетов. Нельзя использовать тип нестандартной проверки подлинности с модулем проверки подлинности Windows по умолчанию.|  
  
## Неподдерживаемые методы проверки подлинности  
 Следующие методы и запросы проверки подлинности не поддерживаются.  
  
|Метод проверки подлинности|Объяснение|  
|---------------------------|-----------------|  
|Анонимная проверка подлинности|Сервер отчетов не принимает запросы без проверки подлинности от анонимного пользователя, за исключением конфигураций развертывания, которые включают нестандартные модули проверки подлинности.<br /><br /> Построитель отчетов принимает запросы без проверки подлинности в том случае, если разрешен доступ к построителю отчетов на сервере отчетов, настроенном для обычной проверки подлинности.<br /><br /> Для всех остальных случаев анонимные запросы будут отвергнуты с ошибкой «HTTP 401: Отказано в доступе» еще до того, как запрос дойдет до [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Получив ошибку «HTTP 401: Отказано в доступе«, клиент должен переформулировать запрос, указав допустимый тип проверки подлинности.|  
|Технологии единого входа (SSO)|Службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] не обеспечивают собственную поддержку для технологий единого входа. Для использования этих технологий необходимо создание нестандартного модуля проверки подлинности.<br /><br /> Среда размещения сервера отчетов не поддерживает ISAPI-фильтры. Если используемая технология SSO реализована в виде фильтра ISAPI, попробуйте воспользоваться встроенной поддержкой сервера ISA для протокола RSASecueID или RADIUS. В противном случае можно создать сервер ISAPI ISA или HTTPModule для RS, однако рекомендуется использовать сервер ISA напрямую.|  
|Паспорт|Не поддерживается в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|Дайджест|Не поддерживается в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## Параметры проверки подлинности  
 При резервировании URL-адреса для сервера отчетов для проверки подлинности настраивается уровень безопасности по умолчанию. Если в процессе настройки этих параметров допущены какие-либо ошибки, то для HTTP-запросов, подлинность которых не может быть проверена, сервер отчетов вернет ошибку «HTTP 401: Отказано в доступе». Чтобы правильно выбрать тип проверки подлинности, необходимо понимать, каким образом проверка подлинности Windows поддерживается в конкретной сети. Должен быть указан как минимум один тип проверки подлинности. Для RSWindows может быть задано несколько типов проверки подлинности. Типы проверки подлинности RSWindows (то есть **RSWindowsBasic**, **RSWindowsNTLM**, **RSWindowsKerberos** и **RSWindowsNegotiate**) и Custom являются взаимоисключающими.  
  
> [!IMPORTANT]  
>  Службы Reporting Services не проверяют заданные параметры на соответствие конкретной вычислительной среде. Безопасность по умолчанию может оказаться неработоспособной либо могут быть заданы параметры настройки, недопустимые для существующей инфраструктуры безопасности. Поэтому перед внедрением в рабочей среде организации необходимо очень тщательно проверить развертывание сервера отчетов в управляемой тестовой среде.  
  
 Веб-служба сервера отчетов и [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] всегда используют один и тот же тип проверки подлинности. Нельзя настроить разные типы проверки подлинности для функциональных областей службы сервера отчетов. Для масштабного развертывания необходимо повторить изменения на всех узлах в конфигурации развертывания. В масштабном развертывании узлы не могут использовать различные типы проверки подлинности.  
  
 При фоновой обработке запросы от конечных пользователей не принимаются, однако выполняется проверка подлинности всех запросов на автоматическое выполнение. В ней всегда используется проверка подлинности Windows и выполняется проверка подлинности запросов с использованием учетной записи службы сервера отчетов или учетной записи автоматического выполнения, если она настроена.  
  
## В этом разделе  
  
-   [Настройка проверки подлинности Windows на сервере отчетов](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
-   [Настройка обычной проверки подлинности на сервере отчетов](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)  
  
-   [Настройка нестандартной проверки подлинности или проверку подлинности с помощью форм на сервере отчетов](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## Связанные задачи  
  
|Описания задач|Ссылки|  
|-----------------------|-----------|  
|Задайте встроенную проверку подлинности Windows.|[Настройка проверки подлинности Windows на сервере отчетов](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)|  
|Задайте обычную проверку подлинности.|[Настройка обычной проверки подлинности на сервере отчетов](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)|  
|Задайте проверку подлинности с помощью форм или другой нестандартный тип проверки.|[Настройка нестандартной проверки подлинности или проверку подлинности с помощью форм на сервере отчетов](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)|  
|Включите [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] для обработки сценария пользовательской проверки подлинности.|[Настройка передачи файлов cookie для пользовательской проверки подлинности на веб-портале](http://msdn.microsoft.com/ru-ru/91aeb053-149e-4562-ae4c-a688d0e1b2ba)|  
  
## См. также:  
 [Предоставление разрешений на сервер отчетов в собственном режиме](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Создание назначений ролей и управление ими](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Задание учетных данных и сведениях о соединении для источников данных отчета](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Реализация модуля безопасности](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
 [Настройка соединений SSL для сервера отчетов, работающего в собственном режиме](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [настроить доступ к построителю отчетов](../../reporting-services/report-server/configure-report-builder-access.md)   
 [Общие сведения о модулях безопасности](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
 [Проверка подлинности в службах Reporting Services](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)   
 [Авторизация в службах Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)  
  
  