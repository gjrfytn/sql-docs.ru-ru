---
title: "Настройка параметров NodeWeight кворума кластера | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2c43965a7e6b0021bb4bcf2d6fdca14e66cafa18
ms.lasthandoff: 04/11/2017

---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>Настройка параметров NodeWeight кворума кластера
  В этом разделе описан порядок настройки параметров NodeWeight для узла элемента в отказоустойчивом кластере Windows Server (WSFC). Параметры NodeWeight используются при определении голосов в кворуме для поддержки аварийного восстановления и сценариев с несколькими подсетями для экземпляров отказоустойчивого кластера [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] и [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **To view quorum NodeWeight settings using:** [Using Powershell](#PowerShellProcedure), [Using Cluster.exe](#CommandPromptProcedure)  
  
-   [См. также](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Перед началом работы  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Эта функция поддерживается только в [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] или более поздних версиях.  
  
> [!IMPORTANT]  
>  Для использования параметров NodeWeight необходимо применить следующее исправление ко всем серверам в кластере WSFC:  
>   
>  [KB2494036](http://support.microsoft.com/kb/2494036): доступно исправление, позволяющее настраивать узел кластера, не имеющий голосов кворума в [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] и в [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Если это исправление не установлено, то в примерах этого раздела будут возвращены пустые значения или значения NULL для NodeWeight.  
  
###  <a name="Security"></a> Безопасность  
 Пользователь должен входить в учетную запись домена, которая является членом локальной группы администраторов, на каждом узле кластера WSFC.  
  
##  <a name="PowerShellProcedure"></a> Использование Powershell  
  
##### <a name="to-configure-nodeweight-settings"></a>Настройка параметров NodeWeight  
  
1.  Запустите повышенный режим Windows PowerShell с помощью команды **Запуск от имени администратора**.  
  
2.  Импортируйте модуль `FailoverClusters` для включения командлетов кластера.  
  
3.  Используйте объект `Get-ClusterNode` для задания свойства `NodeWeight` для каждого узла в кластере.  
  
4.  Выведите свойства узла кластера в удобном для чтения формате.  
  
### <a name="example-powershell"></a>Пример (Powershell)  
 В приведенном ниже примере изменяется параметр NodeWeight в целях удаления голоса кворума для узла "Always OnSrv1", а затем происходит вывод параметров для всех узлов в этом кластере.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = “Always OnSrv1”  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Использование Cluster.exe  
  
> [!NOTE]  
>  Программа cluster.exe является устаревшей в выпуске [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Для будущих разработок используйте PowerShell с отказоустойчивым кластером.  Программа cluster.exe будет удалена в следующем выпуске Windows Server. Дополнительные сведения см. в разделе [Сопоставление команд Cluster.exe с командлетами Windows PowerShell для отказоустойчивых кластеров](http://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### <a name="to-configure-nodeweight-settings"></a>Настройка параметров NodeWeight  
  
1.  Запустите повышенный режим командной строки с помощью команды **Запуск от имени администратора**.  
  
2.  Используйте программу **cluster.exe** для задания значений `NodeWeight` .  
  
### <a name="example-clusterexe"></a>Пример (Cluster.exe)  
 В приведенном ниже примере изменяется значение NodeWeight для удаления голоса кворума узла "Always OnSrv1" в кластере "Cluster001".  
  
```ms-dos  
cluster.exe Cluster001 node Always OnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> См. также  
  
-   [Просмотр событий и журналов для отказоустойчивого кластера](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Командлет Get-ClusterLog отказоустойчивого кластера](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>См. также:  
 [Режим кворума и участвующая в голосовании конфигурация WSFC (SQL Server)](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Просмотр параметров NodeWeight кворума кластера](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [Командлеты отказоустойчивого кластера в Windows PowerShell по выполняемым задачам](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  