---
title: Занятие 7. Добавление действия детализации к родительскому отчету | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3181cfd46cbb2eaf307a539d0b3f906d611dd19b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042535"
---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>Занятие 7. Добавление операции детализации к родительскому отчету
  После добавления элемента управления ReportViewer в приложение веб-сайта далее необходимо добавить действие детализации в родительский отчет.  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>Добавление действия детализации в родительский отчет  
  
1.  Перейдите к родительскому отчету.  
  
2.  Щелкните текстовое поле, в котором содержится значение **Имя**.  
  
3.  Щелкните это текстовое поле правой кнопкой мыши и выберите пункт **Свойства текстового поля**.  
  
4.  Перейдите на вкладку **Действие** и выберите параметр **Переход к отчету** .  
  
5.  В разделе **Указать отчет** введите имя дочернего отчета.  
  
6.  В разделе **Использование этих параметров для выполнения отчета** нажмите кнопку **Добавить** .  
  
7.  Введите **productid** в поле **Имя** , затем выберите пункт **ProductID** в раскрывающемся списке **Значение** .  
  
8.  Нажмите кнопку **ОК** для завершения.  
  
## <a name="next-task"></a>Следующая задача  
 Тем самым в родительский отчет была успешно добавлена операция детализации. Затем необходимо создать фильтр данных для таблицы данных, которая определена в дочернем отчете.  
  
  
