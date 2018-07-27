---
title: Использование переменных в компоненте скрипта | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8556b2ceb0da2c533bead385380956351413aba2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291060"
---
# <a name="using-variables-in-the-script-component"></a>Использование переменных в компоненте скрипта
  Переменные хранят значения, которые пакет и его контейнеры, задачи и обработчики событий могут использовать во время выполнения. Дополнительные сведения см. в разделе [Integration Services &#40;SSIS&#41; Variables](../../integration-services-ssis-variables.md).  
  
 Можно сделать доступными для существующих переменных только для чтения или чтения и записи с помощью пользовательского скрипта, введя разделенный запятыми список переменных в `ReadOnlyVariables` и `ReadWriteVariables` поля на **скрипт** странице **Редактор преобразования "скрипт"**. Помните, что в именах переменных учитывается регистр. Используйте свойство `Value`, чтобы считывать значения отдельных переменных и записывать значения в них. Компонент скрипта обрабатывает любые необходимые блокировки в фоновом режиме, пока скрипт во время выполнения обрабатывает переменные.  
  
> [!IMPORTANT]  
>  Коллекция `ReadWriteVariables` доступна только в методе `PostExecute` для повышения производительности и снижения риска конфликта блокировок. Поэтому нельзя непосредственно увеличивать значение переменной пакета после обработки каждой строки данных. Вместо этого увеличьте значение локальной переменной и присвойте переменной пакета значение локальной переменной в методе `PostExecute` после обработки всех данных. Чтобы обойти это ограничение можно также использовать свойство <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, как описано ниже в этом разделе. Однако запись напрямую в переменную пакета по мере обработки каждой строки отрицательно скажется на производительности и увеличит риск конфликта блокировок.  
  
 Дополнительные сведения о **сценарий** странице **редактор преобразования "скрипт"**, см. в разделе [Настройка компонента скрипта в редакторе компонента скрипта] (() Configuring-the-Script-Component-in-the-Script-Component-Editor.MD) и [редактор преобразования "скрипт" &#40;страница «скрипт»&#41;](../../script-transformation-editor-script-page.md).  
  
 Компонент скрипта создает класс коллекции `Variables` в элементе проекта `ComponentWrapper` со строго типизированным свойством метода доступа для значения каждой предварительно настроенной переменной, в которой свойство имеет то же самое имя, что и сама переменная. Эта коллекция доступна с помощью свойства `Variables` класса `ScriptMain`. Свойство метода доступа предоставляет разрешения только для чтения или для чтения и записи значения этой переменной, в зависимости от ситуации. Например, если к списку `ReadOnlyVariables` добавлена целочисленная переменная с именем `MyIntegerVariable`, ее значение можно получить в скрипте с помощью следующего кода:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 Для работы с переменными в компоненте скрипта можно также использовать свойство <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, вызвав метод `Me.VariableDispenser`. В этом случае доступ к переменным осуществляется напрямую, без использования типизированных и именованных свойств метода доступа к переменным. При использовании свойства <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> необходимо обрабатывать в коде и семантику блокирования, и приведение типов данных для значений переменных. Необходимо использовать свойство <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> вместо типизированных и именованных свойств метода доступа, если требуется работать с переменной, недоступной во время разработки, но создающейся программным способом во время выполнения.  
  
![Значок служб Integration Services (маленький)](../../media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services  **<br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы корпорации Майкрософт, а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
## <a name="see-also"></a>См. также  
 [Службы Integration Services &#40;SSIS&#41; переменных](../../integration-services-ssis-variables.md)   
 [Использование переменных в пакетах](../../use-variables-in-packages.md)  
  
  