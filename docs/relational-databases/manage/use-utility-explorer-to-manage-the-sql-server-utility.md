---
title: "Использование проводника служебной программы для управления служебной программой SQL Server | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd65300d9d3c79ea0604d6ea83c1c9377b7982cc
ms.lasthandoff: 04/11/2017

---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>Использование проводника служебных программ для управления служебной программой SQL Server
  Проводник служебной программы, компонент среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], подключается к экземплярам компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] для отображения всех объектов в служебной программе представления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в виде дерева. Панель содержимого обозревателя программ предоставляет несколько способов просмотра сводных и подробных данных о состоянии исправности ресурсов управляемых экземпляров SQL Server. Обозреватель программ также реализует пользовательский интерфейс для просмотра определений политик и управления ими. Возможности обозревателя программ немного различаются в зависимости от объектов, представленных в служебной программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , однако в целом они охватывают объекты, данные и политики, управляемые служебной программой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [Функции и задачи служебной программы SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="create-utility-control-point"></a>Создание пункта управления программой  
 Перед использованием программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] необходимо создать пункт управления программой. Дополнительные сведения см. в статье [Функции и задачи служебной программы SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md) или [Создание точки управления служебной программой SQL Server (служебная программа SQL Server Utility)](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>Регистрация экземпляра SQL Server или приложения уровня данных из обозревателя программ  
 Регистрация экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняется просто. В обозревателе программ щелкните правой кнопкой мыши узел **Управляемые экземпляры** и выберите команду **Добавить управляемый экземпляр**. Выполните шаги мастера, чтобы завершить операцию. Дополнительные сведения см. в статье [Регистрация экземпляра SQL Server (служебная программа SQL Server Utility)](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
 Чтобы развернуть приложение уровня данных на экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], управляемом в программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], перейдите на вкладку **Обозреватель объектов**, раскройте узел **Управление** и щелкните правой кнопкой мыши элемент **Приложения уровня данных**. В меню правой кнопки мыши выберите команду **Развернуть приложение уровня данных**. Дополнительные сведения см. в статье [Развертывание приложения уровня данных](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md).  
  
## <a name="viewing-utility-explorer"></a>Отображение обозревателя программ  
 По умолчанию обозреватель программ не отображается в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Если обозреватель объектов отсутствует в пользовательском интерфейсе среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , в меню **Вид** выберите пункт **Обозреватель программ**. Чтобы открыть панель содержимого обозревателя программ, в меню **Вид** выберите пункт **Содержимое обозревателя программ**.  
  
## <a name="viewing-objects-in-utility-explorer"></a>Просмотр объектов в обозревателе программ  
 На панели навигации и панели содержимого обозревателя служебных программ отображаются данные, объекты и политики, управляемые служебной программой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . На панели навигации указывается, какие сведения будут отображаться на панели мониторинга и в точках просмотра, а панель содержимого и вкладки подробностей служат для доступа к данным и сведениям политик для объектов, управляемых служебной программой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="sql-server-utility-navigation-pane"></a>Панель навигации служебной программы SQL Server  
 Панель навигации обозревателя программ предоставляет дерево объектов служебной программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , сгруппированных по пункту управления программой. Чтобы раскрыть папку, щелкните знак «плюс» (+) или дважды щелкните имя пункта управления программой панели навигации обозревателя программ. Для выполнения стандартных задач щелкните правой кнопкой мыши папку или объект. Дерево включает следующие узлы.  
  
-   Верхним узлом в дереве является пункт управления программой. Имя узла состоит из следующих частей: "Имя_программы" (Имя_компьютера\имя_экземпляра_пункта_управления_программой). Если пункт управления программой отсутствует, его необходимо создать. Если отсутствует соединение с программой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо установить его. Дополнительные сведения см. в разделе [Функции и задачи служебной программы SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md). Чтобы отобразить данные на панели содержимого обозревателя служебной программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], щелкните имя пункта управления программой в дереве. Дополнительные сведения см. в статье [Панель мониторинга программ (служебная программа SQL Server)](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1).  
  
     Щелкните правой кнопкой мыши узел пункта управления программой (UCP), чтобы обновить данные на панели управления.  
  
-   Щелкните в дереве узел **Развернутые приложения уровня данных** , чтобы открыть список данных на панели содержимого служебной программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . На вкладках подробностей, расположенных внизу панели содержимого, представлены данные по загрузке ЦП и использованию хранилища, а также определения политик и сведения о свойствах отдельных приложений уровня данных, зарегистрированных в программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Дополнительные сведения см. в статье [Подробные сведения о развернутом приложении уровня данных (служебная программа SQL Server)](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
     Щелкните правой кнопкой мыши узел **Развернутые приложения уровня данных** в дереве, чтобы получить доступ к параметрам фильтра или обновить данные в списке.  
  
-   Щелкните в дереве узел **Управляемые экземпляры** , чтобы открыть список данных на панели содержимого программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . На дополнительных вкладках, расположенных внизу панели содержимого, представлены данные по загрузке ЦП и использованию томов хранилища, а также определения политик и сведения о свойствах отдельных управляемых экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , зарегистрированных в служебной программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в статье [Подробные сведения об управляемом экземпляре (служебная программа SQL Server)](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
     Щелкните правой кнопкой мыши узел **Управляемые экземпляры** в представлении в виде дерева, чтобы добавить управляемые экземпляры [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в служебную программу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также получить доступ к параметрам фильтра или обновить данные в списке.  
  
-   Щелкните узел **Администрирование программ** в представлении в виде дерева, чтобы получить доступ к определениям глобальных политик для всех управляемых экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и развернутых приложений уровня данных, зарегистрированных в служебной программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], просмотреть сведения об администрировании пункта управления программой и получить доступ к параметрам настройки хранилища данных управления служебной программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в статье [Администрирование программ (служебная программа SQL Server)](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Кроме того, с помощью элементов управления на вкладке **Политика** можно изменять чувствительность для сообщений о нарушениях политик. Дополнительные сведения см. в статье [Уменьшение уровня шума в политиках загрузки ЦП (служебная программа SQL Server)](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Щелкните правой кнопкой мыши узел **Администрирование программ** в дереве, чтобы обновить данные на панели содержимого.  
  
### <a name="sql-server-utility-dashboard"></a>Панель мониторинга служебной программы SQL Server  
 При выборе узла пункта управления программой в представлении в виде дерева обозревателя программ панель мониторинга служебной программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в области содержимого обозревателя программ заполняется данными. На панели мониторинга представлены сводные данные о состоянии всех экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и приложений уровня данных, управляемых в служебной программе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также общем использовании хранилища для объектов, управляемых служебной программой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в статье [Панель мониторинга программ (служебная программа SQL Server)](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1). Сведения о регистрации или удалении экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] см. в статьях [Регистрация экземпляра SQL Server (служебная программа SQL Server)](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md), [Развертывание приложения уровня данных](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md) или [Удаление экземпляра SQL Server с помощью служебной программы SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>Фильтрация списка объектов в области содержимого обозревателя программ  
 Если узел содержит большое число объектов, поиск нужного объекта может быть затруднен. В таких случаях следует уменьшить размер списка, используя функцию фильтра обозревателя программ. Например, может потребоваться найти определенный экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или только компьютеры с большим объемом свободного файлового пространства. Щелкните правой кнопкой мыши папку, которую требуется отфильтровать, нажмите кнопку фильтра, а затем кнопку **Параметры фильтра** , чтобы открыть диалоговое окно "Параметры фильтра обозревателя программ". Фильтровать список можно по имени, ЦП компьютера, ЦП экземпляра, файловому пространству, пространству тома, параметрам переопределения политик или последнему времени получения отчетов. В раскрывающихся списках в столбцах **Оператор** и **Значение** приведены дополнительные операторы фильтрации.  
  
### <a name="starting-powershell"></a>Запуск PowerShell  
 Сеанс PowerShell можно запустить, щелкнув любую папку или объект в дереве обозревателя объектов правой кнопкой мыши и выбрав пункт **Запустить Powershell**. В результате этого запускается сеанс PowerShell с поддержкой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, в котором установлен путь к объекту, выбранному щелчком правой кнопкой мыши в обозревателе объектов. После этого можно вводить команды PowerShell в интерактивной среде PowerShell. Дополнительные сведения см. в статье [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
 В PowerShell отсутствует справка F1, но содержится командлет **Get-Help** , позволяющий получить сведения об использовании PowerShell. Дополнительные сведения об использовании Get-Help см. в статье [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
## <a name="see-also"></a>См. также:  
 [Функции и задачи служебной программы SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Настройка политик исправности (служебная программа SQL Server)](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)   
 [Обозреватель объектов](http://msdn.microsoft.com/library/469ea8e2-79b9-44c8-bb6f-f0e1c5dbf0f2)  
  
  