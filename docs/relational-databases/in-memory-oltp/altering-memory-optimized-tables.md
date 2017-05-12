---
title: "Изменение оптимизированных для памяти таблиц | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4a8b3f4dabec4d46813c570e1a04fd469075a66
ms.lasthandoff: 04/11/2017

---
# <a name="altering-memory-optimized-tables"></a>Изменение таблиц с оптимизацией для памяти
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Изменения схемы и индекса в таблицах, оптимизированных для памяти, можно выполнить с помощью инструкции ALTER TABLE. Приложение базы данных может продолжать работу, и любая операция, которая обращается к таблице, будет блокироваться до завершения процесса изменения.  
  
## <a name="alter-table"></a>ALTER TABLE  
 
Синтаксис инструкции ALTER TABLE используется для внесения изменений в схему таблицы, а также для добавления, удаления и перестроения индексов. Индексы являются частью определения таблицы:  
  
-   Синтаксис инструкции ALTER TABLE… ADD/DROP/ALTER INDEX поддерживается только для таблиц, оптимизированных для памяти.  
  
-   Без использования инструкции ALTER TABLE инструкции CREATE INDEX, DROP INDEX и ALTER INDEX *не* поддерживаются для индексов в таблицах, оптимизированных для памяти.  
  
 Ниже приведен синтаксис для предложений ADD, DROP и ALTER INDEX в инструкции ALTER TABLE.  
  
```
| ADD   
     {   
        <column_definition>  
      | <table_constraint>  
      | <table_index>    
     } [ ,...n ]  
  
| DROP   
     {  
         [ CONSTRAINT ]   
         {   
              constraint_name   
         } [ ,...n ]  
         | COLUMN   
         {  
              column_name   
         } [ ,...n ]  
         | INDEX   
         {  
              index_name   
         } [ ,...n ]  
     } [ ,...n ]  
  
| ALTER INDEX index_name  
     {   
         REBUILD WITH ( <rebuild_index_option> )     
     }  
}  
```  
  
 Поддерживаются следующие типы изменений.  
  
-   Изменение числа контейнеров  
  
-   Добавление и удаление индекса  
  
-   Изменение, добавление и удаление столбца  
  
-   Добавление и удаление ограничения  
  
 Дополнительные сведения о функции ALTER TABLE и полный синтаксис см. в статье [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="schema-bound-dependency"></a>Зависимость, привязанная к схеме  
 Скомпилированные в собственном коде хранимые процедуры должны быть привязаны к схеме, а значит иметь привязанную к схеме зависимость от оптимизированных в памяти таблиц, к которым они обращаются, и столбцов, на которые они ссылаются. Привязанная к схеме зависимость — это связь между двумя сущностями, которая не допускает удаления или несовместимого изменения упоминаемой сущности, пока существует ссылающаяся сущность.  
  
 Например, если скомпилированная в собственном коде и привязанная к схеме хранимая процедура ссылается на столбец *c1* из таблицы *mytable*, столбец *c1* удалить нельзя. Точно так же при наличии процедуры с инструкцией INSERT без списка столбцов (например, `INSERT INTO dbo.mytable VALUES (...)`), ни один из столбцов в таблице удалить нельзя.  
  
## <a name="examples"></a>Примеры  
 В следующем примере изменяется число контейнеров существующего хэш-индекса. Это приводит к перестроению хэш-индекса с помощью нового числа контейнеров, при этом другие свойства хэш-индекса остаются неизменными.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem   
       ALTER INDEX imPK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID  
              REBUILD WITH (BUCKET_COUNT=67108864);  
GO
```
  
 В следующем примере добавляется столбец с ограничением NOT NULL и с определением DEFAULT и использует аргумент WITH VALUES для предоставления значений каждой существующей строке таблицы. Если аргумент WITH VALUES не используется, то каждая строка в новом столбце имеет значение NULL.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD Comment NVARCHAR(100) NOT NULL DEFAULT N'' WITH VALUES;  
GO
```  
  
 В следующем примере к существующему столбцу добавляется ограничение первичного ключа.  
  
```tsql
CREATE TABLE dbo.UserSession (   
   SessionId int not null,   
   UserId int not null,   
   CreatedDate datetime2 not null,   
   ShoppingCartId int,   
   index ix_UserId nonclustered hash (UserId) with (bucket_count=400000)   
)   
WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY) ;  
GO  
  
ALTER TABLE dbo.UserSession  
       ADD CONSTRAINT PK_UserSession PRIMARY KEY NONCLUSTERED (SessionId);  
GO
```  
  
 В следующем примере удаляется индекс.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       DROP INDEX ix_ModifiedDate;  
GO
```  
  
 В следующем примере добавляется индекс.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD INDEX ix_ModifiedDate (ModifiedDate);  
GO  
```  
  
 В следующем примере добавляется несколько столбцов с индексом и ограничениями.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD    CustomerID int NOT NULL DEFAULT -1 WITH VALUES,  
              ShipMethodID int NOT NULL DEFAULT -1 WITH VALUES,  
              INDEX ix_Customer (CustomerID);  
GO  
```


<a name="logging-of-alter-table-on-memory-optimized-tables-124"></a>

## <a name="logging-of-alter-table-on-memory-optimized-tables"></a>Ведение журнала ALTER TABLE для таблиц, оптимизированных для памяти


В таблицах, оптимизированных для памяти, большинство сценариев ALTER TABLE теперь выполняются параллельно и позволяют оптимизировать операции записи в журнал транзакций. Оптимизация заключается в том, что только изменения метаданных записываются в журнал транзакций. Тем не менее следующие операции ALTER TABLE запускаются в одном потоке и не оптимизированы для журнала.

Для операций, выполняемых в одном потоке, требуется записать в журнал все содержимое измененной таблицы. Далее приведен список операций, выполняемых в одном потоке:

- изменение и добавление столбца для использования типа данных больших объектов (LOB): nvarchar(max), varbinary(max) или varchar(max);

- добавление или удаление индекса columnstore;

- практически все, что влияет на [столбец вне строки](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md);

    - перемещение столбца в строке за пределы строки;

    - перемещение столбца вне строки в строку;

    - создание нового столбца вне строки.

    - *Исключение:* удлинение столбца, который уже находится вне строки, фиксируется в журнале оптимизированным образом.


## <a name="see-also"></a>См. также:  

[Таблицы, оптимизированные для памяти](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  

