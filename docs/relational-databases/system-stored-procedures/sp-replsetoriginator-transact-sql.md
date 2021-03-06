---
title: sp_replsetoriginator (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f72558a573e0cee0ab7fb2ab9b762246964a884
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526186"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Используется для запуска механизма распознавания замыкания на себя и управления в двунаправленной репликации транзакций. Эта хранимая процедура выполняется на издателе в базе данных публикации.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @server_name = ] 'server_name'` — Это имя сервера, на котором применяется транзакция. *originating_server* — **sysname**, не имеет значения по умолчанию.  
  
`[ @database_name = ] 'database_name'` — Имя базы данных, в котором применяется транзакция. *originating_db* — **sysname**, не имеет значения по умолчанию.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 **sp_replsetoriginator** выполняется агентом распространителя для записи источника транзакций, применяемых репликацией. Данные сведения используются для запуска механизма распознавания замыкания на себя для двунаправленных транзакционных подписок, которые имеют набор свойств обратной связи.  
  
## <a name="permissions"></a>Разрешения  
 Только члены **sysadmin** предопределенной роли сервера на издателе, члены **db_owner** предопределенной роли базы данных в базе данных публикации или пользователи в списке доступа к публикации (PAL) могут выполнять процедуру **sp_replsetoriginator**.  
  
## <a name="see-also"></a>См. также  
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
