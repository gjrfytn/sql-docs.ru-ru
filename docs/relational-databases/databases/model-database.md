---
title: "База данных model | Документация Майкрософт"
ms.custom: 
ms.date: 03/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a05d89ba953bf683a992a087be8e3c87777ae9c4
ms.lasthandoff: 04/11/2017

---
# <a name="model-database"></a>База данных model
  База данных **model** используется в качестве шаблона для всех баз данных, созданных для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Так как база данных **tempdb** создается при каждом запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , база данных **model** всегда должна существовать в системе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Содержимое базы данных **model** (включая параметры базы данных) полностью копируется в новую базу данных. Некоторые параметры базы данных **model** используются также при создании новой базы данных **tempdb** во время загрузки, поэтому наличие базы данных **model** в системе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обязательно.  
  
 Вновь созданные пользовательские базы данных используют ту же [модель восстановления](../../relational-databases/backup-restore/recovery-models-sql-server.md) , что и база данных model. Пользователь может настроить значение по умолчанию. Дополнительные сведения о текущей модели восстановления см. в разделе [Просмотр или изменение модели восстановления базы данных (SQL Server)](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  В случае изменения базы данных **model** и внесения в нее пользовательских сведений шаблона рекомендуется сначала создать резервную копию базы данных **model**. Дополнительные сведения см. в разделе [Резервное копирование и восстановление системных баз данных (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="model-usage"></a>Использование базы данных model  
 При выполнении инструкции CREATE DATABASE первая часть базы данных создается путем копирования в нее содержимого базы данных **model** . Оставшаяся часть новой базы данных заполняется пустыми страницами.  
  
 При изменении базы данных **model** все созданные после этого базы данных унаследуют эти изменения. Например, можно установить разрешения или параметры базы данных или добавить такие объекты, как таблицы, функции или хранимые процедуры. Свойства файлов базы данных **model** являются исключением и не учитываются (за исключением первоначального размера файла данных). Исходный размер по умолчанию файла журнала и данных для шаблона базы данных составляет 8 МБ.  
  
## <a name="physical-properties-of-model"></a>Физические свойства базы данных model  
 В следующей таблице представлены начальные значения конфигурации данных и файлов журнала базы данных **model** .  
  
|Файл|Логическое имя|Физическое имя|Увеличение размера файлов|  
|----------|------------------|-------------------|-----------------|  
|Первичные данные|modeldev|model.mdf|Автоматическое увеличение на 64 МБ до заполнения диска.|  
|Журнал|modellog|modellog.ldf|Автоматическое увеличение на 64 МБ до максимального размера в 2 ТБ.|  
  
 Для версий младше [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]см. статью [Шаблон базы данных](https://msdn.microsoft.com/library/ms186388\(v=sql.120\).aspx)со значения роста файла по умолчанию.  
  
 Сведения о перемещении файлов базы данных и журналов **model** см. в разделе [Перемещение системных баз данных](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Параметры базы данных  
 В следующей таблице представлены значения по умолчанию для каждого параметра базы данных в базе данных **model** и обозначено, возможно ли изменение этого параметра. Чтобы просмотреть текущие настройки этих параметров, используйте представление каталога [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Параметр базы данных|Значение по умолчанию|Можно ли изменить|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Да|  
|ANSI_NULL_DEFAULT|OFF|Да|  
|ANSI_NULLS|OFF|Да|  
|ANSI_PADDING|OFF|Да|  
|ANSI_WARNINGS|OFF|Да|  
|ARITHABORT|OFF|Да|  
|AUTO_CLOSE|OFF|Да|  
|AUTO_CREATE_STATISTICS|ON|Да|  
|AUTO_SHRINK|OFF|Да|  
|AUTO_UPDATE_STATISTICS|ON|Да|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Да|  
|CHANGE_TRACKING|OFF|Нет|  
|CONCAT_NULL_YIELDS_NULL|OFF|Да|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Да|  
|CURSOR_DEFAULT|GLOBAL|Да|  
|Параметры доступности базы данных|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Нет<br /><br /> Да<br /><br /> Да|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Да|  
|DB_CHAINING|OFF|Нет|  
|ENCRYPTION|OFF|Нет|  
|MIXED_PAGE_ALLOCATION|ON|Нет|  
|NUMERIC_ROUNDABORT|OFF|Да|  
|PAGE_VERIFY|CHECKSUM|Да|  
|PARAMETERIZATION|SIMPLE|Да|  
|QUOTED_IDENTIFIER|OFF|Да|  
|READ_COMMITTED_SNAPSHOT|OFF|Да|  
|RECOVERY|Зависит от выпуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *|Да|  
|RECURSIVE_TRIGGERS|OFF|Да|  
|Параметры компонента Service Broker|DISABLE_BROKER|Нет|  
|TRUSTWORTHY|OFF|Нет|  
  
 * Дополнительные сведения о текущей модели восстановления базы данных см. в разделе [Просмотр или изменение модели восстановления базы данных (SQL Server)](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) или [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 Описание этих параметров баз данных см. в разделе [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Ограничения  
 Следующие операции не могут быть выполнены в базе данных **model** .  
  
-   добавление файлов или файловых групп;  
  
-   Изменение параметров сортировки. Параметрами сортировки по умолчанию являются параметры сортировки сервера.  
  
-   Изменение владельца базы данных. Владельцем**model** является **sa**.  
  
-   Удаление базы данных.  
  
-   Удаление пользователя **guest** из базы данных.  
  
-   Включение системы отслеживания измененных данных.  
  
-   Участие в зеркальном отображении базы данных.  
  
-   Удаление первичной файловой группы, первичного файла данных или файла журнала.  
  
-   Переименование базы данных или первичной файловой группы.  
  
-   Перевод базы данных в режим «вне сети» (OFFLINE).  
  
-   Перевод первичной файловой группы в режим READ_ONLY.  
  
-   Создание процедур, представлений или триггеров с помощью параметра WITH ENCRYPTION. Ключ шифрования привязывается к базе данных, в которой был создан объект. Зашифрованные объекты, созданные в базе данных **model** могут быть использованы только в базе данных **model**.  
  
## <a name="related-content"></a>См. также  
 [Системные базы данных](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Перемещение файлов базы данных](../../relational-databases/databases/move-database-files.md)  
  
  
