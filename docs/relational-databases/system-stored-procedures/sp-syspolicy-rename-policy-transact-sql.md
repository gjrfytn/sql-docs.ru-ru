---
title: "процедура sp_syspolicy_rename_policy (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_TSQL
- sp_syspolicy_rename_policy
dev_langs: TSQL
helpviewer_keywords: sp_syspolicy_rename_policy
ms.assetid: ce2b07f5-23b1-4f49-8e7b-c18cf3f3d45b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd1296c5d0a7fc4d1798b88fc1bb8f34c9b09b0b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="spsyspolicyrenamepolicy-transact-sql"></a>sp_syspolicy_rename_policy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Переименовывает существующую политику в управлении на основе политик.  
  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_syspolicy_rename_policy { [ @name = ] 'name' | [ @policy_id = ] policy_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@name=** ] **"***имя***"**  
 Имя политики для переименования. *имя* — **sysname**и должен быть указан, если *policy_id* имеет значение NULL.  
  
 [  **@policy_id=** ] *policy_id*  
 Идентификатор политики для переименования. *policy_id* — **int**и должен быть указан, если *имя* имеет значение NULL.  
  
 [  **@new_name=** ] **"***новое_имя***"**  
 — Новое имя для политики. *новое_имя* — **sysname**и является обязательным. Не может быть пустой строкой и не может принимать значение NULL.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Замечания  
 Процедура sp_syspolicy_rename_policy должна выполняться в контексте системной базы данных msdb.  
  
 Необходимо указать значение либо для *имя* или *policy_id*. Они не могут одновременно иметь значения NULL. Чтобы получить эти значения, запросите системное представление msdb.dbo.syspolicy_policies.  
  
## <a name="permissions"></a>Permissions  
 Требуется членство в предопределенной роли базы данных PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Возможно повышение учетных данных: пользователи в роли PolicyAdministratorRole могут создавать триггеры сервера и планировать выполнение политик, влияющих на работу экземпляра [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Например, пользователи в роли PolicyAdministratorRole могут создать политику, которая может запретить создание большинства объектов в компоненте [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Вследствие возможного повышения прав учетных данных роль PolicyAdministratorRole должна предоставляться только пользователям, имеющим право изменять конфигурацию компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Примеры  
 В следующем примере имя политики «Test Policy 1» меняется на «Test Policy 2».  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy @name = N'Test Policy 1'  
, @new_name = N'Test Policy 2';  
  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Управление на основе политик хранимых процедур &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  