---
title: "Зеркальное отображение и моментальные снимки баз данных (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "зеркальное отображение базы данных [SQL Server], взаимодействие"
  - "моментальные снимки [моментальные снимки базы данных SQL Server], зеркальное отображение базы данных"
  - "моментальные снимки базы данных [SQL Server], зеркальное отображение базы данных"
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 40
---
# Зеркальное отображение и моментальные снимки баз данных (SQL Server)
  Преимущество зеркальной базы данных проявляется в возможности использовать ее для разгрузки при формировании отчетов. Чтобы использовать зеркальную базу данных для выполнения отчетов, можно создавать моментальные снимки базы данных и направлять запросы клиентских соединений к самому позднему снимку. Моментальный снимок базы данных представляет собой статичный, доступный только для чтения, согласованный по транзакциям моментальный снимок состояния базы данных-источника на момент создания снимка. Для создания моментального снимка в зеркальной базе данных, эта база данных должна быть в синхронизированном состоянии зеркального отображения.  
  
 В отличие от самой зеркальной базы данных, моментальный снимок базы данных доступен клиентам. Пока зеркальный сервер соединен с основным сервером, можно направлять запрашивающих отчеты клиентов на подключение к моментальному снимку. Имейте в виду, что так как моментальный снимок базы данных является статичным, новые данные недоступны. Чтобы относительно новые данные были доступными для пользователей, необходимо периодически создавать новый моментальный снимок базы данных, а приложения должны устанавливать входящие клиентские соединения с наиболее поздним снимком.  
  
 Новый моментальный снимок базы данных почти пустой, но по мере того, как новые страницы базы данных впервые обновляются, снимок растет. Так как каждый моментальный снимок базы данных увеличивается, каждый снимок потребляет столько же ресурсов, как и обычная база данных. В зависимости от конфигураций зеркального и основного сервера, избыточное число моментальных снимков базы данных в зеркальной базе данных может уменьшить производительность основной базы данных. Поэтому, рекомендуется хранить лишь несколько относительно новых моментальных снимков зеркальной базы данных. Обычно после создания замещающего моментального снимка следует перенаправить входящие запросы на новый моментальный снимок, а после завершения текущих запросов удалить предыдущий снимок.  
  
> [!NOTE]  
>  Дополнительные сведения о моментальных снимках базы данных см. в разделе [Моментальные снимки базы данных (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
 Если происходит переключение ролей, то база данных и ее моментальные снимки перезапускаются, при этом пользователи временно отключаются. Впоследствии моментальные снимки базы данных остаются на экземпляре сервера, где они были созданы, который стал новой основной базой данных. Пользователям эти снимки будут доступны и после отработки отказа. Однако при этом появляется дополнительная нагрузка на новый основной сервер. Если в среде важна производительность, рекомендуется создавать моментальный снимок новой зеркальной базы данных, когда она становится доступной, и перенаправлять клиентов на новый снимок, а все моментальные снимки бывшей зеркальной базы данных удалять.  
  
> [!NOTE]  
>  В качестве специального решения для отчетов, обладающих достаточной масштабируемостью, можно рассмотреть репликацию. Дополнительные сведения см. в статье [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).  
  
## Пример  
 В данном примере создаются моментальные снимки зеркальной базы данных.  
  
 Предполагается, что в сеансе зеркального отображения используется база данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. В данном примере создаются три моментальных снимка на зеркальной копии базы данных `AdventureWorks` , которая находится на диске `F` . Моментальные снимки называются `AdventureWorks_0600`, `AdventureWorks_1200`и `AdventureWorks_1800` , имена означают приблизительное время создания снимков.  
  
1.  Создается первый моментальный снимок базы данных на зеркальной копии [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]:  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  Создается второй моментальный снимок базы данных на зеркальной копии [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Пользователи, которые все еще работают со снимком `AdventureWorks_0600` , продолжают его использовать.  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     На этом этапе новые клиентские соединения можно программно направлять на последний моментальный снимок.  
  
3.  Создается третий моментальный снимок на зеркальной копии [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Пользователи, которые все еще работают со снимками `AdventureWorks_0600` и `AdventureWorks_1200` , могут продолжать их использовать.  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     На этом этапе новые клиентские соединения можно программно направлять на последний моментальный снимок.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Создание моментального снимка базы данных (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Просмотр моментального снимка базы данных (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Удаление моментального снимка базы данных (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [&#91;В начало&#93;](#Top)  
  
## См. также:  
 [Моментальные снимки базы данных (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Подключение клиентов к сеансу зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  