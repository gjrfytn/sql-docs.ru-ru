---
title: "SQL Server, объект Broker TO Statistics | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 54599c96e1a89b7d4e7ae102cc09efa3c0345bf9
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server, объект Broker TO Statistics
  Объект производительности SQLServer:Broker TO Statistics сообщает о том, сколько раз в диалогах компонента [!INCLUDE[ssSB](../../includes/sssb-md.md)] запрашиваются объекты передачи и как часто объекты передачи записываются в базу данных **tempdb**.  
  
 В объектах передачи записывается состояние передач сообщений для диалога компонента [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Они хранятся в памяти. Чтобы освободить память, компонент [!INCLUDE[ssSB](../../includes/sssb-md.md)] периодически записывает пакеты неактивных объектов передачи в рабочие таблицы базы данных **tempdb**.  
  
 В следующей таблице перечислены счетчики этого объекта.  
  
|Счетчики объекта SQL Server Broker TO Statistics|Description|  
|----------------------------------------------|-----------------|  
|**Средн. длина пакетов записи**|Среднее число объектов передачи, сохраняемых в пакете.|  
|**Средн. время записи пакета (мс)**|Среднее время в миллисекундах, необходимое для сохранения пакета объектов передачи.|  
|**Средн. время для базовой записи пакета (мс)**|Только для внутреннего применения.|
|**Средн. время между пакетами (мс)**|Среднее время в миллисекундах между записью пакетов объектов передачи.|  
|**Средн. базовое время между пакетами**|Только для внутреннего применения.| 
|**Получено объектов передачи/с**|Число раз в секунду, когда диалоги запрашивали объекты передачи.|  
|**Грязных объектов передачи/с**|Число раз в секунду, когда объекты передачи были отмечены как грязные. Объекты передачи отмечаются как грязные при первом изменении, которое приводит к тому, что копия в памяти отличается от копии в базе данных **tempdb**. Объекты передачи изменяются, когда компонент [!INCLUDE[ssSB](../../includes/sssb-md.md)] должен записать изменение в состоянии передач сообщений для диалога.|  
|**Запись объектов передачи/с**|Число раз в секунду, когда пакет объектов передачи был записан в рабочие таблицы базы данных **tempdb** . Большое число записей может говорить о нехватке памяти для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
## <a name="see-also"></a>См. также:  
 [SQL Server, объект Access Methods](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [SQL Server, объект Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  