---
title: Просмотр свойств ограничений ребер | Документация Майкрософт
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server], attributes
- displaying edge constraint attributes
- viewing edge constraint attributes
ms.assetid: b0e57cb7-9b26-4b96-b76a-1f59f5f498c5
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 129d61ddf42a159dbeba74a168d10dac72094b3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790682"
---
# <a name="view-edge-constraint-properties"></a>Просмотр свойств ограничений ребер
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Просмотреть свойства ограничения ребер [!INCLUDE[noversion](../../includes/ssnoversion-md.md)] можно с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [безопасность](#Security)  
  
-   **Просмотр атрибутов внешнего ключа таблицы с помощью различных средств.**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-view-the-foreign-key-attributes-of-a-relationship-in-a-specific-table"></a>Просмотр атрибутов внешнего ключа связей в таблице  
  
1.  В **обозревателе объектов** подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В приведенном далее примере возвращаются сведения обо всех ограничениях ребер и их свойствах для таблицы ребер `bought` из базы данных tempdb.  
    
    ```sql
    USE TEMPDB
    GO
    -- CREATE node and edge tables
    CREATE TABLE Customer
      (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Supplier
      (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Product 
      (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
      ) 
    AS NODE
    GO
    -- CREATE edge table with edge constraints.
    CREATE TABLE bought
      (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
      )
    AS EDGE
    GO
    
    -- Query sys.edge_constraints and sys.edge_constraint_clauses to view 
    -- edge constraint properties. 
    SELECT
        EC.name AS edge_constraint_name
        , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
        , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
        , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
        , is_disabled
        , is_not_trusted
    FROM sys.edge_constraints EC
    INNER JOIN sys.edge_constraint_clauses ECC
        ON EC.object_id = ECC.object_id
    WHERE EC.parent_object_id = object_id('bought')
    ```  
  
 Дополнительные сведения см. в следующих статьях: [sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) и [sys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
