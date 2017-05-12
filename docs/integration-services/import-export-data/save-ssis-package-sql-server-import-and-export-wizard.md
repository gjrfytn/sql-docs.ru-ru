---
title: "Сохранение пакета служб SSIS (мастер экспорта и импорта SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.savedtspackage.f1"
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Сохранение пакета служб SSIS (мастер экспорта и импорта SQL Server)
  Если на странице **Сохранение и запуск пакета** вы указали, что хотите сохранить созданный пакет служб SSIS, мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] отображает окно **Сохранение пакета служб SSIS**. На этой странице можно указать дополнительные параметры для сохранения пакета.  

Параметры, которые вы видите на странице **Сохранение пакета служб SSIS**, зависят от выбора, сделанного ранее на странице **Сохранение и запуск пакета** и касающегося сохранения пакета в SQL Server или в файловой системе. Чтобы ознакомиться с описанием страницы **Сохранение и запуск пакета**, см. раздел [Сохранение и запуск пакета](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**Что такое пакет?** Мастер использует службы SQL Server Integration Services (SSIS) для копирования данных. В службах SSIS основной единицей является пакет. По мере перемещения по страницам и указания параметров мастер создает пакет служб SSIS в памяти.
 
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Снимок экрана: сохранение пакета в файловой системе
 
На следующем снимке экрана показана страница мастера **Сохранение пакета служб SSIS**, отображаемая после выбора параметра **Файловая система** на странице **Сохранение и запуск пакета**. 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package1.png "Save SSIS Package page of the Import and Export Wizard")  

## <a name="screen-shot---save-the-package-in-sql-server"></a>Снимок экрана: сохранение пакета в SQL Server

 На следующем снимке экрана показана страница мастера **Сохранение пакета служб SSIS**, отображаемая после выбора параметра **SQL Server** на странице **Сохранение и запуск пакета**. 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package2.png "Save SSIS Package page of the Import and Export Wizard")  
  
## <a name="provide-a-name-and-description-for-the-package"></a>Укажите имя и описание пакета  
 **Название**  
 Введите уникальное имя пакета.  
  
 **Описание**  
 Введите описание пакета. Рекомендуется описать назначение пакета, чтобы сделать работу с пакетами проще и понятнее.  
  
 **Цель**  
 Назначение ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или файловая система), указанное ранее для пакета. Если вы хотите сохранить пакет в другом назначении, вернитесь на страницу **Сохранение и запуск пакета**.
  
## <a name="save-the-package-in-the-file-system"></a>Сохранение пакета в файловой системе 
Если в качестве назначения выбрана файловая система, заполните следующие поля.

 **Имя файла**  
 Введите путь и имя файла для целевого файла или используйте кнопку **Обзор**, чтобы выбрать расположение.  
  
> [!TIP] Не забудьте указать конечную папку, введя ее либо перейдя к ней. Если ввести только имя файла без пути, вы не будете знать, где мастер сохранит пакет. Кроме того, мастер может попытаться сохранить пакет в расположении, где у него нет разрешения на сохранение файлов, что приводит к ошибке.  
>   
>  Запомните, где именно сохранен пакет.  
  
 **Обзор**  
 Можно также перейти по пути к целевому файлу в диалоговом окне **Сохранение пакета**.  

## <a name="save-the-package-in-sql-server"></a>Сохранение пакета в SQL Server 
Если в качестве назначения выбран [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], заполните следующие поля.

Мастер сохраняет пакет в таблице **sysssispackages** базы денных **msdb**.
 
 > [!NOTE] При выборе этого параметра пакет не сохраняется в базе данных каталога служб SSIS (SSISDB).  
 
 **Имя сервера**  
 Введите или выберите имя целевого сервера.  
   
 **Использовать проверку подлинности Windows**  
Подключитесь к серверу, используя встроенную проверку подлинности Windows. Предпочтителен этот метод проверки подлинности.  
  
 **Использовать проверку подлинности SQL Server**  
Подключитесь к серверу, используя проверку подлинности SQL Server.  
  
 **Имя пользователя**  
Если указана проверка подлинности SQL Server, введите имя пользователя [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Пароль**  
Если указана проверка подлинности SQL Server, введите пароль [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Сведения о двух страницах с параметрами сохранения пакета  
 Страница **Сохранение пакета служб SSIS** является одной из двух страниц, на которых выбираются параметры для сохранения пакета служб SSIS.  
  
-   На предыдущей странице **Сохранение и выполнение пакета** выбирается тип сохранения пакета — в SQL Server или в виде файла. Здесь также указываются параметры безопасности для сохраняемого пакета. Чтобы ознакомиться с описанием страницы **Сохранение и запуск пакета**, см. раздел [Сохранение и запуск пакета](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
  
-   На текущей странице указывается имя пакета и вводятся дополнительные сведения о месте его сохранения.  
 
## <a name="run-the-saved-package-again-later"></a>Повторный запуск сохраненного пакета  
 Сведения о том, как снова запустить сохраненный пакет, см. в одном из следующих разделов:  
  
-   Чтобы запустить пакет с помощью служебной программы с удобным пользовательским интерфейсом, см. раздел [Справочник по пользовательскому интерфейсу программы выполнения пакетов (DtExecUI)](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).  
  
-   Чтобы запустить пакет из командной строки или из пакетного файла, см. раздел [Программа dtexec](../../integration-services/packages/dtexec-utility.md).  
  
-   Если пакет сохранен в файловой системе, см. раздел [Запуск пакета с помощью SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md) для запуска пакета в среде разработки. прежде чем открыть и запустить пакет, следует добавить его в проект служб Integration Services.  
 
-   Если пакет сохранен в базе данных **msdb** SQL Server, подключитесь к службам Integration Services. Затем обозревателе объектов в среде SQL Server Management Studio перейдите к окну **Сохраненные пакеты | MSDB**, щелкните пакет правой кнопкой мыши и выберите **Выполнить пакет**.

## <a name="customize-the-saved-package"></a>Настройка сохраненного пакета  
 Дополнительные сведения о настройке сохраненного пакета см. в разделе [Пакеты служб Integration Services (SSIS)](../../integration-services/integration-services-ssis-packages.md).  
  
## <a name="whats-next"></a>Дальнейшие действия  
 После указания дополнительных параметров для сохранения пакета выполняется переход на страницу **Завершение работы мастера**. На этой странице просмотрите параметры, выбранные в мастере, и запустите операцию. Дополнительные сведения см. в разделе [Завершение работы мастера](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>См. также:  
[Сохранение пакетов](../../integration-services/save-packages.md)  
[Запуск пакетов служб Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 