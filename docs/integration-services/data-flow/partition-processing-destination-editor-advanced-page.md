---
title: "Редактор назначения обработки секций (страница &#171;Дополнительно&#187;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.partprocessingtransformation.advanced.f1"
helpviewer_keywords: 
  - "редактор назначения «Обработка секций»"
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Редактор назначения обработки секций (страница &#171;Дополнительно&#187;)
  Страница **Дополнительно** диалогового окна **Редактор назначения обработки секций** позволяет настроить обработку ошибок.  
  
 Дополнительные сведения о назначении для обработки секции см. в разделе [Partition Processing Destination](../../integration-services/data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Описанные здесь задачи не применимы к табличным моделям служб Analysis Services.  Нельзя связать входные столбцы со столбцами секционирования для табличных моделей. Вместо этого для обработки секции следует использовать задачу выполнения DDL [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) служб Analysis Services.  
  
## Параметры  
 **Использовать конфигурацию ошибок по умолчанию**  
 Укажите, нужно ли использовать обработку ошибок в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] по умолчанию. По умолчанию, присваивается значение **True**.  
  
 **Действие при возникновении ошибки ключа**  
 Укажите способ обработки записей с недопустимыми ключевыми значениями.  
  
|Значение|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Преобразовать неприемлемое значение ключа в значение Unknown.|  
|**DiscardRecord**|Удаляет запись.|  
  
 **Пропускать ошибки**  
 Указывает, что ошибки должны пропускаться.  
  
 **Остановить при возникновении ошибки**  
 Указывает, что в случае ошибки обработка должна прерываться.  
  
 **Количество ошибок**  
 Выберите порог ошибок, при достижении которого обработка должна закончиться, если выбран режим **Остановить при возникновении ошибки**.  
  
 **Действие при возникновении ошибки**  
 Если был выбран режим **Остановить при возникновении ошибки**, укажите действие, которое нужно выполнить при достижении порога ошибок.  
  
|Значение|Description|  
|-----------|-----------------|  
|**StopProcessing**|Останавливает обработку.|  
|**StopLogging**|Останавливает ведение журнала ошибок.|  
  
 **Ключ не найден**  
 Укажите действие при ошибке «Ключ не найден». По умолчанию, присваивается значение **Сообщить и продолжить**.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Повторяющийся ключ**  
 Указывает действие при ошибке «Повторяющийся ключ». По умолчанию, присваивается значение **Пропустить ошибку**.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Ключ NULL преобразован в неизвестный**  
 Выберите действие для ситуации, когда ключ NULL был преобразован в значение Unknown. По умолчанию, присваивается значение **Пропустить ошибку**.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Ключ NULL не допускается**  
 Указывает действие при обнаружении ключа NULL в случае запрета ключей NULL. По умолчанию, присваивается значение **Сообщить и продолжить**.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Путь к журналу ошибок**  
 Введите путь для журнала ошибок или выберите место назначения, нажав кнопку обзора **(...)**.  
  
 **Обзор (...)**  
 Укажите путь к журналу ошибок.  
  
## См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Редактор назначения "Обработка секций" (страница "Сопоставления")](../../integration-services/data-flow/partition-processing-destination-editor-mappings-page.md)  
  
  