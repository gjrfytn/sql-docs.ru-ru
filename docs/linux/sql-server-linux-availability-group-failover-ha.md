---
title: "Работы группы доступности SQL Server для Linux | Документы Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 07a50a59c320d7abb58c725c717393f8751b337d
ms.contentlocale: ru-ru
ms.lasthandoff: 08/28/2017

---
# <a name="operate-ha-availability-group-for-sql-server-on-linux"></a>Работы группы доступности высокого уровня ДОСТУПНОСТИ для SQL Server в Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>Отработку отказа группы доступности

Используйте средства управления кластером для отработки отказа группы доступности, управляемых диспетчером внешних кластера. Например, если решение использует Pacemaker для управления кластером Linux, используйте `pcs` для выполнения ручной переход на другой ресурс RHEL или Ubuntu. На SLES используйте `crm`. 

> [!IMPORTANT]
> В обычных условиях при сбое с помощью Transact-SQL или SQL Server средства управления, такие как среда SSMS или PowerShell. Когда `CLUSTER_TYPE = EXTERNAL`, единственное допустимое значение для `FAILOVER_MODE` — `EXTERNAL`. Эти параметры все действия ручной или автоматический переход на другой ресурс, выполняются диспетчером внешних кластеров. 

### <a name="manual-failover-examples"></a>Примеры отработка отказа вручную

Отработка отказа группы доступности с помощью средств управления внешних кластера вручную. В обычных условиях не инициировать переход на другой ресурс с помощью Transact-SQL. Если средства внешнего управления не отвечает на запрос, вы можете принудительно выполнить отработку отказа группы доступности. Инструкции по принудительному отработка отказа вручную. в разделе [вручную переместить при средств кластера не отвечать на запросы](#forceManual).

Выполните вручную отработки отказа в два этапа. 

1. Переместите ресурс группы доступности из кластера узел, владеющий ресурсы на новый узел.

   Диспетчер кластеров перемещает ресурс группы доступности и добавляет ограничение расположения. Это ограничение настраивает ресурсов для запуска на новый узел. Для перемещения либо вручную или автоматически при сбое в будущем, необходимо удалить это ограничение.

2. Удалите ограничение расположения.

#### <a name="1-manually-fail-over"></a>1. Отработка отказа вручную

Чтобы вручную перевести ресурс группы доступности с именем *ag_cluster* на узел кластера с именем *nodeName2*, выполните соответствующую команду для распространения:

- **Пример RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Пример SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>После вручную переключить ресурс, необходимо удалить ограничение расположения, которое автоматически добавляется во время перемещения.

#### <a name="2-remove-the-location-constraint"></a>2. Удаление ограничения расположения

Во время перемещения вручную `pcs` команда `move` или `crm` команда `migrate` добавляет ограничение расположения для ресурса на новый целевой узел. Чтобы увидеть новое ограничение, после перемещения ресурса вручную выполните следующую команду:

- **Пример RHEL/Ubuntu**

   ```bash
   sudo pcs constraint --full
   ```

- **Пример SLES**

   ```bash
   crm config show
   ```

Расположение нужно удалить, чтобы гарантировать последующие успешные перемещения, включая автоматический переход на новый ресурс. 

Чтобы удалить ограничение, выполните приведенную ниже команду, 

- **Пример RHEL/Ubuntu**

   В этом примере `ag_cluster-master` имя ресурса, который был перемещен. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **Пример SLES**

   В этом примере `ag_cluster` имя ресурса, который был перемещен. 

   ```bash
   crm resource clear ag_cluster
   ```

Вы также можете выполнить приведенную ниже команду для удаления ограничения расположения,  

- **Пример RHEL/Ubuntu**

   где `cli-prefer-ag_cluster-master` — это код ограничения, которое необходимо удалить. `sudo pcs constraint --full` возвращает этот код. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **Пример SLES**

   В следующей команде `cli-prefer-ms-ag_cluster` идентификатор ограничения. `crm config show` возвращает этот код. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>При автоматическом переходе на другой ресурс ограничение расположения не добавляется, поэтому очистка не требуется. 

Дополнительные сведения см. в следующих разделах:
- [Chapter 7. Managing Cluster Resources](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html) (Глава 7. Управление ресурсами кластера)
- [Pacemaker - вручную переместить ресурсы](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [руководство по администрированию SLES - ресурсы](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 

### <a name="forceManual"></a>Вручную переместить при средств кластера не отвечать на запросы 

В крайних случаях, если пользователь не может использовать средства управления кластером для взаимодействия с кластером (т. е. кластера не отвечает, средства управления кластером неисправный себя), пользователь может быть переход на другой ресурс вручную - обход Диспетчер внешних кластера. Это не рекомендуется для выполнения обычных операций и следует использовать в случаях, кластер не удается выполнить действие перехода на другой ресурс, с помощью средства управления кластером.

Если не удается переход группы доступности с помощью средства управления кластером, выполните следующие действия для отработки отказа с помощью средств SQL Server.

1. Убедитесь, что ресурс группы доступности не находится под управлением кластера больше. 

      - Попытка установить ресурс неуправляемом режиме. Это сигнализирует ресурсов агента, чтобы прекратить отслеживание ресурсов и управления. Например: 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - При неудачной попытке задания режима ресурсов в неуправляемых режим, удалите данный ресурс. Например:

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >При удалении ресурса также удаляет все связанные ограничения. 

1. Вручную задать переменной контекста сеанса `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Переход группы доступности с помощью Transact-SQL. В примере ниже замены `<**MyAg**>` с именем группы доступности. Подключитесь к экземпляру SQL Server, на котором размещена целевая вторичная реплика и выполните следующую команду:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. Перезапустите мониторинг ресурсов кластера и управления. Выполните следующую команду:

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>Уровень мониторинга и переход на другой ресурс для триггера базы данных

Для `CLUSTER_TYPE=EXTERNAL`, семантика триггер отработки отказа различаются по сравнению с WSFC. Если группы доступности на экземпляре SQL Server в WSFC, переход из `ONLINE` состояние для базы данных вызывает работоспособность группы доступности для сообщения ошибки. Это даст сигнал диспетчера кластеров для запуска действие отработки отказа. В Linux экземпляр SQL Server не удается связаться с кластером. Мониторинг работоспособности базы данных выполняется «за пределами in». Если пользователь выбрал в для мониторинга отработки отказа базы данных и обеспечения отказоустойчивости (путем установки параметра `DB_FAILOVER=ON` при создании группы доступности), кластер будет проверять, если состояние базы данных является `ONLINE` каждый раз при выполнении действие мониторинга. Кластер запрашивает состояние в `sys.databases`. Для любого состояния, отличный от `ONLINE`, инициирует отработку отказа автоматически (если выполнены условия для автоматического перехода на другой ресурс). Фактическое время отработки отказа зависит от частоты действие мониторинга, а также состояние базы данных обновляются в представлении каталога sys.databases.

## <a name="upgrade-availability-group"></a>Обновление группы доступности

Перед обновлением группы доступности, просмотрите рекомендации по [обновление экземпляров реплики группы доступности](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Следующие разделы описывают выполнить последовательное обновление с экземплярами SQL Server в Linux с группами доступности. 

### <a name="upgrade-steps-on-linux"></a>Этапы обновления в Linux

Когда реплики доступности группы экземпляров SQL Server в Linux, тип кластера группы доступности — `EXTERNAL` или `NONE`. Группа доступности, которая находится под управлением диспетчера кластеров, помимо отказоустойчивого кластера (WSFC) является `EXTERNAL`. Pacemaker с Corosync примером может служить Диспетчер внешних кластера. Группа доступности с диспетчер кластера не имеет типа кластера `NONE` относятся приведенные ниже действия по обновлению для групп доступности кластера типа `EXTERNAL` или `NONE`.

1. Прежде чем начать, создайте резервную копию каждой базы данных.
2. Обновление экземпляров SQL Server, размещения вторичных реплик.

    а. Сначала обновите асинхронные вторичные реплики.

    б. Обновите синхронные вторичные реплики.

   >[!NOTE]
   >Если группа доступности имеет только асинхронных реплик — Чтобы избежать потери данных измените одной реплики на синхронный и подождите, пока он синхронизирован. Затем обновите этой реплики.
   
   б.1. Остановить ресурса на узел, содержащий вторичную реплику, предназначенных для обновления
   
   Перед выполнением команды обновления, остановите ресурс кластера не будет отслеживать ее и выполнять отработку отказа без необходимости. В следующем примере добавляется ограничение расположения на узле, который приведет к ресурса следует остановить. Обновление `ag_cluster-master` с именем ресурса и `nodeName1` с узла, на котором размещена реплика, предназначенных для обновления.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   б.2. Обновление SQL Server на вторичной реплике

   В следующем примере выполняется обновление `mssql-server` и `mssql-server-ha` пакетов.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   б.3. Удаление ограничения расположения

   Перед выполнением команды обновления, остановите ресурс кластера не будет отслеживать ее и выполнять отработку отказа без необходимости. В следующем примере добавляется ограничение расположения на узле, который приведет к ресурса следует остановить. Обновление `ag_cluster-master` с именем ресурса и `nodeName1` с узла, на котором размещена реплика, предназначенных для обновления.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Как рекомендуется обеспечить работу ресурс (с помощью `pcs status` команда) и Вторичная реплика подключена и синхронизировать состояние после обновления.

1. После обновления всех вторичных реплик вручную при сбое в один из синхронных вторичных реплик.

   Для группы доступности с `EXTERNAL` кластера типа, используйте средства управления кластером сбой over, группы доступности с `NONE` тип кластер должен использовать Transact-SQL для отработки отказа. 
   В следующем примере выполняется ресурс группы доступности с помощью средства управления кластером. Замените `<targetReplicaName>` с именем синхронной вторичной реплики, который станет основным:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >Следующие шаги применяются только к группам доступности, у которых нет диспетчера кластеров.  
   Если тип кластера группы доступности `NONE`вручную при сбое. Последовательно выполните следующие шаги.

      а. Следующая команда задает первичной реплики во вторичные. Замените `AG1` с именем группы доступности. Выполните команду Transact-SQL на экземпляре SQL Server, на котором размещена первичная реплика.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      б. Следующая команда задает синхронная вторичная реплика к первичной. Выполните следующую команду Transact-SQL на целевом экземпляре SQL Server - экземпляр, на котором размещена вторичная реплика.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. После отработки отказа обновите SQL Server в старой первичной реплике, повторив процедуру, описанную в шагах б.1 б.3 выше.

   В следующем примере выполняется обновление `mssql-server` и `mssql-server-ha` пакетов.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. Для группы доступности с внешних кластера диспетчер - где типом кластера — ВНЕШНИХ, очистка ограничение расположение, которое было вызвано отработка отказа вручную. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Возобновление перемещения данных для только что обновленный вторичной реплики - бывшая первичная реплика. Это требуется в том случае, если экземпляр выше версии SQL Server передает блоков журнала ниже версии экземпляру в группе доступности. Выполните следующую команду на новую вторичную реплику (предыдущей первичной реплики).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

После обновления всех серверов, можно выполнить восстановление после сбоя - переключение обратно на исходную первичную - при необходимости. 

## <a name="drop-an-availability-group"></a>Удалить группу доступности

Чтобы удалить группу доступности, запустите [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Если тип кластера `EXTERNAL` или `NONE` выполните команду на каждом экземпляре SQL Server, на котором размещена реплика. Например, чтобы удалить группу доступности с именем `group_name` выполните следующую команду:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Следующие шаги

[Настройка Red Hat Enterprise Linux кластера для ресурсов кластера группы доступности SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Настройка SUSE Linux Enterprise Server кластера для ресурсов кластера группы доступности SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Настройка кластера Ubuntu для ресурсов кластера группы доступности SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
