---
title: Соединение задач и контейнеров с помощью очередностью по умолчанию | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a900b6c2bb6e55d57bcf32aff0ac6ea4667bdd7f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389242"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>Соединение задач и контейнеров с помощью элементов управления очередностью по умолчанию
  Объекты управления очередностью соединяют два исполняемых объекта. Исполняемым объектом может быть любая задача, контейнеры «цикл по элементам», «цикл по каждому элементу» или контейнеры последовательности. Ниже описана процедура настройки поведения по умолчанию для объектов управления очередностью, а также настройка исполняемых объектов с помощью управления очередностью по умолчанию.  
  
## <a name="creating-default-precedence-constraints"></a>Создание объектов управления очередностью по умолчанию  
 При первом запуске конструктора служб [!INCLUDE[ssIS](../includes/ssis-md.md)] значение по умолчанию для управления очередностью равно `Success`. Чтобы изменить в конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] значение по умолчанию для управления очередностью, выполните следующие действия.  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>Настройка значения по умолчанию для управления очередностью  
  
1.  Откройте [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  В меню **Сервис** выберите команду **Параметры**.  
  
3.  В диалоговом окне **Параметры** разверните узел **Конструкторы бизнес-аналитики** , затем разверните **Конструкторы служб Integration Services**.  
  
4.  Щелкните **Автосоединение для потока управления** и выберите **Подключить новую фигуру к выбранной фигуре по умолчанию**.  
  
5.  В раскрывающемся списке выберите либо **Использовать ограничение ошибки для новой фигуры** , либо **Использовать ограничение завершения для новой фигуры**.  
  
6.  Нажмите кнопку **ОК**.  
  
#### <a name="to-create-a-default-precedence-constraint"></a>Создание объекта управления очередностью по умолчанию  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Перейдите на вкладку **Поток управления** .  
  
4.  В области конструктора на вкладке **Поток управления** щелкните задачу или контейнер и перетащите их соединители на исполняемый объект, к которому нужно применить управление очередностью.  
  
5.  Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## <a name="see-also"></a>См. также  
 [Управление очередностью](control-flow/precedence-constraints.md)   
 [Установите для параметра очередностью с помощью контекстного меню](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Задайте свойства элементов управления очередностью](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Использование выражения в элементах управлении очередностью](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
