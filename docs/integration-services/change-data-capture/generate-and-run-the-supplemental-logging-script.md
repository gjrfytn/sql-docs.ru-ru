---
title: "Создание и запуск скрипта дополнительного журналирования | Microsoft Docs"
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
  - "supLog"
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Создание и запуск скрипта дополнительного журналирования
  Страница «Настройка таблиц для отслеживания изменений» служит для запуска в базе данных-источнике Oracle скрипта для задания дополнительного журналирования.  
  
 **Запуск скриптов дополнительного журналирования**  
  
 Нажмите кнопку **Выполнить скрипт** , чтобы запустить скрипт дополнительного журналирования в таблицах, определенных для экземпляра CDC. Этот скрипт настраивает базу данных Oracle таким образом, что все интересующие столбцы будут записываться в журналы транзакций базы данных при регистрации операций UPDATE для отслеживаемых таблиц. Как правило, этот скрипт проверяет и выполняет системный администратор Oracle.  
  
 Скрипт также можно выполнить вручную с помощью программы SQL*Plus.  
  
 **Запуск скрипта вручную**  
  
 Щелкните **Копировать** , чтобы скопировать скрипт в буфер обмена. Запустите программу SQL*Plus и перейдите в каталог с базой данных-источником Oracle. Вставьте скрипт в SQL\*Plus, чтобы выполнить его.  
  
 Чтобы сохранить скрипт дополнительного журналирования в текстовый файл, щелкните **Сохранить как** и перейдите в каталог, куда необходимо сохранить файл. Введите имя файла и нажмите кнопку **Сохранить** , чтобы сохранить файл.  
  
 Нажмите кнопку **Далее** , чтобы перейти на страницу [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md).  
  
## См. также раздел  
 [Как создать экземпляр изменения базы данных SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Обзор и создание скриптов дополнительного журналирования](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  