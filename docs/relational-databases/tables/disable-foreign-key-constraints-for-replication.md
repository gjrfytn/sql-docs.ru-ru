---
title: "Отключение ограничений внешнего ключа для репликации | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e16bd86b4a8b0d333b9b88752d702d783ba180cc
ms.lasthandoff: 04/11/2017

---
# <a name="disable-foreign-key-constraints-for-replication"></a>Отключение ограничений внешнего ключа для репликации
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Отключить ограничения внешнего ключа для репликации можно в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Это может потребоваться при публикации данных из предыдущей версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Если таблица публикуется для репликации, ограничения внешнего ключа для нее автоматически отключаются в случае операций, выполняемых агентами репликации. Когда агент репликации на подписчике выполняет вставку, обновление или удаление, ограничение не проверяется. Если эту же операцию выполняет пользователь, ограничение проверяется. Ограничение отключено для агента репликации по той причине, что оно уже проверено на издателе при выполнении исходной операции вставки, обновления или удаления данных.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Отключение ограничения внешнего ключа для репликации с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Требуется разрешение ALTER на таблицу.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Отключение ограничения внешнего ключа для репликации  
  
1.  В **обозревателе объектов**раскройте таблицу, содержащую ограничение внешнего ключа, которое необходимо изменить, а затем разверните папку **Ключи** .  
  
2.  Правой кнопкой мыши щелкните ограничение, а затем выберите команду **Изменить**.  
  
3.  В диалоговом окне **Связи по внешнему ключу** выберите значение **Нет** для параметра **Включить использование для репликации**.  
  
4.  Щелкните **Закрыть**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Отключение ограничения внешнего ключа для репликации  
  
1.  Для выполнения этой задачи в [!INCLUDE[tsql](../../includes/tsql-md.md)]удалите ограничение внешнего ключа. Затем добавьте новое ограничение внешнего ключа и укажите параметр NOT FOR REPLICATION.  
  
 Дополнительные сведения см. в разделе [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  