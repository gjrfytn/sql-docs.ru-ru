---
title: "Включение доступа к серверу отчетов для мобильного приложения Power BI | Microsoft Docs"
ms.date: "12/17/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1a71522-394b-46a7-b9ec-f964bdd81d82
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Включение доступа к серверу отчетов для мобильного приложения Power BI
С помощью мобильного приложения Power BI можно работать с мобильными отчетами. Чтобы предоставить мобильному приложению Power BI доступ к службам Reporting Services, необходимо выполнить некоторые условия.  
  
-   [Для работы с мобильными отчетами требуются службы Reporting Services в собственном режиме.](#nativemode)  
-   [Необходимо включить обычную проверку подлинности для служб Reporting Services](#basicauth) (CTP-версии 3.2).  
-   [Рекомендуется включить HTTPS и использовать допустимое доверие сертификата для клиентского устройства.](#https)  
-   [Необходимо проверить параметры брандмауэра.](#firewall)  
  
<a name="nativemode"/>  
## Службы Reporting Services в собственном режиме  
Мобильные отчеты поддерживаются только в собственном режиме. Они недоступны в режиме интеграции с SharePoint. Мобильное приложение Power BI работает только с экземпляром в собственном режиме.  
  
<a name="basicauth"/>  
## Включение обычной проверки подлинности  
Чтобы подключаться к серверу с мобильными отчетами и использовать их с помощью мобильного приложения Power BI для iOS, требуется обычная проверка подлинности. По умолчанию для служб Reporting Services обычная проверка подлинности не включена. Дополнительные сведения о настройке обычной проверки подлинности см. в статье [Настройка проверки подлинности Windows на сервере отчетов](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).  
  
Кроме того, чтобы разрешить издателю публиковать мобильные отчеты, необходимо включить проверку подлинности Windows.  
  
<a name="https"/>  
## Включение HTTPS  
Если используется обычная проверка подлинности, рекомендуется также включить протокол HTTPS в службах Reporting Services. При этом используемые сертификаты должны быть доверенными для клиентских устройств, где установлено мобильное приложение Power BI для iOS. Это означает, что цепочка сертификатов должна быть допустимой и доступной для клиентского устройства.  
  
Если для разработки и оценки необходимо использовать самозаверяющий сертификат, его можно экспортировать с сервера отчетов и установить на мобильном устройстве. Сведения об установке самозаверяющего сертификата можно посмотреть в документации по устройству.  
  
Дополнительные сведения о включении подключений SSL см. в статье [Настройка соединений SSL для сервера отчетов, работающего в собственном режиме](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
<a name="firewall"/>  
## Необходимо проверить параметры брандмауэра.  
Рекомендуется проверить параметры брандмауэра, чтобы убедиться, что все устройства могут подключиться к службам Reporting Services.   
  
Дополнительные сведения о настройке брандмауэра Windows см. в статье [Настройка брандмауэра для доступа к серверу отчетов](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
## См. также:  
  
[Настройка обычной проверки подлинности на сервере отчетов](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
[Настройка соединений SSL для сервера отчетов, работающего в собственном режиме](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[настроить брандмауэр для доступа к серверу отчетов](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
  
  
  
  