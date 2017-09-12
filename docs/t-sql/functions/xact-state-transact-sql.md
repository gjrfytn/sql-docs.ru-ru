---
title: "Функция XACT_STATE (Transact-SQL) | Документы Microsoft"
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
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d5760cf8b2da0abea5505245681ae5164cbc9aca
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="xactstate-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Является скалярной функцией, которая сообщает о состоянии пользовательской транзакции текущего выполняемого запроса. Функция XACT_STATE указывает, имеет ли запрос активную пользовательскую транзакцию и может ли она быть зафиксирована.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
XACT_STATE()  
```  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 **smallint**  
  
## <a name="remarks"></a>Замечания  
 XACT_STATE возвращает следующие значения.  
  
|Возвращаемое значение|Значение|  
|------------------|-------------|  
|1|Текущий запрос содержит активную пользовательскую транзакцию. Запрос может выполнять любые действия, включая запись данных и фиксирование транзакции.|  
|0|У текущего запроса нет активной пользовательской транзакции.|  
|-1|В текущем запросе есть активная транзакция, однако произошла ошибка, из-за которой транзакция классифицируется как нефиксируемая. Запросу не удается зафиксировать транзакцию или выполнить откат до точки сохранения; можно только запросить полный откат транзакции. Запрос не может выполнить никакие операции записи, пока не будет проведен откат транзакции. До отката транзакции запрос может выполнять только операции считывания. После отката транзакции запросу будут доступны как операции считывания, так и операции записи, а также запуск новых транзакций.<br /><br /> После завершения работы пакета компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] автоматически выполнит откат любых активных нефиксируемых транзакций. Если при переходе транзакции в нефиксируемое состояние не было отправлено сообщение об ошибке, после завершения выполнения пакета сообщение об ошибке будет отправлено клиентскому приложению. Сообщение показывает, что обнаружены нефиксируемые транзакции и выполнен откат.|  
  
 Оба XACT_STATE и @@TRANCOUNT функции могут использоваться для определения, является ли текущий запрос содержит активную пользовательскую транзакцию. @@TRANCOUNT не может использоваться для определения, является ли этот транзакция была классифицирована как нефиксированная транзакция. Функция XACT_STATE не может использоваться для определения наличия вложенных транзакций.  
  
## <a name="examples"></a>Примеры  
 В следующем примере выбор между фиксацией и откатом транзакции делается с помощью функции `XACT_STATE` в блоке `CATCH` конструкции `TRY…CATCH`. Поскольку функция `SET XACT_ABORT` принимает значение `ON`, транзакция становится нефиксируемой из-за нарушения ограничения.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  