---
title: "Параметр конфигурации сервера &#171;affinity mask&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "affinity mask, параметр по умолчанию"
  - "обновление кэша процессора"
  - "кэш процессора [SQL Server]"
  - "ЦП [SQL Server], лицензирование"
  - "отложенный вызов процессов"
  - "affinity mask, параметр"
  - "соответствие процессоров [SQL Server]"
  - "SMP"
  - "DPC"
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
caps.latest.revision: 52
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 52
---
# Параметр конфигурации сервера &#171;affinity mask&#187;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Используйте вместо него инструкцию [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) .  
  
 Для одновременного выполнения множества задач [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows иногда распределяет потоки процессов между разными процессорами. Безусловно, такая организация работы эффективна с точки зрения операционной системы, но может привести к снижению производительности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при больших нагрузках системы, поскольку в кэше каждого процессора неоднократно перезагружаются данные. В этих условиях назначение процессорам определенных потоков может повысить производительность, устраняя повторную загрузку процессоров и уменьшая количество переносов потоков между процессорами (а значит, уменьшая число переключений контекста). Такая связь между потоком и процессором называется соответствием процессоров.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает соответствие процессоров с помощью двух параметров: affinity mask (также известен как **CPU affinity mask**) и affinity I/O mask. Дополнительные сведения о параметре affinity I/O mask см. в разделе [Параметр конфигурации сервера "affinity Input-Output mask"](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md). Поддержка соответствия процессоров и ввода-вывода для серверов с числом ЦП от 33 до 64 требует также использования параметров [Параметр конфигурации сервера "affinity64 mask"](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) и [Параметр конфигурации сервера "affinity64 Input-Output mask"](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)соответственно.  
  
> [!NOTE]  
>  Поддержка соответствия процессоров для серверов с числом процессоров от 33 до 64 доступна только в 64-разрядных версиях операционных систем.  
  
 Параметр affinity mask, который существовал в предыдущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], динамически управляет соответствием ЦП.  
  
 В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]параметр affinity mask можно настраивать без последующей перезагрузки экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. После установки параметра конфигурации с помощью хранимой процедуры sp_configure необходимо выполнить инструкцию RECONFIGURE или RECONFIGURE WITH OVERRIDE. Если же используется выпуск [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], то после изменения значения параметра affinity mask требуется перезагрузка.  
  
 Изменения масок сходства происходят динамически, что дает пользователям возможность запускать планировщики процессоров, связывающие процессы в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]и завершать их работу по требованию. Это может происходить при изменении условий работы сервера. Например, если к серверу добавляется новый экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , то может потребоваться внести изменения в параметр affinity mask, чтобы перераспределить нагрузку процессоров.  
  
 Изменения битовых масок соответствия требуют, чтобы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запустил новый планировщик процессора и завершил работу текущего планировщика. После этого новые пакеты могут обрабатываться новым или оставшимися планировщиками.  
  
 Чтобы запустить новый планировщик процессора, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] создает новый планировщик и добавляет его в список стандартных планировщиков. Новый планировщик используется только для обработки новых входящих пакетов. Текущие пакеты обрабатываются старым планировщиком. Рабочие потоки переходят на новый планировщик по мере освобождения или по мере создания новых рабочих потоков.  
  
 Для завершения работы планировщика необходимо, чтобы все пакеты завершили свою работу. Планировщик, чья работа завершена, помечается как находящийся в режиме «вне сети», чтобы ему не были назначены новые пакеты.  
  
 При добавлении или удалении нового планировщика постоянные системные задачи, например lockmonitor, checkpoint, поток системной задачи (обрабатывающей DTC) и обработчик сигналов, продолжают работать на планировщике, пока сервер находится в режиме «в сети». Эти постоянные системные задачи не перемещаются динамически. Для перераспределения процессорной нагрузки этих задач между планировщиками необходимо перезапустить экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] попытается завершить работу планировщика, связанного с постоянной системной задачей, задача будет продолжать выполняться даже если планировщик будет работать в режиме «вне сети» (и не будет перенесена). Этот планировщик привязан к процессорам измененной маской сходства, он не должен нагружать процессор, с которым он был приведен в соответствие до изменения. Использование дополнительных планировщиков, работающих в режиме «вне сети», не должно значительно влиять на нагрузку системы. Если это не так, то для повторной настройки этих задач нужно будет перезагрузить сервер баз данных.  
  
 Маска привязки ввода-вывода напрямую влияет на задачи привязки ввода-вывода (например, на lazywriter и logwriter). Если задачи lazywriter и logwriter не приведены в соответствие с процессорами, они следуют общим правилам постоянных задач, например lockmonitor или checkpoint.  
  
 Чтобы гарантировать, что новая маска сходства допустима, команда RECONFIGURE проверяет, чтобы нормальные соответствия процессоров и ввода-вывода были взаимно исключающими. Если это не так, то сообщение об ошибке будет отправлено в сеанс клиента и записано в журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , сигнализируя о том, что такая настройка не рекомендуется. Запуск с параметром RECONFIGURE WITH OVERRIDE позволяет соответствиям процессоров и ввода-вывода не быть взаимоисключающими.  
  
 Если указать маску сходства, которая попытается сопоставить поток несуществующему процессору, то команда RECONFIGURE отправит сообщение об ошибке в сеанс клиента и в журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Использование параметра RECONFIGURE WITH OVERRIDE в этом случае ничего не изменит, и будет создано еще одно сообщение об ошибке.  
  
 Можно также исключить работу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на процессорах, получивших специальные рабочие нагрузки от операционной системы Windows 2000 или Windows Server 2003. Если установить значение бита, представляющего процессор, в 1, этот процессор будет выбран ядром СУБД [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для назначения потоков. Если для параметра **affinity mask** задано значение 0 (по умолчанию), алгоритмы планирования Microsoft Windows 2000 или Windows Server 2003 самостоятельно определяют схожесть потоков. Если для **affinity mask** задано любое ненулевое значение, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] интерпретирует это значение схожести как битовую маску, определяющую процессоры, пригодные для выбора.  
  
 Если потокам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запрещено выполняться на определенных процессорах, ОС Microsoft Windows 2000 или Windows Server 2003 может лучше обрабатывать процессы, характерные для Windows. Например, на сервере с 8 процессорами, на котором работают два экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (экземпляры A и B), системный администратор может использовать параметр affinity mask для назначения первого набора из 4 процессоров экземпляру A и второго набора из 4 процессоров экземпляру B. Чтобы выполнить настройку больше чем для 32 процессоров, задавайте и параметр affinity mask, и параметр affinity64 mask. Ниже приведены возможные значения параметра **affinity mask** .  
  
-   Однобайтовая маска схожести ( **affinity mask** ) обеспечивает управление компьютерами, содержащими до 8 ЦП.  
  
-   Двухбайтовая маска схожести ( **affinity mask** ) обеспечивает управление компьютерами, содержащими до 16 ЦП.  
  
-   Трехбайтовая маска схожести ( **affinity mask** ) обеспечивает управление компьютерами, содержащими до 24 ЦП.  
  
-   Четырехбайтовая маска схожести ( **affinity mask** ) обеспечивает управление компьютерами, содержащими до 32 ЦП.  
  
-   Для управления большим числом процессоров для первых 32 процессоров используется четырехбайтовая маска соответствия, а для оставшихся — четырехбайтовое значение параметра affinity64 mask.  
  
 Так как задание соответствия процессоров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — специализированная операция, выполнять ее рекомендуется только при необходимости. В большинстве случаев соответствие по умолчанию, назначаемое Microsoft Windows 2000 или Windows Server 2003, гарантирует оптимальную производительность. При задании масок соответствия следует также учитывать требования к ЦП других приложений. Дополнительные сведения см. в документации по операционной системе Windows.  
  
> [!NOTE]  
>  Для просмотра и анализа нагрузки на отдельные процессоры можно использовать системный монитор Windows.  
  
 При задании параметра affinity I/O mask его необходимо использовать в сочетании с параметром конфигурации affinity mask. Не следует включать один и тот же процессор и в параметре **affinity mask** , и в параметре affinity I/O mask. Биты, соответствующие каждому ЦП, должны находиться в одном из трех состояний.  
  
-   значение 0 для обоих параметров, affinity mask и affinity I/O mask;  
  
-   значение 1 для параметра affinity mask и 0 для параметра affinity I/O mask;  
  
-   значение 0 для параметра affinity mask и 1 для параметра affinity I/O mask.  
  
> [!CAUTION]  
>  Не используйте маску привязки процессоров в операционной системе Windows и маску привязки в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]одновременно. Эти настройки предназначены для достижения одного результата, и если их значения будут несогласованными, результат может быть непредсказуем. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Соответствие процессоров лучше всего настраивать с помощью параметра хранимой процедуры sp_configure в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Пример  
 Если процессоры 1, 2 и 5 выбраны как доступные путем установки битов 1, 2 и 5 равными 1, а биты 0, 3, 4, 6 и 7 установлены равными 0, то в качестве значения параметра affinity mask должно быть указано шестнадцатеричное значение 0x26 или его десятичный эквивалент `38` . Биты нумеруются справа налево. В параметре affinity mask начинается отсчет процессоров от 0 до 31, поэтому в следующем примере счетчик `1` представляет второй процессор на сервере.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 Это значения **affinity mask** для компьютера с 8 процессорами.  
  
|Десятичное значение|Битовая маска|Количество допустимых потоков SQL Server в процессорах|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 и 1|  
|7|00000111|0, 1 и 2|  
|15|00001111|0, 1, 2 и 3|  
|31|00011111|0, 1, 2, 3 и 4|  
|63|00111111|0, 1, 2, 3, 4 и 5|  
|127|01111111|0, 1, 2, 3, 4, 5 и 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6 и 7|  
  
 Параметр affinity mask является дополнительным. С помощью системной хранимой процедуры sp_configure изменить значение параметра **affinity mask** можно только при условии, что параметр **show advanced options** имеет значение 1. После выполнения команды [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE изменения параметров вступают в силу немедленно и не требуют перезапуска экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Доступ к неоднородной памяти (NUMA)  
 При использовании аппаратного доступа к неоднородной памяти (NUMA), если установлена маска сходства, каждый планировщик в узле сопоставляется своему собственному ЦП. Когда маска сходства не установлена, каждый планировщик соответствует группе процессоров в пределах узла NUMA, и планировщик, сопоставленный с узлом NUMA N1, может планировать работу на любом процессоре в узле, но не на процессорах, связанных с другим узлом.  
  
 Любая операция, выполняющаяся на одиночном узле NUMA, может использовать страницы буфера этого узла. Когда операция выполняется параллельно на процессорах из нескольких узлов, может использоваться память любого задействованного узла.  
  
## Вопросы лицензирования  
 Динамическое изменение схожести жестко ограничивается лицензированием по процессорам. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не позволяет использовать любые конфигурации параметров affinity mask, нарушающие политику лицензирования.  
  
### Запуск  
 Если применение заданного значения affinity mask приводит к нарушению политики лицензирования во время запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или во время присоединения базы данных, то уровень ядра завершает процесс запуска либо операцию присоединения или восстановления базы данных, а затем сбрасывает текущее значение sp_configure для параметра affinity mask в нуль, передавая сообщение об ошибке в журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### Повторная настройка  
 Если применение указанного значения affinity mask приводит к нарушению политики лицензирования при выполнении команды [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE, то сообщение об ошибке с требованием к администратору базы данных перенастроить значение affinity mask отправляется в сеанс клиента и в журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . В этом случае команда RECONFIGURE WITH OVERRIDE принята не будет.  
  
## См. также:  
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  