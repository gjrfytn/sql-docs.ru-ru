---
title: "Добавление зависимостей к ресурсу SQL Server | Документация Майкрософт"
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
- resource dependencies [SQL Server]
- failover clustering [SQL Server], dependencies
- clusters [SQL Server], dependencies
- dependencies [SQL Server], clustering
ms.assetid: 25dbb751-139b-4c8e-ac62-3ec23110611f
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bffe545296432d465fd744092519c9882ccc04c1
ms.lasthandoff: 04/11/2017

---
# <a name="add-dependencies-to-a-sql-server-resource"></a>добавить зависимости к ресурсу SQL Server
  В этом разделе описывается добавление зависимостей к ресурсам экземпляра отказоустойчивого кластера (FCI) AlwaysOn с помощью оснастки "Диспетчер отказоустойчивости кластеров". Оснастка «Диспетчер отказоустойчивости кластеров» — это приложение управления кластером для службы WSFC.  
  
-   **Before you begin:**  [Limitations and Restrictions](#Restrictions), [Prerequisites](#Prerequisites)  
  
-   **To add a dependency to a SQL Server resource, using:** [Windows Failover Cluster Manager](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> ограничения  
 При добавлении любых ресурсов к группе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] важно отметить, что добавляемый ресурс должен иметь уникальное сетевое имя и IP-адрес SQL.  
  
 Не используйте существующие в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]сетевые имена ресурсов и IP-адреса ресурсов в других целях. При совместном использовании ресурсов [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] другими программами могут возникнуть следующие проблемы.  
  
-   Возникновение неожиданных перебоев в работе.  
  
-   Неудачная установка пакетов обновления.  
  
-   Неправильная работа программы установки [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . При возникновении этой проблемы становится невозможным устанавливать дополнительные экземпляры [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] или выполнять обслуживание подпрограмм.  
  
 Рассмотрим эти дополнительные проблемы.  
  
-   Протокол FTP с репликацией [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . При работе с экземплярами [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , использующими протокол FTP с репликацией [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , служба FTP должна использовать один из тех же физических дисков, которые использует установка [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , настроенная на использование службы FTP.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Чтобы гарантировать доступность [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] при добавлении ресурса в группу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и существовании зависимости от ресурса [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , [!INCLUDE[msCoName](../../../includes/msconame-md.md)] рекомендует добавить зависимость для ресурса агента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Не добавляйте зависимость на ресурс [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Чтобы гарантировать высокий уровень доступности компьютера, на котором работает [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , необходимо настроить ресурс агента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] таким образом, чтобы сбой ресурса агента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не влиял на группу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Ресурсы общих папок и принтеров. При добавлении ресурсов общих папок или кластера печати не следует размещать их на физических дисках, используемых компьютером, на котором работает [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Размещение этих ресурсов на указанных жестких дисках может привести к снижению производительности и возможностей компьютера, на котором работает [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Замечания о координаторе MS DTC. После установки операционной системы и настройки FCI необходимо настроить координатор распределенных транзакций ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ) (MS DTC) для работы в кластере с помощью оснастки "Диспетчер отказоустойчивости кластеров". Если MS DTC не будет настроен для работы в кластере, это не помешает установке [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , но может ограничить функциональные возможности приложений [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Если координатор MS DTC установлен в группе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и имеются зависящие от него ресурсы, то MS DTC не будет доступен, когда эта группа оказывается вне сети или проходит отработку отказа. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] рекомендует поместить координатор MS DTC в отдельную группу с собственным ресурсом физического диска, если это возможно.  
  
###  <a name="Prerequisites"></a> предварительные требования  
 Если установить [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] в группе ресурсов WSFC с несколькими дисками и разместить данные на одном из этих дисков, то ресурс [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] будет зависеть только от этого диска. Чтобы разместить данные или журналы на других дисках, необходимо добавить для них зависимости к ресурсу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="WinClusManager"></a> Использование оснастки «Диспетчер отказоустойчивости кластеров»  
 **Добавление зависимости к ресурсу SQL Server**  
  
-   Откройте оснастку «Диспетчер отказоустойчивости кластеров»  
  
-   Выделите группу, содержащую ресурс [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , который необходимо сделать зависимым.  
  
-   Если ресурс, соответствующий диску, в группе уже существует, перейдите к шагу 4. В противном случае выберите группу, содержащую данный диск. Если эта группа не принадлежит к тому же узлу, что и группа, содержащая [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , группу, содержащую дисковый ресурс, необходимо переместить в указанный узел, содержащий группу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Выберите ресурс [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , откройте диалоговое окно **Свойства** и на вкладке **Зависимости** добавьте ссылку на диск в список зависимостей [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  