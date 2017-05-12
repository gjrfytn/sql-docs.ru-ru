---
title: "Переименование многомерной базы данных (службы Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "переименование баз данных"
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 20
---
# Переименование многомерной базы данных (службы Analysis Services)
  Способ изменения имени базы данных служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] зависит от способа подключения к базе данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Чтобы изменить имя существующей базы данных, необходимо подключиться к ней в режиме в сети. Чтобы изменить имя базы данных, в которой будут создаваться экземпляры объектов проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , необходимо подключиться к ней в режиме проекта.  
  
### Изменение имени базы данных в режиме в сети  
  
1.  Используя среду [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], подключитесь напрямую к базе данных [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  В обозревателе решений щелкните правой кнопкой мыши базу данных, после чего выберите пункт **Изменить базу данных**.  
  
3.  В текстовом поле **Имя базы данных** измените имя базы данных.  
  
4.  На панели инструментов щелкните **Сохранить** или **Сохранить все** , щелкните **Сохранить выбранные элементы** или **Сохранить все** в меню **Файл** , или закройте **Конструктор баз данных** и при появлении запроса нажмите кнопку **Сохранить** .  
  
     Имя базы данных обновится в экземпляре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , а объекты базы данных обновятся в обозревателе решений.  
  
### Изменение имени базы данных в проектном режиме  
  
1.  Откройте проект служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  В обозревателе решений щелкните правой кнопкой мыши проект служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и выберите пункт **Свойства**.  
  
3.  В диалоговом окне **Страницы свойств** в разделе **Свойства конфигурации** выберите пункт **Развертывание** .  
  
4.  Измените свойство **База данных** на новое имя базы данных.  
  
     В следующий раз при развертывании проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] он будет развернут с новым именем базы данных. Если база данных уже существует, она будет перезаписана.  
  
### Изменение имени базы данных с помощью среды SQL Server Management Studio.  
  
-   Щелкните правой кнопкой базу данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и измените свойство "Имя".  
  
## См. также  
 [Свойства сервера в службах Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Задание свойств многомерной базы данных (службы Analysis Services)](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [Настройка свойств проекта служб Analysis Services (среда SSDT)](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Развертывание проектов служб Analysis Services (среда SSDT)](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  