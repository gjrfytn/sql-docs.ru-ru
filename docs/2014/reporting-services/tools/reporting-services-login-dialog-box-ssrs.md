---
title: Диалоговое окно имени для входа Reporting Services (SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f451128cbcd218a75ae269f43de922f04f3e7db9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033175"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Диалоговое окно «Имя входа служб Reporting Services» (службы SSRS)
  В диалоговом окне **Имя входа служб Reporting Services** задаются учетные данные для публикации отчетов на сервере отчетов.  
  
-   **Примечание** Если это первый раз, то публикация отчета на сервере отчетов после установки свойства развертывания **TargetServerURL** для проекта, убедитесь, что имя сервера, который вы указали аналогичную `http://localhost/reportserver`, а не `http://localhost/reports`. Указание каталога `reports` на локальном сервере вместо каталога `reportserver` косвенно вызывает открытие этого диалогового окна. Дополнительные сведения о настройке параметра **TargetServerURL** см. в разделе [Задание свойств развертывания (службы Reporting Services)](set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Параметры  
 **Server**  
 Отображает имя сервера отчетов. Например, `http://localhost/reportserver`. Для серверов отчетов, использующих порт, отличный от порта по умолчанию 80, включается номер порта. Например, `http://localhost:81/reportserver`.  
  
 **Имя пользователя**  
 Введите имя пользователя для входа в данную веб-службу.  
  
 **Пароль**  
 Введите пароль для входа в данную веб-службу.  
  
## <a name="see-also"></a>См. также  
 [Подключения к данным, источники данных и строки подключения в службах Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Задание учетных данных и сведения о соединении для источников данных отчета](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Справка F1 конструктора отчетов](report-designer-f1-help.md)  
  
  
