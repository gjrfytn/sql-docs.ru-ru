---
title: "cлужба &#171;Модуль записи SQL&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "VDI [SQL Server]"
  - "восстановление [SQL Server] модуль записи SQL"
  - "резервные копии [SQL Server], во время работы SQL Server"
  - "служба «Теневое копирование томов»"
  - "резервные копии томов во время работы [SQL Server]"
  - "интерфейс виртуальных устройств резервного копирования [SQL Server]"
  - "cлужба «Модуль записи SQL»"
  - "службы [SQL Server], модуль записи SQL"
  - "модуль записи MSDE"
  - "VSS"
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# cлужба &#171;Модуль записи SQL&#187;
  Служба «Модуль записи SQL» предоставляет дополнительные возможности резервного копирования и восстановления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью механизма службы теневого копирования тома.  
  
 Служба «Модуль записи SQL» устанавливается автоматически. Она должна запускаться при запросе службы теневого копирования томов (VSS) резервного копирования или восстановления. Служба настраивается с помощью оснастки «Службы» [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Служба модуля записи SQL устанавливается на всех операционных системах.  
  
## Назначение  
 Во время работы компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] блокирует файлы данных и обладает монопольными правами доступа к ним. Если служба «Модуль записи SQL» не запущена, то у программ резервного копирования, работающих в Windows, нет доступа к файлам данных, а резервное копирование должно выполняться с помощью функции резервного копирования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Служба «Модуль записи SQL» позволяет во время работы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешить программам резервного копирования Windows копирование файлов данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## служба «Теневое копирование томов»  
 Служба теневого копирования томов — это набор API-интерфейсов COM, которые обеспечивают платформу для реализации резервного копирования томов во время записи приложениями данных в эти тома. В службе теневого копирования томов предусмотрен согласованный интерфейс, обеспечивающий координацию пользовательских приложений, обновляющих данные на диске (модулей записи) и программ, выполняющих резервное копирование приложений (генераторов запросов).  
  
 Служба теневого копирования томов захватывает и копирует стабильные образы для резервного копирования в работающих системах, особенно на серверах. При этом не происходит чрезмерного понижения производительности и стабильности работы служб. Дополнительные сведения о службе теневого копирования томов см. в документации по Windows.  
  
## Интерфейс виртуальных устройств резервного копирования (VDI)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] включает API с названием "Интерфейс виртуальных устройств резервного копирования" (VDI), который позволяет независимым поставщикам программного обеспечения встраивать [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в их продукты для поддержки операций резервного копирования и восстановления. Эти функции API обеспечивают максимальную надежность и производительность, а также поддерживают все функции резервного копирования и восстановления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], включая полный набор возможностей оперативного и моментального резервного копирования.  
  
## Разрешения  
 Служба «Модуль записи SQL» должна запускаться под учетной записью **Local System** . Модуль записи SQL использует имя входа **NT Service\SQLWriter** при подключении к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. С помощью имени входа **NT Service\SQLWriter** процесс записи SQL может запускаться на более низком уровне прав доступа в учетной записи, помеченной как **без имени входа**, что снижает потенциальную уязвимость. Если модуль записи SQL отключен, то каждая служебная программа, которая полагается на моментальные снимки VSS, например System Center Data Protection Manager, а также некоторые другие продукты сторонних поставщиков, перестанет работать и будет сбоить с риском принятия нецелостных резервных копий баз данных. Если ни службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ни система, где они выполняются, ни система их размещения (в случае виртуальной машины) не нуждаются в чем-либо помимо резервного копирования [!INCLUDE[tsql](../../includes/tsql-md.md)], то модуль записи SQL можно спокойно отключить и удалить имя входа.  Обратите внимание, что модуль записи SQL может вызываться системой или резервной копией тома независимо от того, использует ли копия моментальные снимки напрямую или нет. Некоторые продукты для резервного копирования системы используют службу VSS во избежание блокировки по открытым или заблокированным файлам. Модулю записи SQL требуются повышенные разрешения в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], поскольку во время его работы на короткий момент времени замораживаются все операции ввода и вывода для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Функции  
 Служба «Модуль записи SQL» поддерживает:  
  
-   полное резервное копирование и восстановление баз данных, включая полнотекстовые каталоги;  
  
-   разностное резервное копирование и восстановление;  
  
-   восстановление с перемещением;  
  
-   переименование базы данных;  
  
-   резервная копия, предназначенная только для копирования;  
  
-   автоматическое восстановление моментального снимка базы данных.  
  
 Служба «Модуль записи SQL» не поддерживает:  
  
-   Резервные копии журналов;  
  
-   Резервное копирование файлов и файловых групп;  
  
-   Восстановление страницы  
  
  