---
title: "MSSQL_REPL027056 | Документация Майкрософт"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1423e3639f64a4d82cf89fb16d7b849e445b0ed0
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>Сведения о сообщении  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|27056|  
|Источник события|MSSQLSERVER|  
|Компонент|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Символическое имя||  
|Текст сообщения|Процессу слияния не удалось изменить журнал поколений в '%1'. В целях диагностики запустите синхронизацию повторно, включив подробное протоколирование и укажите выходной файл для записи.|  
  
## <a name="explanation"></a>Объяснение  
 Эта ошибка обычно возникает в результате состязания между чрезмерно увеличившимися системными таблицами репликации слиянием. Большой размер системных таблицы обычно обусловлен длительным сроком хранения публикации, поскольку метаданные должны сохраняться в этих таблицах до тех пор, пока не закончится срок хранения.  
  
## <a name="user-action"></a>Действие пользователя  
 **Способы устранения проблемы.**  
  
1.  Уменьшите значение параметров**DownloadGenerationsPerBatch** и **-UploadGenerationsPerBatch** агента слияния, чтобы разрешить продолжение обработки, пока устраняются причины ошибки. Параметры агента могут задаваться в профилях агента или в командной строке. Дополнительные сведения см. в разделе:  
  
    -   [Работа с профилями агента репликации](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Просмотр и изменение параметров командной строки агента репликации (среда SQL Server Management Studio)](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Укажите наименьшее возможное значение срока хранения публикации. Дополнительные сведения см. в статье [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
3.  Обслуживая репликацию слиянием, иногда проверяйте увеличение размера системных таблиц, связанных с репликацией слиянием: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**и **MSmerge_past_partition_mappings**. Время от времени проводите повторную индексацию этих таблиц. Дополнительные сведения см. в статье [Реорганизация и перестроение индексов](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="see-also"></a>См. также:  
 [Справочник по ошибкам и событиям (репликация)](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  