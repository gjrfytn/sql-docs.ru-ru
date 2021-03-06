---
title: Сообщить о диалоговом окне Свойства ссылки (построитель отчетов) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 540ba2502ebf55b493c901640513f19382b22a37
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292794"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>Диалоговое окно «Свойства отчета» — «Ссылки» (построитель отчетов)
  На вкладке **Ссылки** диалогового окна **Свойства отчета** можно удалить или добавить ссылки на пользовательские или другие внешние сборки и экземпляры пользовательских классов, используемые выражениями в определении отчета. Пользовательские сборки не поддерживаются в локальном режиме построителя отчетов. Для составления отчетов, использующих пользовательские сборки, с помощью конструктора отчетов в [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Параметры  
 **Добавить или удалить сборки**  
 Отображает список сборок, на которые имеются ссылки в отчете. Сборка должна быть доступна на компьютере, на котором установлено средство для создания отчетов, и на сервере отчетов. Имя ссылки должно соответствовать содержимое  **\<CodeModule >** точно теги в файле языка определения отчетов (RDL-файл).  
  
 **Добавить**  
 Нажмите, чтобы добавить сборку. Нажмите кнопку с многоточием (...), чтобы открыть **откройте** диалоговое окно и выберите сборки, необходимые для завершения обработки отчета и выражение оценки.  
  
 **Удалить**  
 Чтобы удалить ссылку на сборку из списка, выделите имя сборки, а затем нажмите кнопку **Удалить** .  
  
 **Добавить или удалить классы**  
 Отображает список экземпляров классов, которые используются в отчете. Список классов используется только элементами на основе экземпляров, но не статическими элементами.  
  
 **Добавить**  
 Нажмите, чтобы добавить ссылку на класс. Нажмите кнопку с многоточием (...), чтобы открыть **откройте** диалоговое окно и выберите классы, необходимые для завершения обработки отчета и выражение оценки.  
  
 **Удалить**  
 Чтобы удалить экземпляр класса, выберите его и нажмите кнопку **Удалить** .  
  
 **Вверх**  
 Применительно к классам, характеризующимся наличием зависимостей, допускается перемещение этой ссылки в более высокую позицию списка.  
  
 **Вниз**  
 Применительно к классам, характеризующимся наличием зависимостей, допускается перемещение этой ссылки в более низкую позицию списка.  
  
## <a name="see-also"></a>См. также  
 [Справка построителя отчетов для диалоговых окон, панелей и мастеров](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Выражения (построитель отчетов и службы SSRS)](report-design/expressions-report-builder-and-ssrs.md)  
  
  
