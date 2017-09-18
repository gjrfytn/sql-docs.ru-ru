---
title: "OPENQUERY (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 105284d935888db46be8081bfca0c181eb920636
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Выполняет указанный передаваемый запрос к указанному связанному серверу. Этот сервер является источником данных OLE DB. Из предложения FROM запроса можно ссылаться на функцию OPENQUERY как на имя таблицы. На функцию OPENQUERY можно также ссылаться как на целевую таблицу инструкции INSERT, UPDATE или DELETE. Это зависит от возможностей поставщика OLE DB. Запрос может возвратить несколько результирующих наборов, но функция OPENQUERY возвращает только первый.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>Аргументы  
 *связанный_сервер*  
 Идентификатор, представляющий имя связанного сервера.  
  
 **"** *запроса* **"**  
 Строка запроса, выполненного в связанном сервере. Максимальная длина строки 8 КБ.  
  
## <a name="remarks"></a>Замечания  
 В качестве аргументов в функции OPENQUERY нельзя использовать переменные.  
  
 Функцию OPENQUERY нельзя использовать для выполнения расширенных хранимых процедур на связанном сервере. Однако расширенную хранимую процедуру можно выполнить на связанном сервере с помощью четырехкомпонентного имени. Например:  
  
```  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 Любой вызов функции OPENDATASOURCE, OPENQUERY или OPENROWSET в предложении FROM вычисляется отдельно и независимо от любого вызова этих функций, используемого как назначение при обновлении, даже если в двух таких вызовах будут заданы идентичные аргументы. В частности, условия фильтра или соединения, применяемые к результатам одного из таких вызовов, никак не влияют на результаты другого.  
  
## <a name="permissions"></a>Permissions  
 Функцию OPENQUERY может выполнить любой пользователь. Разрешения, используемые для подключения к удаленному серверу, извлекаются из настроек, определенных для связанного сервера.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. Выполнение передаваемого запроса UPDATE  
 В следующем примере используется передаваемый запрос `UPDATE` к связанному серверу, созданному в примере А.  
  
```  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>Б. Выполнение передаваемого запроса INSERT  
 В следующем примере используется передаваемый запрос `INSERT` к связанному серверу, созданному в примере А.  
  
```  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>В. Выполнение передаваемого запроса DELETE  
 В следующем примере используется передаваемый запрос `DELETE` для удаления строки, созданной в примере В.  
  
```  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
## <a name="see-also"></a>См. также:  
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [Функции наборов строк &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [ГДЕ &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  