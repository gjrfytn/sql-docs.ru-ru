---
title: "Очистка метаданных слияния (программирование репликации на языке Transact-SQL) | Документация Майкрософт"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 847a42192c396dcda29ed214e279f00d991a4eb0
ms.lasthandoff: 04/11/2017

---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>очистить метаданные слияния (программирование репликации на языке Transact-SQL)
  Агент слияния периодически чистит метаданные репликации слиянием в зависимости от заданного срока хранения публикации. Это происходит на издателе и подписчике в системных таблицах [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)и [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . Данные в этих таблицах могут чиститься и программным путем с помощью хранимых процедур репликации.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Очистка метаданных слияния вручную  
  
1.  В базе данных публикации на издателе выполните хранимую процедуру [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md).  
  
2.  Обратите внимание на то, что количество строк , удаляемых в шаге 1 из системных таблиц [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)и [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) , выводится, соответственно, в выходных параметрах **@num_genhistory_rows**, **@num_contents_rows**и **@num_tombstone_rows** (необязательно).  
  
3.  Повторите шаги 1 и 2 на подписчике для очистки метаданных в базе данных подписки.  
  
## <a name="see-also"></a>См. также:  
 [Окончание срока действия и отключение подписки](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  