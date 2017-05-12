---
title: "Удаление объектов служб Data Quality Services | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 07a9b670a58f8ec0d6fcc0159b6237b7fc32dcbd
ms.lasthandoff: 04/11/2017

---
# <a name="remove-data-quality-server-objects"></a>Удаление объектов служб Data Quality Services
  При удалении [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] с экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]или при полном удалении экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , содержащего [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , некоторые объекты [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] сохраняются, в том числе базы данных служб DQS. Это означает, что при удалении сервера служб DQS с помощью программы установки SQL Server данные [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] не теряются. После завершения процесса удаления эти объекты [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] необходимо удалить вручную.  
  
> [!NOTE]  
>  -   Перед удалением [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]рассмотрите возможность создания резервных копий всех имеющихся баз знаний путем их экспорта в файл DQSB, который впоследствии можно будет использовать для импорта всех баз знаний в новую установку [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Экспорт и импорт всех баз знаний служб DQS можно выполнить только с помощью программы DQSInstaller.exe, запускаемой из командной строки с соответствующими параметрами. Дополнительные сведения см. в статье [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).  
> -   Перед удалением баз данных служб DQS, возможно, следует создать их резервную копию для последующего восстановления. Дополнительные сведения об этой процедуре см. в разделе [Управление базами данных DQS](../../data-quality-services/manage-dqs-databases.md).  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>Удаление сервера DQS с экземпляра SQL Server  
 После удаления сервера [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] с экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]необходимо вручную удалить следующие объекты сервера [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] с экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] после того, как процесс удаления сервера [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] будет завершен:  
  
-   Базы данных DQS_MAIN, DQS_PROJECTS и DQS_STAGING_DATA.  
  
-   \#Имена для входа ##MS_dqs_db_owner_login## и ##MS_dqs_service_login##.  
  
-   Хранимая процедура DQInitDQS_MAIN из базы данных master.  
  
 Эти объекты можно удалить в среде SQL Server Management Studio, щелкнув правой кнопкой мыши объект и выбрав в контекстном меню пункт **Удалить** .  
  
> [!IMPORTANT]  
>  Если сервер [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] удаляется с экземпляра SQL Server с помощью параметра командной строки `–uninstall` , то в рамках процесса удаления будут удалены все объекты служб DQS. Удалять данные объекты вручную после удаления сервера [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]не потребуется. Для удаления [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] из командной строки введите следующую команду в командной строке и нажмите клавишу ВВОД:   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Удаление экземпляра SQL Server, содержащего сервер DQS  
 При полном удалении экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , содержащего сервер [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], необходимо вручную удалить базы данных DQS_MAIN, DQS_PROJECTS и DQS_STAGING_DATA с компьютера после завершения процесса удаления. В установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию файлы баз данных DQS_MAIN, DQS_PROJECTS и DQS_STAGING_DATA находятся в папке C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA.  
  
## <a name="see-also"></a>См. также:  
 [Удаление существующего экземпляра SQL Server (программа установки)](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Удаление SQL Server 2016](../../sql-server/install/uninstall-sql-server.md)  
  
  