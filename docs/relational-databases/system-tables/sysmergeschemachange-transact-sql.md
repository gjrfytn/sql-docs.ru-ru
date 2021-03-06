---
title: sysmergeschemachange (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8cbe36230a513129ee8261dbf7fda1a592d1f732
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786286"
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит сведения о публикуемых статьях, формируемые агентом моментальных снимков. Эта таблица хранится в базах данных публикации и подписки.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|Идентификатор публикации.|  
|**artid**|**uniqueidentifier**|Идентификатор статьи.|  
|**schemaversion**|**int**|Номер последнего изменения схемы.|  
|**schemaguid**|**uniqueidentifier**|Уникальный идентификатор последней схемы.|  
|**SchemaType**|**int**|Тип изменения схемы:<br /><br /> **Значение -1** = недопустим.<br /><br /> **1** = команда SQL.<br /><br /> **2** = скрипт схемы.<br /><br /> **3** = собственный программа массового копирования (BCP).<br /><br /> **4** = символьная программа BCP.<br /><br /> **5** = последнее записанное поколение.<br /><br /> **6** = последнее отправленное поколение.<br /><br /> **7** = каталог.<br /><br /> **8** = приоритет.<br /><br /> **9** = срок хранения.<br /><br /> **10** = скрипт триггеров.<br /><br /> **11** = Alter table.<br /><br /> **12** = повторная инициализация.<br /><br /> **13** = ALTER TABLE (отличным от[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).<br /><br /> **14** = повторная инициализация с передачей.<br /><br /> **15** = ограничение и скрипт индекса.<br /><br /> **16** = Очистка метаданных.<br /><br /> **17** = обновление последнего отправленного поколения.<br /><br /> **18** = уровень обратной совместимости.<br /><br /> **19** = проверка данных подписчика.<br /><br /> **20** = оптимально секционирована.<br /><br /> **21** = специализированый Сопоставитель.<br /><br /> **22** = порядок обработки статей.<br /><br /> **23** = опубликовано в публикации транзакций.<br /><br /> **24** = Коррекция ошибок.<br /><br /> **25** = альтернативную папку моментальных снимков.<br /><br /> **26** = только для загрузки.<br /><br /> **27** = отслеживание удалений.<br /><br /> **40** = скрипт перед созданием моментального снимка.<br /><br /> **45** = скрипт после создания моментального снимка.<br /><br /> **46** = пользовательский скрипт по требованию.<br /><br /> **50** = заголовка моментального снимка begin.<br /><br /> **51** = конец заголовка моментального снимка.<br /><br /> **52** = анонс моментального снимка.<br /><br /> **53** = адрес протокола передачи файлов (FTP).<br /><br /> **54** = порт FTP.<br /><br /> **55** = подкаталог FTP.<br /><br /> **56** = сжатый моментальный снимок.<br /><br /> **57** = имя входа FTP.<br /><br /> **58** = пароль FTP.<br /><br /> **60** = скрипт перед созданием системы.<br /><br /> **61** = схема хранимой процедуры.<br /><br /> **62** = схема представления.<br /><br /> **63** = схема пользовательской функции.<br /><br /> **64** = Просмотр индексов.<br /><br /> **65** = расширенные свойства.<br /><br /> **66** = проверки.<br /><br /> **67** = команда SQL перед моментальным снимком.<br /><br /> **71** = Проверка динамического моментального снимка.<br /><br /> **80** = system таблица собственный BCP 9.0.<br /><br /> **81** = символ системной таблицы BCP 9.0.<br /><br /> **82** = system таблица собственный BCP 9.0 (только глобальные).<br /><br /> **83** = символ системной таблицы BCP 9.0 (только глобальные).<br /><br /> **84** = system таблица собственный BCP 9.0 (облегченные).<br /><br /> **85** = символ системной таблицы BCP 9.0 (облегченные).<br /><br /> **128** = динамический BCP (бит).<br /><br /> **131** = динамический собственный BCP.<br /><br /> **132** = динамический символ BCP.<br /><br /> **208** = динамической системная таблица собственный BCP 9.0.<br /><br /> **209** = динамический символ системной таблицы BCP 9.0.<br /><br /> **210** = динамической системная таблица собственный BCP 9.0 (только глобальные).<br /><br /> **211** = динамический символ системной таблицы BCP 9.0 (только глобальные).<br /><br /> **212** = динамической системная таблица собственный BCP 9.0 (облегченные).<br /><br /> **213** = динамический символ системной таблицы BCP 9.0 (облегченные).<br /><br /> **300** = действия языка определения данных (DDL).<br /><br /> **1024** = пошаговый контроль моментального снимка.<br /><br /> **1049** = пошаговых моментальных снимков.<br /><br /> **1074** = добавочный моментальный снимок начало заголовка.<br /><br /> **1075** = заголовок конца добавочных моментальных снимков.<br /><br /> **1076** = анонс моментального снимка.<br /><br /> **1077** = пошаговый FTP-адрес.<br /><br /> **1078** = пошаговый порт FTP.<br /><br /> **1079** = пошаговый подкаталог FTP.<br /><br /> **1080** = сжатый пошаговый моментальный снимок.<br /><br /> **1081** = добавочное ИМЕНИ входа.<br /><br /> **1082** = пошаговый пароль FTP.|  
|**schematext**|**nvarchar(2000)**|Имя файла скрипта или команды, которая включает имя файла|  
|**schemastatus**|**tinyint**|Показывает, есть ли незафиксированные изменения схемы для этой статьи. Может принимать следующие значения:<br /><br /> **0** = неактивно.<br /><br /> **1** = активно.<br /><br /> При изменении схемы ожидает выполнения, это значение присваивается **1**.|  
|**schemasubtype**|**int**|Подтип изменения схемы:<br /><br /> **1** = ADDCOLUMN<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = ADDPRIMARYKEY<br /><br /> **5** = ADDUNIQUE<br /><br /> **6** = ADDREFERENCE<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = ADDCHECK<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>См. также  
 [Таблицы репликации &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Представления репликации (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
