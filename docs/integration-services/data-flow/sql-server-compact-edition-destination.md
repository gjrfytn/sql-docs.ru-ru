---
title: "Назначение &#171;SQL Server Compact Edition&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sqlservercompactdest.f1"
helpviewer_keywords: 
  - "назначения [службы Integration Services], SQL Server Compact"
  - "SQL Server Compact, назначение"
  - "вставка данных"
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
caps.latest.revision: 56
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 56
---
# Назначение &#171;SQL Server Compact Edition&#187;
  Назначение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact записывает данные в базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  На 64-разрядном компьютере пакеты, которые соединяются с источниками данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, должны запускаться в 32-разрядном режиме. Поставщик [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, используемый службами [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] для соединения с источниками данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, доступен только в 32-разрядной версии.  
  
 Настройка назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact производится путем указания имени таблицы, в которую назначение SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact вставляет данные. Пользовательское свойство TableName назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact содержит имя таблицы.  
  
 Назначение использует диспетчер соединений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, чтобы подключиться к источнику данных; диспетчер соединений определяет поставщик OLE DB для использования. Дополнительные сведения см. в разделе [Диспетчер соединений SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 Назначение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact содержит пользовательское свойство TableName, которое может быть обновлено выражением свойства после загрузки пакета. Дополнительные сведения см. в разделах [Выражения служб Integration Services (SSIS)](../../integration-services/expressions/integration-services-ssis-expressions.md), [Использование выражений свойств в пакетах](../../integration-services/expressions/use-property-expressions-in-packages.md) и [Пользовательские свойства назначения SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md).  
  
 Назначение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact имеет один вход и не поддерживает вывод ошибок.  
  
## Настройка назначения SQL Server Compact Edition  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства назначения «SQL Server»](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
## Связанные задачи  
 Дополнительные сведения о настройке свойств компонента см. в разделе [Установление свойств компонента потока данных](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## См. также  
 [Поток данных](../../integration-services/data-flow/data-flow.md)  
  
  