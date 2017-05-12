---
title: "Свойства сети | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "LingerTimeout, свойство"
  - "EnableNagleAlgorithm, свойство"
  - "MinPendingAcceptExCount, свойство"
  - "MaxPendingSendCount, свойство"
  - "EnableBinaryXML, свойство"
  - "MinPendingReceiveCount, свойство"
  - "MaxCompletedReceiveCount, свойство"
  - "DisableNonblockingMode, свойство"
  - "RequestSizeThreshold, свойство"
  - "CompressionLevel, свойство"
  - "ReceiveBufferSize, свойство"
  - "EnableCompression, свойство"
  - "ServerSendTimeout, свойство"
  - "IPV4Support, свойство"
  - "MaxPendingReceiveCount, свойство"
  - "MaxPendingAcceptExCount, свойство"
  - "IPV6Support, свойство"
  - "MaxAllowedRequestSize, свойство"
  - "ServerReceiveTimeout, свойство"
  - "EnableLingerOnClose, свойство"
  - "InitialConnectTimeout, свойство"
  - "SendBufferSize, свойство"
  - "ScatterReceiveMultiplier, свойство"
  - "свойства сети [службы Analysis Services]"
ms.assetid: ef4251e2-abe5-4c5b-9868-7549782d0244
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# Свойства сети
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] поддерживают свойства сервера, перечисленные в следующих таблицах. Дополнительные сведения о дополнительных свойствах сервера и их настройке см. в разделе [Свойства сервера в службах Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Область применения:** многомерный и табличный режим сервера  
  
## Общие сведения  
 **ListenOnlyOnLocalConnections**  
 Логическое свойство, указывающее прослушивание только локальных соединений, например локального сервера.  
  
## Средство прослушивания  
 **IPV4Support**  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее поддержку протокола IPv4. Это свойство имеет одно из значений, содержащихся в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|*0*|Протокол IPv4 отключен; подключение клиентов невозможно.|  
|*1*|(По умолчанию) необходим протокол IPv4; сервер невозможно запустить без прослушивания по IPv4.|  
|*2*|Дополнительный протокол IPv4; сервер пытается прослушать по протоколу IPv4, но запускается в любом случае.|  
  
 **IPV6Support**  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее поддержку протокола IPv6. Это свойство имеет одно из значений, содержащихся в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|*0*|Протокол IPv6 отключен; подключение клиентов невозможно.|  
|*1*|(По умолчанию) необходим протокол IPv6; сервер невозможно запустить без прослушивания по IPv6. |  
|*2*|Дополнительный протокол IPv6; сервер пытается прослушать по протоколу IPv6, но запускается в любом случае.|  
  
 **MaxAllowedRequestSize**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RequestSizeThreshold**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerReceiveTimeout**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ServerSendTimeout**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## Запросы  
 **EnableBinaryXML**  
 Логическое свойство, определяющее, распознает ли сервер запросы в двоичном XML-формате.  
  
 **EnableCompression**  
 Логическое свойство, определяющее сжатие запросов.  
  
## Ответы  
 **CompressionLevel**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **EnableBinaryXML**  
 Логическое свойство, определяющее включение на сервере двоичных XML-ответов.  
  
 **EnableCompression**  
 Логическое свойство, определяющее сжатие ответов клиентам.   
  
## TCP  
 **InitialConnectTimeout**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxCompletedReceiveCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingAcceptExCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingReceiveCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxPendingSendCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingAcceptExCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinPendingReceiveCount**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ScatterReceiveMultiplier**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ DisableNonblockingMode**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ EnableLingerOnClose**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\EnableNagleAlgorithm**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ LingerTimeout**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ ReceiveBufferSize**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SocketOptions\ SendBufferSize**  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## См. также  
 [Свойства сервера в службах Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Определение режима работы сервера экземпляра служб Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  