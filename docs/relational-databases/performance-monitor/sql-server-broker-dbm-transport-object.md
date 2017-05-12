---
title: "Брокер SQL Server, объект DBM Transport | Документация Майкрософт"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0bad82d13370dfba9e1067986d1f1789ecf006ec
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-broker---dbm-transport-object"></a>Брокер SQL Server, объект DBM Transport
  В объекте производительности **Broker/DBM Transport** содержатся счетчики производительности, сообщающие сведении о работе в сети служб Service Broker и зеркального отображения баз данных. В следующей таблице перечислены счетчики этого объекта.  
  
|Счетчик «SQL Server: Service Broker / транспорт зеркального отображения баз данных»|Описание|  
|------------------------------------------------|-----------------|  
|**Текущее число полученных байт**|Этот счетчик сообщает количество байт, считанных текущими запущенными транспортными операциями приема.|  
|**Текущее число отправленных байт**|Этот счетчик сообщает количество байт во фрагментах сообщений, которые в текущей момент посылаются по сети.|  
|**Текущее число отправленных фрагментов сообщений**|Этот счетчик сообщает общее число фрагментов сообщений, которые в текущей момент посылаются по сети.|  
|**Отправлено фрагментов сообщений P1/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 1, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P2/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 2, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P3/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 3, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P4/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 4, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P5/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 5, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P6/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 6, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P7/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 7, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P8/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 8, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P9/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 9, отправляемых по сети за одну секунду.|  
|**Отправлено фрагментов сообщений P10/с**|Этот счетчик содержит число фрагментов сообщений с приоритетом 10, отправляемых по сети за одну секунду.|  
|**Получено фрагментов сообщений в секунду**|Этот счетчик сообщает число фрагментов сообщений, принимаемых по сети за одну секунду.|   
|**Отправка фрагментов сообщений в сек.**|Этот счетчик сообщает число фрагментов сообщений всех приоритетов, посылаемых по сети за одну секунду.|  
|**Средний размер фрагмента получаемого сообщения**|Этот счетчик сообщает средний размер фрагментов сообщений, принимаемых по сети.|  
|**Базовое значение размера получаемого фрагмента сообщения**|Только для внутреннего применения.| 
|**Средний размер отправленных фрагментов сообщений**|Этот счетчик сообщает средний размер фрагментов сообщений, посылаемых по сети.|  
|**Средний базовый размер отправленных фрагментов сообщений**|Только для внутреннего применения.|
|**Число открытых соединений**|Этот счетчик сообщает число сетевых соединений, открытых на данный момент компонентом Service Broker.|  
|**Текущее число отложенных полученных байт**|Этот счетчик сообщает количество байт, содержащееся во фрагментах сообщений, принятых по сети, но еще не помещенных в очередь или не отмененных.|  
|**Текущее число отложенных отправленных байт**|Этот счетчик сообщает общее число байт во фрагментах сообщений, которые готовы к отправке по сети.|  
|**Текущее число отложенных полученных фрагментов**|Этот счетчик сообщает количество фрагментов сообщений, принятых по сети, но еще не помещенных в очередь или не отмененных.|  
|**Текущее число отложенных отправленных фрагментов**|Этот счетчик сообщает общее число фрагментов сообщений, готовых к отправке по сети.|  
|**Получение байт в сек.**|Этот счетчик сообщает число байт, принимаемых по сети конечными точками компонента Service Broker и зеркального отображения за одну секунду.|  
|**Общее число полученных байт**|Этот счетчик сообщает общее число байт, принятых по сети конечными точками компонента Service Broker и зеркального отображения.|  
|**Средняя длина получаемых данных**|Этот счетчик сообщает среднее число байт в транспортных операциях приема.|  
|**Баз. ср. длина полученного ввода-вывода**|Только для внутреннего применения.|
|**Получение операций ввода-вывода в секунду**|Этот счетчик сообщает количество транспортных операций ввода-вывода по приему, выполняемых транспортным слоем Service Broker / зеркального отображения за одну секунду. Обратите внимание, что транспортная операция приема может содержать более одного фрагмента сообщения.|  
|**Полученных буферных копий ввода-вывода в байтах в секунду**|Скорость перемещения фрагментов буфера в оперативной памяти во время операций ввода-вывода по приему на транспортном уровне.|
|**Полученных буферных копий ввода-вывода**|Число раз, когда операциям ввода-вывода по приему на транспортном уровне приходилось перемещать фрагменты буфера в оперативной памяти.| 
|**Отправка байт в сек.**|Этот счетчик сообщает число байтов, отправляемых по сети конечными точками компонента Service Broker и зеркального отображения за одну секунду.|   
|**Общее число отправленных байт**|Этот счетчик сообщает общее число байтов, отправленных по сети конечными точками компонента Service Broker и зеркального отображения.| 
|**Средняя длина отправляемых данных**|Этот счетчик сообщает среднее число байт для каждой транспортной операции отправки. Обратите внимание, что транспортная операция отправки может содержать более одного фрагмента сообщения.|  
|**Баз. ср. длина отправляемого ввода-вывода**|Только для внутреннего применения.|
|**Количество отправок данных в сек.**|Этот счетчик сообщает количество выполненных транспортных операций ввода-вывода по отправке за одну секунду. Обратите внимание, что транспортная операция отправки может содержать более одного фрагмента сообщения.|  
  
## <a name="see-also"></a>См. также:  
 [sys.dm_broker_forwarded_messages (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  