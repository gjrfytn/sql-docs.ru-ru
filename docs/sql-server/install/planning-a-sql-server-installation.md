---
title: "Планирование установки SQL Server | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 72117bfd62b37633e2b815fb1c8014b48c63d2ab
ms.lasthandoff: 04/11/2017

---
# <a name="planning-a-sql-server-installation"></a>Планирование установки SQL Server
  Чтобы установить [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], выполните описанные далее действия.  
  
-   Ознакомьтесь с требованиями по установке, сведениями о проверках конфигурации системы и вопросами безопасности для установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Запуск программы установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для установки или обновления до последней версии. Перед обновлением ознакомьтесь со статьей [Обновление до SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md).  
  
-   Настройка [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при помощи программ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Независимо от метода установки, необходимо подтвердить свое согласие с условиями лицензии на использование пакета программ как физического лица или от имени организации, если на используемое программное обеспечение не распространяется отдельное соглашение [!INCLUDE[msCoName](../../includes/msconame-md.md)] , такое как соглашение о корпоративном лицензировании Майкрософт или отдельное соглашение с независимым поставщиком программного обеспечения или изготовителем оборудования (OEM).  
  
 Условия лицензионного соглашения отображаются для ознакомления и принятия в пользовательском интерфейсе программы установки. Автоматические установки (с использованием параметров /Q или /QS) должны включать параметр /IAcceptSQLServerLicenseTerms. Ознакомиться с условиями лицензии можно на странице [Условия лицензионного соглашения о программном обеспечении Майкрософт](http://go.microsoft.com/fwlink/?LinkID=148209).  
  
> [!NOTE]  
>  В зависимости от способа получения ПО (например, по [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), на его использование могут распространяться дополнительные условия.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Новые возможности установки SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 В этом разделе подробно рассматриваются новые и усовершенствованные возможности установки в данной версии [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Требования к оборудованию и программному обеспечению для установки SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 В этом разделе перечислены минимальные требования к оборудованию и программному обеспечению, необходимые для установки и запуска экземпляра [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Вопросы безопасности при установке SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 В этой статье приведены некоторые рекомендации по безопасности, которых следует придерживаться как до, так [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и после установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Настройка учетных записей службы Windows и разрешений](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 В этом разделе описана конфигурация по умолчанию служб данного выпуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также параметры конфигурации служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые можно настроить во время и после установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [Сетевые протоколы и библиотеки](../../sql-server/install/network-protocols-and-network-libraries.md)  
 В этом разделе описана конфигурация сетевых протоколов, устанавливаемая по умолчанию для служб данной версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также доступные параметры для настройки.  
  
 [Работа с несколькими версиями и экземплярами SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 В этом разделе описаны рекомендации по установке нескольких версий и экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Версии SQL Server на местных языках](../../sql-server/install/local-language-versions-in-sql-server.md)  
 В этом разделе рассматриваются локализованные версии [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="related-sections"></a>См. также  
 [Установка SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
 В этом разделе представлены общие сведения о разных параметрах установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Установка компонентов бизнес-аналитики SQL Server 2016](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 В этом разделе документации по программе установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] описывается процедура установки функций [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые входят в состав платформы бизнес-аналитики Майкрософт.  
  
 [Обновление до SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)  
 В данном разделе представлена общая информация по обновлению экземпляров предыдущих версий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Удаление SQL Server 2016](../../sql-server/install/uninstall-sql-server.md)  
 В этом разделе описано, как полностью удалить существующий экземпляр [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] и подготовить систему к повторной установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Установка отказоустойчивого кластера SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 В этом разделе документации по программе установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] описывается процедура установки и настройки кластера отработки отказа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также:  
 [Установка SQL Server 2016 из командной строки](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Решения высокого уровня доступности (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Подготовка к установке отказоустойчивого кластера](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [Обновление до SQL Server 2016 с помощью мастера установки (программа установки)](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
