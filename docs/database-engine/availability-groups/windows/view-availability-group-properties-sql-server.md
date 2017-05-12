---
title: "Просмотр свойств группы доступности (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Группы доступности [SQL Server]"
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
caps.latest.revision: 13
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 13
---
# Просмотр свойств группы доступности (SQL Server)
  В этом разделе описывается просмотр свойств группы доступности для группы доступности AlwaysOn с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)] в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Для просмотра свойств группы доступности используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 **Просмотр и изменение свойств группы доступности**  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена первичная реплика, и разверните дерево сервера.  
  
2.  Разверните узел **Высокий уровень доступности AlwaysOn** и узел **Группы доступности**.  
  
3.  Щелкните правой кнопкой мыши группу доступности, свойства которой нужно просмотреть, и выберите команду **Свойства**.  
  
4.  В диалоговом окне **Свойства группы доступности** просмотреть и в некоторых случаях изменить свойства выбранной группы доступности можно на страницах **Общие** и **Настройки резервного копирования** . Дополнительные сведения см. в статье [Свойства группы доступности: создание групп доступности (страница "Общие")](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-general-page.md) и [Свойства группы доступности: создание группы доступности (страница "Настройки резервного копирования")](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-backup-preferences-page.md).  
  
     На странице **Разрешения** можно просмотреть текущие имена входа, роли и явные разрешения, связанные с группой доступности. Дополнительные сведения см. в статье [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Просмотр свойств и состояния группы доступности**  
  
 Чтобы запросить свойства и состояния групп доступности, для которых на экземпляре сервера размещена реплика доступности, используйте следующие представления.  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 Возвращает строку для каждой группы доступности, для которых в локальном экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] размещена реплика доступности. Каждая строка содержит кэшированную копию метаданных группы доступности.  
  
 **Имена столбцов:** group_id, имя, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 Возвращает строку для каждой группы доступности в кластере WSFC. Каждая строка содержит метаданные группы доступности из отказоустойчивой кластеризации Windows Server (WSFC).  
  
 **Имена столбцов:** group_id, имя, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 Возвращает по строке для каждой из групп доступности, у которых имеется реплика доступности на локальном экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Каждая строка отображает состояния работоспособности определенной группы доступности.  
  
 **Имена столбцов:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Просмотр сведений о группах доступности**  
  
-   [Просмотр свойств реплики доступности (SQL Server)](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Просмотр свойств прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md)  
  
-   [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Отслеживание групп доступности (Transact-SQL)](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
 **Настройка существующей группы доступности**  
  
-   [Добавление вторичной реплики к группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Удаление вторичной реплики из группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Добавление базы данных в группу доступности (SQL Server)](../../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md)  
  
-   [Удаление базы данных-получателя из группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Создание или настройка прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Удаление прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Удаление базы данных-источника из группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Удаление группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
 **Переход на другой ресурс группы доступности вручную**  
  
-   [Выполнение запланированного перехода на другой ресурс вручную для группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Выполнение принудительного перехода на другой ресурс вручную для группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
## См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Отслеживание групп доступности (Transact-SQL)](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md)  
  
  