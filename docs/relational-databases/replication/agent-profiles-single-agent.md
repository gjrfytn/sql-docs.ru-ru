---
title: "Профили агента (один агент) | Документация Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.profiles.perfprofileagentname.f1
helpviewer_keywords:
- Agent Profile dialog box
ms.assetid: 22713555-c496-4ce1-8ec7-4ae75cfadca8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 16dd8b8f48927c74afc929f62e13339c23df9b05
ms.lasthandoff: 04/11/2017

---
# <a name="agent-profiles-single-agent"></a>Профили агента (один агент)
  Диалоговое окно **Профили агентов** служит для управления профилями агента. Профили агентов предоставляют удобный способ управления параметрами среды выполнения для каждого агента. Каждый агент имеет профиль по умолчанию, а некоторые агенты имеют и дополнительные предопределенные профили. Например, агент слияния имеет профиль «медленной связи», предназначенный для соединений с низкой пропускной способностью. Предопределенных профилей достаточно для создания большинства приложений, однако существует возможность создания пользовательских профилей, позволяющих настроить поведение агента.  
  
## <a name="options"></a>Параметры  
 **По умолчанию для нового**  
 Выберите профиль, который будет использован при создании заданий для агента заданного типа. Например, при создании подписок для публикации слиянием задание агента слияния для каждой подписки будет использовать выбранный профиль. Если нужно изменить профиль существующих заданий, выберите профиль и нажмите **Изменить существующие агенты**.  
  
 **Название**  
 Имя профиля.  
  
 **Тип**  
 Тип профиля: **Пользовательский** (определяемый пользователем) или **Системный** (предустановленный).  
  
 **Свойства (...)**  
 Нажмите для просмотра значений каждого параметра в профиле агента.  
  
 **Создать**  
 Нажмите для создания нового профиля.  
  
 **Delete**  
 Выберите пользовательский профиль и нажмите кнопку **Удалить** , чтобы удалить его. Предопределенные профили удалить нельзя.  
  
 **Изменить существующие агенты**  
 Выберите профиль и нажмите **Изменить существующие агенты** , чтобы указать, что все существующие задания для агента данного типа должны использовать выбранный профиль. Например, если создано несколько подписок на публикацию слиянием и нужно изменить профиль, чтобы указать, что задание агента слияния для каждой из этих подписок должно использовать **Профиль агента медленного канала связи**, то выберите этот профиль и нажмите **Изменить существующие агенты**.  
  
## <a name="see-also"></a>См. также:  
 [Работа с профилями агента репликации](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Обзор агентов репликации](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Профили агента репликации](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  