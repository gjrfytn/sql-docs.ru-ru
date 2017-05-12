---
title: "План обслуживания (вкладка &quot;Конструирование&quot;) | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.maintplanproperties.optimizations.f1
- sql13.swb.maint.planeditor.f1
- sql13.swb.maint.subplaneditor.f1
ms.assetid: 6d20d4d4-5b3f-454a-8a05-f0aac803c5ad
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18b12faae420e8294dc79c15e1e0f168faaa5395
ms.lasthandoff: 04/11/2017

---
# <a name="maintenance-plan-design-tab"></a>План обслуживания (вкладка «Конструирование»)
  **План обслуживания** (вкладка "Конструирование") используется для указания свойств плана обслуживания и его вложенных планов. Перетащите задачи из области элементов в конструктор планов. Щелкните правой кнопкой мыши группы задач, чтобы создать ветвящиеся пути выполнения. Планы обслуживания сохраняются в виде пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , которые запускаются заданиями агентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Параметры  
 **Добавление вложенного плана**  
 Добавляет настраиваемый вложенный план.  
  
 **Свойства вложенного плана**  
 Отображает диалоговое окно **Свойства вложенного плана** . Выберите в сетке вложенный план и щелкните этот значок, чтобы ввести имя, описание и расписание для вложенного плана. Чтобы вывести диалоговое окно **Свойства вложенного плана** , можно дважды щелкнуть вложенный план в сетке. Длина имени вложенного плана ограничена 128 знаками, а длина описания плана — 512 знаками.  
  
 **Удаление выбранного вложенного плана**  
 Удаляет выбранный вложенный план.  
  
 **Расписание вложенного плана**  
 Вызывает диалоговое окно **Свойства расписания задания** . Выберите в сетке вложенный план и щелкните этот значок, чтобы настроить расписание для вложенного плана.  
  
 **Удаление расписания**  
 Удаляет расписание из выбранного вложенного плана.  
  
 **Управление соединениями**  
 Вызывает диалоговое окно **Управление соединениями** . Используется для добавления дополнительных соединений экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] к плану обслуживания. Каждая задача обслуживания в редакторе вложенных планов может использовать любое из этих соединений. В процессе выполнения план обслуживания устанавливает соединение между сервером планов обслуживания и указанными серверами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью учетных данных соединения.  
  
 **Отчеты и ведение журнала**  
 Выводит диалоговое окно **Отчеты и ведение журнала** , которое используется для управления отчетами, касающимися операций плана обслуживания, и для настройки ведения журналов на локальном и удаленном сервере.  
  
 **Серверы**  
 Отображает диалоговое окно **Серверы** , которое используется для выбора серверов, на которых будут выполняться задачи вложенного плана. Этот параметр доступен только на главных серверах в многосерверном окружении. Дополнительные сведения см. в статье [Создание многосерверной среды](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6).  
  
 **Название**  
 Отображает имя плана обслуживания. Имя нового плана обслуживания необходимо указать в диалоговом окне до открытия конструктора планов обслуживания. Чтобы переименовать план обслуживания, щелкните правой кнопкой мыши план в обозревателе объектов и выберите **Переименовать**.  
  
 **Описание**  
 Просмотрите или укажите описание для плана обслуживания. Максимальная длина описания составляет 512 знаков.  
  
 **Область конструктора**  
 Создание и обслуживание планов обслуживания. Используйте область конструктора, чтобы добавлять задачи обслуживания к плану, удалять задачи из плана, указывать ссылки очередности между задачами, а также для указания ветвления задач и параллелизма.  
  
 Ссылка очередности между двумя задачами устанавливает связь между ними. Вторая задача ( *зависимая*) выполняется только в том случае, если результат выполнения первой задачи ( *приоритетной*) удовлетворяет указанным критериям. Обычно оценка результата выполнения задается как **Успешно**, **Ошибка**или **Завершение**. Область конструктора планов обслуживания основана на области конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Дополнительные сведения см. в статье [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md).  
  
 Например, для задачи «Дефрагментация индекса» можно указать, что она должна выполняться только в случае, если предыдущая задача «Проверка целостности базы данных» была завершена успешно. Возможность ссылок очередности задач также позволяет управлять условиями обработки ошибок и сбоев в плане. Например, можно указать, что в случае неудачного выполнения задачи «Проверка целостности базы данных» задача «Оповещение оператора» сообщает пользователю или оператору о неудаче.  
  
 Указание задач, которые должны выполняться в случае неудачного выполнения предшествующей задачи, является примером *ветвления задач*.  
  
 Указание на то, что выполнение двух или более задач должно начаться одновременно, например после успешного завершения предшествующей задачи, является примером *параллелизма задач*. Все задачи, не имеющие ограничений, запускаются и выполняются одновременно. Чтобы отложить задачу до завершения предыдущей, используются ограничения.  
  
 После помещения задачи обслуживания в область конструктора ее свойства при необходимости могут быть изменены. Например, конкретная база данных, резервное копирование которой должно быть осуществлено задачей «Резервное копирование базы данных», указывается после того, как эта задача добавлена в план. Задачи в области конструктора, которые не были должным образом настроены, помечены красным значком с белым символом «x».  
  
 Чтобы добавить в план задачу обслуживания, перетащите значок задачи из области элементов **Задачи плана обслуживания** в область конструктора планов, или дважды щелкните задачу в области элементов, чтобы добавить ее в активную область конструктора. Если область элементов **Задачи плана обслуживания** не отображается, выберите пункт **Область элементов** в меню [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **среды** . Откройте узел **Задачи плана обслуживания** на панели **Область элементов** .  
  
 Чтобы удалить задачу из плана, выберите задачу в области конструктора и нажмите клавишу **DELETE** , либо щелкните правой кнопкой мыши задачу и выберите **Удалить**.  
  
 Чтобы установить очередность двух задач, вначале перетащите их в область конструктора, а затем щелкните задачу, которая должна выполняться первой (приоритетная задача) и перетащите стрелку к зависимой задаче. Когда ссылка очередности установлена, конструктор отображает стрелку, связывающую две задачи, причем приоритетная задача указывает на зависимую. Когда ссылка указывается впервые, по умолчанию ее ограничение устанавливается таким образом, что зависимая задача выполняется только в случае, если результатом выполнения приоритетной задачи будет **Успешно**.  
  
 Для изменения свойств ссылки очередности дважды щелкните ссылку, чтобы запустить **Редактор ограничений очередностью**. Он предоставляет много параметров для указания логических условий, определяющих выполнение зависимой задачи. Например, параметр **Результат выполнения** может быть установлен в значении **Ошибка**, и в этом случае зависимая задача выполняется только при неудачном выполнении приоритетной задачи. Изменить значение свойства ссылки, определяющего результат выполнения, на **Успешно**, **Ошибка**или **Завершение**можно, щелкнув правой кнопкой мыши ссылку и выбрав соответствующий пункт в контекстном меню.  
  
 Чтобы установить ветвление задач, сначала создайте ссылки очередности между двумя задачами. Затем поместите в область конструктора еще одну зависимую задачу, которая выполняется при условии, отличном от условия выполнения первой зависимой задачи. Щелкните предшествующую задачу и перетащите вторую стрелку от приоритетной задачи к зависимой. Чтобы изменить результат выполнения (**Успешно**, **Ошибка**или **Завершение**), вызывающий выполнение зависимой задачи, дважды щелкните ссылку со стрелкой и измените значение в поле **Результат выполнения** . Либо щелкните правой кнопкой мыши ссылку и выберите необходимый результат выполнения из контекстного меню.  
  
 Чтобы установить параллелизм задач, свяжите две или более зависимые задачи с одной и той же приоритетной задачей. Измените свойства ссылок приоритета таким образом, чтобы ссылки, указывающие на зависимые задачи, которые должны выполняться параллельно, имели одно и то же значение в полях результата выполнения.  
  
## <a name="additional-features-available-from-the-shortcut-menu"></a>Дополнительные функции, доступные из контекстного меню  
 Для просмотра дополнительных параметров выберите одну или более задач в область конструктора и щелкните правой кнопкой мыши, чтобы открыть контекстное меню. В дополнение к обычным пунктам **Вырезать**, **Копировать**, **Вставить**, **Удалить**и **Выбрать все**для некоторых задач становятся доступными следующие возможности.  
  
 **Добавить заметку**  
 Добавляет описательную заметку в область конструктора.  
  
 **Правка**  
 Открывает диалоговое окно «Свойства задачи».  
  
 **Отключить**  
 Делает задачу временно недоступной.  
  
 **Включить**  
 Восстанавливает отключенную задачу.  
  
 **Группирование**  
 Создает группу, содержащую одну или несколько задач.  
  
 **Разгруппировать**  
 Удаляет задачи из группы.  
  
 **Автомасштабирование**  
 Устанавливает оптимальный размер для каждой задачи.  
  
 **Свернуть**  
 Скрывает задачи в пределах группы.  
  
 **Развернуть**  
 Показывает задачи в группе, которые ранее были скрыты с помощью пункта **Свернуть**.  
  
 **Масштаб**  
 Изменяет размер задач в области конструктора  
  
## <a name="see-also"></a>См. также:  
 [Планы обслуживания](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Создание плана обслуживания](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
  