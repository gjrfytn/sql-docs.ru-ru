---
title: "Свойства сервера (страница &#171;Процессоры&#187;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.serverproperties.processor.f1"
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Свойства сервера (страница &#171;Процессоры&#187;)
  Используйте эту страницу, чтобы просмотреть или изменить параметры процессоров. Настройки соответствия процессоров доступны только в случае, если в системе установлено более одного процессора.  
  
## Параметры  
 **Соответствие процессоров**  
 Связывает процессоры с определенными потоками, чтобы устранить чрезмерную нагрузку на процессоры и уменьшить количество переходов потоков между процессорами. Дополнительные сведения см. в разделе [Параметр конфигурации сервера "affinity mask"](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md).  
  
 **Привязка ввода-вывода**  
 Связывает операции дискового ввода-вывода [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с определенным подмножеством ЦП. Дополнительные сведения см. в разделе [Параметр конфигурации сервера "affinity Input-Output mask"](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md).  
  
 **Автоматически устанавливать маску соответствия для всех процессоров**  
 Позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливать соответствие процессоров.  
  
 **Автоматически устанавливать маску схожести ввода-вывода для всех процессоров**  
 Позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливать привязку ввода-вывода.  
  
 **Максимальное число потоков исполнителя.**  
 Значение 0 позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливать количество потоков исполнителя динамически. Эта настройка является наиболее подходящей для большинства систем. Однако в зависимости от конфигурации системы, присвоение этому параметру определенного значения иногда улучшает производительность. Дополнительные сведения см. в статье [Configure the max worker threads Server Configuration Option](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).  
  
 **Повысить приоритет SQL Server**  
 Указывает, следует ли [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выставить более высокий приоритет планирования [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows по сравнению с другими процессами на том же компьютере. Дополнительные сведения см. в статье [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).  
  
 **Использовать волокна Windows (использование упрощенных пулов)**  
 Использовать легковесные потоки (волокна) Windows вместо обычных потоков для службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Обратите внимание на то, что такая возможность доступна только в Windows 2003 Server Edition. Дополнительные сведения см. в разделе [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
 **Настроенные значения**  
 Отображает настроенные значения для параметров на этой панели. В случае изменения этих значений выберите пункт **Текущие значения** и посмотрите, вступили ли в силу внесенные изменения. В противном случае первым должен быть перезапущен экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Текущие значения**  
 Просмотр текущих значений для параметров на этой панели. Эти значения доступны только для чтения.  
  
## См. также:  
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  