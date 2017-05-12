---
title: "Определение версии схемы определения отчета (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML-схемы [службы Reporting Services]"
  - "язык определения отчетов, схема XML"
  - "схемы [службы Reporting Services]"
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# Определение версии схемы определения отчета (SSRS)
  В файле определения отчета указывается пространство имен языка определения отчетов для версии схемы определения отчета, использованной для проверки RDL-файла. Если RDL-файл открывается в среде разработки отчетов, такой как конструктор в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , или построителе отчетов и если отчет был создан в предыдущем пространстве имен, автоматически создается файл резервной копии и отчет обновляется до текущего пространства имен. Если сохранить обновленное определение отчета, будет сохранен преобразованный RDL-файл. Это единственный способ обновления определения отчетов. Само определение отчетов не обновляется на сервере отчетов. Скомпилированный отчет обновляется на сервере отчетов. Дополнительные сведения см. в разделе [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
### Инструкции. Определение версии RDL-схемы отчета  
  
1.  Откройте файл отчета в формате RDL в приложении, таком как «Блокнот» или XML Notepad 2007, пригодном для просмотра XML-кода.  
  
     XML-элемент Report указывает пространство имен схемы. Например, следующий элемент Report указывает пространство имен для конструктора отчетов и пространство имен для определения отчета.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Пространство имен определения отчета указано следующим URL-адресом: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`.  
  
### Как определить версию RDL-схемы конструктора отчетов  
  
1.  Открыть новый проект. Версия выбранного проекта определяет версию схемы языка определения отчетов. В [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]поддерживается использование нескольких версий схемы. Дополнительные сведения см. в разделе [Развертывание и поддержка версий в SQL Server Data Tools (SSRS)](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  В меню **Проект** выберите **Добавить новый элемент**. Откроется диалоговое окно **Добавление нового элемента** .  
  
3.  На панели **Шаблоны** нажмите кнопку **Отчет**.  
  
4.  В поле **Имя**введите имя отчета или примите имя по умолчанию.  
  
5.  Нажмите кнопку **Добавить**. Конструктор отчетов открывает новый пустой отчет в режиме конструктора.  
  
6.  В меню **Вид** выберите пункт **Код**. Определение отчета отображается в виде XML-файла.  
  
     XML-элемент Report указывает пространство имен схемы. Например, следующий элемент Report указывает пространство имен для конструктора отчетов и пространство имен для определения отчета.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Пространство имен определения отчета указано следующим URL-адресом: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### Инструкции. Определение версии RDL-схемы отчета на сервере отчетов  
  
-   В диспетчере отчетов введите URL-адрес сервера отчетов. Например, следующий URL-адрес указывает сервер отчетов на локальном компьютере.  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     XSD-файл открывается в браузере.  
  
     Элемент XML-схемы указывает пространство имен схемы. Например, следующий элемент схемы указывает три пространства имен: ссылку targetNamespace, которая используется в среде [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], XSD-ссылку для самой схемы (XSD) и ссылку определения отчета.  
  
    ```  
    <xsd:schema   
    targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     Пространство имен определения отчета указано следующим URL-адресом: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
## См. также  
 [Обновление отчетов](../../reporting-services/install-windows/upgrade-reports.md)   
 [Язык определения отчетов (службы SSRS)](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  