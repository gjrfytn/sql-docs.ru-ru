---
title: "Назначение HDFS-файлов | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.hdfsfiledest.f1"
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Назначение HDFS-файлов
  Компонент назначения HDFS-файлов позволяет записывать данные в пакете служб SSIS в HDFS-файл. Поддерживаются следующие форматы файлов: Text, Avro и ORC.  
  
 Чтобы настроить назначение HDFS-файлов, перетащите источник HDFS-файлов в конструктор потоков данных и дважды щелкните компонент, чтобы открыть редактор.  
  
 ![HDFS File Destination Editor](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS File Destination Editor")  
  
## Параметры  
 Настройте следующие параметры на вкладке **Общие** в диалоговом окне **Hadoop File Destination Editor** (Редактор назначения файлов Hadoop).  
  
|Поле|Description|  
|-----------|-----------------|  
|**Hadoop Connection (Подключение Hadoop)**|Укажите существующий диспетчер подключений Hadoop или создайте новый. Этот диспетчер подключений указывает, где размещены HDFS-файлы.|  
|**Путь к файлу**|Укажите имя HDFS-файла.|  
|**Формат файла**|Укажите формат HDFS-файла. Доступны следующие значения: Text, Avro и ORC.|  
|**Знак-разделитель столбцов**|Если выбран текстовый формат, укажите знак-разделитель столбцов.|  
|**Имена столбцов в первой строке данных**|Если выбран текстовый формат, укажите, будет ли первая строка файла содержать имена столбцов.|  
  
 После настройки этих параметров перейдите на вкладку **Столбцы**, чтобы сопоставить исходные столбцы с целевыми столбцами в потоке данных.  
  
## См. также  
 [Диспетчер подключений Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Источник "Файл HDFS"](../../integration-services/data-flow/hdfs-file-source.md)  
  
  