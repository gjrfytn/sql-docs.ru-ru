---
title: Сохранение отчета в библиотеке SharePoint (построитель отчетов) | Документы Майкрософт
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ca1376faaac9c3278a265c96a6196dbd971a41c2
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285292"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>Сохранение отчета в библиотеке SharePoint (построитель отчетов)
  Чтобы сохранить отчет на сервере отчетов, настроенном для режима интеграции с SharePoint, необходимо перейти на сервер SharePoint и установить соединение с сервером отчетов. В определении отчета все ссылки на элементы, связанные с отчетом, должны использовать переменные, относящиеся к серверу отчетов SharePoint. Связанные элементы включают вложенные отчеты, детализированные отчеты и ресурсы (например, изображения, хранящиеся в Интернете). Дополнительные сведения см. в разделе [Указание путей к внешним элементам (построитель отчетов и службы SSRS)](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Необходимо обладать разрешением **Член** или **Владелец** на сайте SharePoint для задания свойств проекта.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>Сохранение отчета на сайте SharePoint  
  
1.  В построителе отчетов нажмите кнопку **Сохранить**. Откроется диалоговое окно **Сохранить как**_\<элемент отчета>_.  
  
    > [!NOTE]  
    >  Во время повторного сохранения отчет автоматически сохраняется в предыдущем расположении. Чтобы изменить расположение, используйте параметр **Сохранить как** .  
  
2.  Также можно щелкнуть ссылку **Последние сайты и серверы** , чтобы вывести список недавно использовавшихся серверов отчета и сайтов SharePoint.  
  
3.  Выберите сайт SharePoint и щелкните **Сохранить**.  
  
    > [!NOTE]  
    >  Если не сохранять измененный отчет в течение более 10 часов, он отключается от сервера без сохранения. Если это произойдет, в правой нижней строке состояния щелкните **Отключение**, затем щелкните **Подключение**. Последний сервер будет в списке доступных серверов. Выберите его, и отчет вновь подключится.  
  
## <a name="see-also"></a>См. также:  
 [Поиск, просмотр отчетов и управление ими (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
