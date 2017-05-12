---
title: "Устранение неполадок при переполнении журнала транзакций (ошибка SLQ Server 9002) | Документация Майкрософт"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
caps.latest.revision: 59
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 09bb30a44ef1675353fe8fa5bd9245c3f25c3894
ms.lasthandoff: 04/11/2017

---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Устранение неполадок при переполнении журнала транзакций (ошибка SLQ Server 9002)
  В этом разделе описаны возможные действия при переполнении журнала транзакций, а также советы о том, как его избежать. 
  
  Когда журнал транзакций переполняется, в компоненте [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] происходит ошибка **9002**. Журнал может заполниться, когда база данных работает в режиме "в сети" или находится в процессе восстановления. Если журнал заполняется, когда база данных находится в режиме «в сети», база данных остается в режиме «в сети», но доступной только для чтения, но не для обновления. Если журнал заполняется, когда база данных находится в процессе восстановления, компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] помечает базу данных как RESOURCE PENDING. В любом случае необходимо вмешательство пользователя, чтобы сделать журнал транзакций доступным.  
  
## <a name="responding-to-a-full-transaction-log"></a>Действия при переполнении журнала транзакций  
 Ответные действия при переполнении журнала транзакций частично зависят от условий, которые вызвали переполнение журнала. 
 
 Чтобы определить, что препятствует усечению журнала транзакций в конкретном случае, используйте столбцы **log_reuse_wait** и **log_reuse_wait_desc** представления каталога **sys.database**. Дополнительные сведения см. в разделе [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Описание причин, которые могут задержать усечение журнала, см. в разделе [Журнал транзакций (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> **ВАЖНО!**  
>  Если при возникновении ошибки 9002 база данных находилась в состоянии восстановления, то после устранения проблемы восстановите базу данных с помощью инструкции [ALTER DATABASE *имя_базы_данных* SET ONLINE.](https://msdn.microsoft.com/library/bb522682.aspx)  
  
 При переполнении журнала транзакций предусмотрены следующие ответные действия:  
  
-   создание резервной копии журнала;  
  
-   освобождение места на диске, чтобы журнал мог автоматически расти;  
  
-   перемещение файла журнала на диск с достаточным объемом свободного места;  
  
-   увеличение размера файла журнала;  
  
-   добавление файла журнала на другой диск;  
  
-   завершение или уничтожение длительной транзакции.  
  
 Эти возможности описаны в следующих разделах. Выберите ответное действие, наиболее подходящее в конкретной ситуации.  
  
## <a name="back-up-the-log"></a>Резервное копирование журнала  
 Для полных моделей восстановления и моделей с неполным протоколированием резервное копирование может предотвратить усечение журнала транзакций, если оно не было сделано недавно. Если резервная копия журнала создается в первый раз, **следует сделать вторую резервную копию журнала** , чтобы разрешить компоненту [!INCLUDE[ssDE](../../includes/ssde-md.md)] усечение журнала до точки последнего резервного копирования. Усечение журнала освобождает пространство для новых записей журнала. Чтобы избежать повторного переполнения журнала, следует чаще выполнять резервное копирование.  
  
 **Создание резервной копии журнала транзакций**  
  
> **ВАЖНО**  
>  Если база данных повреждена, см. раздел [Резервные копии заключительного фрагмента журнала (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
-   [Создание резервной копии журнала транзакций (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Освобождение места на диске  
 Возможно, следует освободить место на диске, где находится файл журнала транзакций для базы данных. Для этого можно удалить или переместить другие файлы. Освобожденное место на диске позволит системе восстановления автоматически увеличить размер файла журнала.  
  
### <a name="move-the-log-file-to-a-different-disk"></a>Перемещение файла журнала на другой диск  
 Если на текущем диске невозможно освободить достаточное количество места, следует переместить файл на другой диск, где места достаточно.  
  
> **ВАЖНО!** Файлы журнала ни в коем случае не следует размещать в файловых системах со сжатием.  
  
 **Перемещение файла журнала**  
  
-   [Перемещение файлов базы данных](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>Увеличение размера файла журнала  
 Если на диске, на котором находится журнал, доступно свободное место, можно увеличить размер файла журнала. Максимальный объем файлов журнала составляет 2 терабайта (ТБ) на файл журнала.  
  
 **Увеличение размера файла**  
  
 Если автоувеличение отключено, база данных находится в режиме «в сети» и на диске достаточно свободного места, выполните одно из следующих действий.  
  
-   Вручную увеличьте размер файла для получения одного шага роста размера файла.  
  
-   Включить свойство автоматического увеличения при помощи инструкции ALTER DATABASE, чтобы установить отличное от нуля значение шага роста для параметра FILEGROWTH.  
  
> **ПРИМЕЧАНИЕ.** В любом случае, если достигнут текущий предел размера файла, увеличьте значение MAXSIZE.  
  
### <a name="add-a-log-file-on-a-different-disk"></a>Добавление файла журнала на другой диск  
 Добавьте новый файл журнала базы данных на другом диске, где достаточно места, с помощью инструкции ALTER DATABASE <имя_базы_данных> ADD LOG FILE.  
  
 **Добавление файла журнала**  
  
-   [Добавление файлов данных или журналов в базу данных](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>Завершение длительной транзакции
### <a name="discovering-long-running-transactions"></a>Обнаружение длительных транзакций
Очень длительная транзакция может привести к переполнению журнала транзакций. Длительные транзакции можно обнаружить следующими способами:
 - **[sys.dm_tran_database_transactions](https://msdn.microsoft.com/library/ms186957.aspx).**
Данное динамическое административное представление возвращает сведения о транзакциях на уровне базы данных. Столбцы этого представления содержат сведения о времени первой записи журнала [(database_transaction_begin_time)](https://msdn.microsoft.com/library/ms186957.aspx), текущем состоянии транзакции [(database_transaction_state)](https://msdn.microsoft.com/library/ms186957.aspx)и [регистрационном номере (LSN)](https://msdn.microsoft.com/library/ms191459.aspx) первой записи в журнале транзакций [(database_transaction_begin_lsn)](https://msdn.microsoft.com/library/ms186957.aspx).

 - **[DBCC OPENTRAN](https://msdn.microsoft.com/library/ms182792.aspx).**
Эта инструкция позволяет установить идентификатор владельца транзакции, таким образом, можно отследить источник транзакции для более упорядоченной остановки (фиксацией, а не откатом).

### <a name="kill-a-transaction"></a>Завершение транзакции
В некоторых случаях может потребоваться завершить процесс, для этого можно применить инструкцию [KILL](https://msdn.microsoft.com/library/ms173730.aspx) . Ее следует использовать с осторожностью, особенно если запущены критические процессы, которые нельзя завершать. Дополнительные сведения см. в разделе [KILL (Transact-SQL)](https://msdn.microsoft.com/library/ms173730.aspx).

## <a name="see-also"></a>См. также:  
[Статья базы знаний — неожиданное увеличение или переполнение журнала транзакций в SQL Server](https://support.microsoft.com/en-us/kb/317375)
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Управление размером файла журнала транзакций](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [Резервные копии журналов транзакций (SQL Server)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
