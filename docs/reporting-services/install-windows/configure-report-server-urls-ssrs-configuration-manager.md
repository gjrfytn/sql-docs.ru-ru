---
title: "Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "служба сервера отчетов Windows, виртуальные каталоги"
  - "серверы отчетов [службы Reporting Services], виртуальные каталоги"
  - "виртуальные каталоги [службы Reporting Services]"
  - "диспетчер отчетов [службы Reporting Services], виртуальные каталоги"
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 10
---
# Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS)
  В [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL-адреса используются для доступа к веб-службам сервера отчетов и [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Прежде чем использовать любое приложение, необходимо настроить по крайней мере по одному URL-адресу для веб-службы и [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для URL-адресов обоих приложений предоставляет значения по умолчанию, которые подходят для большинства сценариев развертывания, в том числе развертывания параллельно с другими веб-службами и приложениями.  
  
-   При установке стандартной конфигурации URL-адреса создаются автоматически при помощи значений по умолчанию.  
  
-   Если URL-адреса создаются или изменяются при помощи программы настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , для них можно принять значения по умолчанию, либо указать пользовательские значения. При задании URL-адреса на странице появляется проверочная ссылка с URL-адресом; таким образом, можно убедиться, что указанные настройки приводят к допустимому соединению. Пошаговые инструкции по настройке и проверке URL-адресов см. в разделе [Настройка URL-адреса (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
## Определение URL-адреса сервера отчетов  
 URL-адрес точно определяет расположение экземпляра приложения сервера отчетов в сети. При создании URL-адреса сервера отчетов необходимо указать следующие элементы.  
  
|Часть|Описание|  
|----------|-----------------|  
|Имя узла|IP-адрес позволяет однозначно идентифицировать устройство в сети TCP/IP. Это физический IP-адрес каждого сетевого адаптера, установленного в компьютер. Если IP-адрес указывает на заголовок узла, можно указать заголовок узла. Если сервер отчетов развертывается в сети организации, то можно использовать сетевое имя компьютера.|  
|Порт|TCP-порт является конечной точкой в устройстве. Сервер отчетов прослушивает запросы, проходящие через определенный порт.|  
|Виртуальный каталог|Порт часто используется несколькими веб-службами или приложениями. Поэтому URL-адрес сервера отчетов всегда содержит виртуальный каталог, соответствующий приложению, которое получает запрос. Уникальное имя виртуального каталога необходимо указать для каждого из приложений служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , прослушивающих один и тот же IP-адрес и порт.|  
|Параметры SSL|URL-адреса в службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] могут быть настроены для использования существующего SSL-сертификата, установленного на компьютер ранее. Дополнительные сведения см. в разделе [Настройка соединений SSL для сервера отчетов, работающего в собственном режиме](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## URL-адреса по умолчанию  
 При получении доступа к серверу отчетов или [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] посредством соответствующего URL-адреса этот адрес должен содержать имя узла, а не IP-адрес. В сети TCP/IP IP-адрес приводит к имени узла (или сетевому имени компьютера). Если настройка URL-адресов осуществляется при помощи значений по умолчанию, доступ к веб-службе сервера отчетов должен быть возможен при использовании URL-адресов, в которых в качестве имени узла указано имя компьютера или localhost:  
  
-   http://\<имя_компьютера>/reportserver  
  
-   http://localhost/reportserver  
  
 Настройки, благодаря которым доступны такие URL-адреса, отражены в следующей таблице. Эта таблица представляет значения по умолчанию, которые разрешают соединение с сервером отчетов посредством URL-адресов, содержащих имя узла:  
  
|Часть|Значение|Объяснение|  
|----------|-----------|-----------------|  
|IP-адрес|Все назначенные|Служба доменных имен в рабочей сети извлекает IP-адрес из имени узла в URL-адресе. При условии, что в заданном URL-адресе определен IP-адрес, запрос, отправленный на определенный узел, всегда достигнет пункта назначения.|  
|Порт|80|Порт 80 — это стандартный порт компьютера для соединений TCP/IP. Поскольку сервер отчетов прослушивает порт 80, указание номера порта в URL-адресе можно опустить. При использовании другого порта его необходимо указать в URL-адресе.|  
|Виртуальный каталог|ReportServer|Обратите внимание, что в обоих URL-адресах в примере содержится имя виртуального каталога. Если определение URL-адреса не настроено соответствующим образом, имя виртуального каталога приложения всегда должно быть указано в URL-адресе.|  
  
> [!NOTE]  
>  Базовое URL-резервирование позволяет использовать в URL-адресах любые допустимые имена узлов. Программой настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] создается резервирование URL-адреса в файле HTTP.SYS, используя синтаксис, допускающий переход к определенному экземпляру сервера отчетов по нескольким вариантам имени узла. Дополнительные сведения о резервировании URL-адреса см. в разделе [Сведения о резервировании и регистрации URL-адресов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).  
  
## Разрешения для URL-адресов сервера отчетов на стороне сервера  
 Разрешения для каждой конечной точки URL-адреса предоставляются исключительно учетной записи службы сервера отчетов. Только у этой учетной записи имеется право доступа к запросам, направленным к URL-адресам служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. При настройке идентификатора службы в программе установки или в программе настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для этой учетной записи создаются и обрабатываются ограниченные списки управления доступом на уровне пользователей (DACL). Если учетная запись службы изменена, программой настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] обновляются все резервирования URL-адресов, чтобы интегрировать новые сведения об учетной записи. Дополнительные сведения см. в разделе [Синтаксис резервирования URL-адресов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).  
  
## Проверка подлинности клиентских запросов, отправленных на URL-адрес сервера отчетов  
 По умолчанию в конечных точках URL-адресов поддерживается проверка подлинности Windows. Это модуль безопасности, используемый по умолчанию. При реализации пользовательской проверки или поставщика проверки подлинности с помощью форм необходимо изменить параметры проверки подлинности на сервере отчетов. При необходимости параметры проверки подлинности Windows можно также изменить, чтобы они соответствовали подсистеме проверки подлинности, используемой в сети. Дополнительные сведения см. в разделе [Проверка подлинности с использованием сервера отчетов](../../reporting-services/security/authentication-with-the-report-server.md) электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## В этом разделе  
 [Настройка URL-адреса (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 В этом разделе содержатся инструкции по настройке и изменению резервирования URL-адресов в программе настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Сведения о резервировании и регистрации URL-адресов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 Настройте URL-адресы, используемые для доступа к приложениям и отчетам. В этом разделе описаны URL-адреса приложений, URL-адреса по умолчанию и способы работы URL-резервирования и регистрации в службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Синтаксис резервирования URL-адресов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 Резервирования URL-адресов по умолчанию, используемые службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], действительны в большинстве сценариев. Однако при необходимости ограничить доступ или расширить развертывание с целью обеспечения доступа к Интернету или экстрасети может потребоваться настроить параметры в соответствии с собственными требованиями. В данном разделе описывается синтаксис резервирования URL-адреса, и содержатся рекомендации по созданию пользовательских резервирований для развертываний.  
  
 [URL-адреса файлов конфигурации (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 Файл RSReportServer.config содержит несколько записей для резервирований URL-адресов, а также URL-адреса, используемые [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] и модулем доставки сообщений электронной почты сервера отчетов. В данном разделе описаны параметры конфигурации URL-адресов, позволяющее понять их сравнение.  
  
 [Резервирование URL-адресов при развертывании сервера отчетов на нескольких экземплярах (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/url reservations for multi-instance report server deployments.md)  
 При установке нескольких экземпляров служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] на одном компьютере увеличивается вероятность дублирования URL-адресов во время их регистрации. Чтобы избежать таких ошибок, следует придерживаться приведенных в данном разделе рекомендаций по созданию резервирований URL-адресов, зависящих от экземпляров.  
  
## См. также:  
 [Настройка URL-адреса (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 