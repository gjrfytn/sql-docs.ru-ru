---
title: Параметры сайта и компоненты веб-сайтов (режим SharePoint) служб Reporting Services | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b2e6997afd52c8b999d981c5c15b782ad9a56407
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031075"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Страницы "Параметры сайта" и "Возможности сайта" служб Reporting Services (режим интеграции с SharePoint)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint имеет несколько пользовательских компонентов уровня сайта, а также компонент сайта, которым можно управлять со страницы «Настройки сайта SharePoint». Эти параметры распространяются на весь сайт и влияют на все приложения служб [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Для просмотра этой страницы требуются разрешения диспетчера содержимого или системного администратора.  
  
|Параметр сайта|Описание|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Параметры сайта|Параметры для всего сайта, описанные в этом разделе.|  
|Управление оповещениями об изменении данных|Управление компонентом предупреждения об изменении данных.|  
|Синхронизация файлов сервера отчетов|Компонент уровня сайта, который по умолчанию отключен.<br /><br /> Синхронизирует файлы сервера отчетов (RDL, RSDS, SMDL, RSD, RSC, RDLX) между библиотекой документов SharePoint и сервером отчетов при добавлении или обновлении файлов непосредственно в библиотеке документов.<br /><br /> Дополнительные сведения см. в разделе [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Открытие страницы «Параметры сайта служб Reporting Services»  
  
1.  С сайта SharePoint **действия сайта** меню **параметры сайта**.  
  
2.  В разделе **Службы Reporting Services** выберите пункт **Параметры сайта служб Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Параметры, приведенные на странице «Параметры сайта служб Reporting Services»  
  
|Параметр|Описание|  
|------------|-----------------|  
|**Разрешить загрузку элемента управления RSClientPrint ActiveX**|Данный элемент управления отображает пользовательское диалоговое окно печати, в котором поддерживаются все стандартные функции: предварительный просмотр, указание отдельных страниц и их диапазонов, поля и ориентация страниц. Дополнительные сведения об этом элементе управления см. в разделе [Using the RSClientPrint Control in Custom Applications](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Разрешить отслеживание удаленных ошибок в локальном режиме**|Показывать или скрывать подробные сообщения об ошибках, возникающих на удаленных компьютерах при работе в локальном режиме. При появлении сообщения об ошибке, аналогичного приведенному далее, может оказаться полезным включение отслеживания удаленных ошибок.<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Включить метаданные о специальных возможностях для отчетов**|Включение метаданных о специальных возможностях в выходные данные HTML для отчетов|  
|**Включить точную подгонку визуализации данных под размер для отчетов**|Настройка точной подгонки визуализации данных при использовании внутри табликса. Сюда входят: диаграмма, датчик и карта. Когда этот параметр не установлен, визуализация данных подгоняется приблизительно, при этом может оставаться незанятое место. Этот параметр применяется только к отображению в веб-части средства просмотра отчетов. Для управления этим поведением при просмотре на стороне сервера необходимо изменить файл **rsreportserver.config** . Дополнительные сведения см. в следующих разделах:<br /><br /> [Файл конфигурации RSReportServer](report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [HTML Device Information Settings](html-device-information-settings.md).<br /><br /> Включение этого параметра может негативно сказаться на производительности, поскольку на обработку для определения точного размера может уйти больше времени, чем при приблизительной подгонке.|  
  
## <a name="see-also"></a>См. также  
 [Управление Служебным приложением SharePoint службы Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
