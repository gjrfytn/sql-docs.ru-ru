---
title: Подключения фильтра или веб-часть "документы" (службы Reporting Services в режиме интеграции с SharePoint) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4da46abbfb586a2968f92a04538f5a82e06898c6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031225"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>установить соединение с веб-частью «Фильтр» или с веб-частью «Документы» (службы Reporting Services в режиме интеграции с SharePoint)
  Если используется продукт SharePoint, можно создать панель мониторинга или страницу веб-частей, включающую веб-части «Фильтр» или «Документы» и веб-часть средства просмотра отчетов. Поддерживается версия [!INCLUDE[SPF2010](../includes/spf2010-md.md)] или [!INCLUDE[SPS2010](../includes/sps2010-md.md)]. Также поддерживаются версии [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] и [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007. С помощью соединения с веб-частью «Фильтр» пользователи, которые выбирают значения фильтра в веб-части «Фильтр», могут отправить значение в параметризованный отчет на той же самой странице. С помощью соединения с веб-частью «Документы» пользователи, выбравшие отчет в библиотеке «Документы», могут просмотреть его в веб-части «Средство просмотра отчетов».  
  
 Веб-часть «Фильтр» используется для передачи значений в один или более параметров отчета. Чтобы использовать веб-часть «Фильтр», необходимо, чтобы параметры отчета были совместимы со значениями, типами данных и форматом, посылаемыми в веб-часть.  
  
 Веб-часть «Документы» связана с библиотекой «Документы» домашнего веб-сайта. Чтобы просмотреть, добавить или удалить элементы библиотеки «Документы», выберите **Просмотреть все содержимое веб-сайта**. В меню «Библиотеки» выберите **Документы**. Для управления элементами библиотеки «Документы» можно использовать меню **Создание**, **Передача**и **Действия** .  
  
### <a name="to-connect-a-filter-web-part"></a>Соединение с веб-частью «Фильтр»  
  
1.  Открытие и создание страницы веб-части или инструментальной панели.  
  
2.  В меню **Действия веб-сайта** выберите команду **Редактировать страницу**.  
  
3.  Нажмите кнопку **Добавить веб-часть**.  
  
4.  В окне **Все веб-части**в категории **Разное** выберите элемент **Средство просмотра отчетов служб SQL Server Reporting Services**.  
  
5.  Нажмите кнопку **Добавить**. Веб-часть будет добавлена в верхнюю часть зоны.  
  
6.  В другой области той же страницы веб-части или панели мониторинга содержащей веб-часть нажмите кнопку **Добавить веб-часть**.  
  
7.  В меню **Все веб-части**в разделе **Фильтры** выберите необходимую веб-часть.  
  
8.  Нажмите кнопку **Добавить**. Веб-часть будет добавлена в верхнюю часть зоны.  
  
9. В области, содержащей веб-часть, в меню **Правка** веб-части последовательно укажите пункты **Соединения**, **Передать значения фильтров**и выберите пункт **Средство просмотра отчетов** - *имя отчета*.  
  
10. Проверьте изменения и сохраните страницу.  
  
### <a name="to-connect-a-documents-web-part"></a>Соединение с веб-частью «Документы»  
  
1.  Открытие и создание страницы веб-части или инструментальной панели.  
  
2.  В меню **Действия веб-сайта** выберите команду **Редактировать страницу**.  
  
3.  Нажмите кнопку **Добавить веб-часть**.  
  
4.  В меню **Все веб-части**в разделе **Списки и библиотека** выберите пункт **Документы**.  
  
5.  Нажмите кнопку **Добавить**. Веб-часть будет добавлена в верхнюю часть зоны.  
  
6.  Нажмите кнопку **Применить** в нижней части панели средств, а затем кнопку **ОК** , чтобы закрыть панель.  
  
7.  В другой области той же страницы веб-части или панели мониторинга содержащей веб-часть нажмите кнопку **Добавить веб-часть**.  
  
8.  В окне **Все веб-части**в категории **Разное** выберите элемент **Средство просмотра отчетов служб SQL Server Reporting Services.**  
  
9. Нажмите кнопку **Добавить**. Веб-часть будет добавлена в верхнюю часть зоны.  
  
10. В области, содержащей веб-часть, в меню **Правка** веб-части последовательно укажите курсор на пункты **Соединения**, **Получить определения отчетов из**и выберите пункт **Документы**.  
  
11. Проверьте изменения и сохраните страницу.  
  
## <a name="see-also"></a>См. также  
 [Добавление веб-части средства просмотра отчетов на веб-страницу (службы Reporting Services в режиме интеграции с SharePoint)](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [Веб-часть средства просмотра отчетов на сайте SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Настройка веб-части средства просмотра отчетов](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
