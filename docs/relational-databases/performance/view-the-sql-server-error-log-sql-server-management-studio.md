---
title: "Просмотр журнала ошибок SQL Server (среда SQL Server Management Studio) | Документация Майкрософт"
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4acdc87a3317c38b5b19235dae681bce426244e3
ms.lasthandoff: 04/11/2017

---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Просмотр журнала ошибок SQL Server (среда SQL Server Management Studio)
  В журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] записываются пользовательские и определенные системные события, которые пригодятся при устранении неполадок. 
  

  ## <a name="how-to-view-the-logs"></a>Просмотр журналов
1.  В SSMS выберите **Обозреватель объектов**

>Чтобы **открыть** обозреватель объектов, используйте клавишу **F8**на клавиатуре. Или в главном меню щелкните "Вид"/"Обозреватель объектов" ![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 


2.  В **обозревателе объектов**подключитесь к экземпляру SQL Server и разверните его.
  
3.  Найдите и разверните раздел **Управление** (при условии, что у вас есть разрешения на его просмотр).

4.  Щелкните правой кнопкой мыши **Журналы SQL Server**, выберите "Просмотр" и **Просмотр журнала SQL Server**.
 ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5.  Отображается средство просмотра журнала (это может занять около минуты) со списком журналов для просмотра.
  
6. Несколько пользователей порекомендовали статью [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/) (Расположение удостоверения для файла журнала SQL Server) на сайте [MSSQLTips.com](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/). Там доступно еще огромное количество полезной информации, советуем вам ознакомиться с этим ресурсом.
  
  
