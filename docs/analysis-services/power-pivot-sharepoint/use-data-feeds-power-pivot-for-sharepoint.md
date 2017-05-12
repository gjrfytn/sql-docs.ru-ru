---
title: "Использование веб-каналов данных (PowerPivot для SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# Использование веб-каналов данных (PowerPivot для SharePoint)
  Канал данных — это один или несколько потоков данных, формируемых из источника данных в сети и направляемых в целевой документ или приложение. При использовании [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для Excel веб-каналы данных позволяют получать существующие корпоративные данные или бизнес-данные из произвольных источников данных в окне [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] книги Excel 2010. После импорта веб-канала данных в книгу на него можно ссылаться в любых операциях обновления данных, планируемых на сервере SharePoint.  
  
 Использование веб-канала данных зависит от того, используются встроенные функции экспорта в приложениях, поддерживающих веб-каналы данных Atom, или настраиваемые службы данных. Приложения, которые могут публиковать и считывать XML-данные Atom, позволяют передавать данные таким образом, чтобы пользователю не нужно было работать с каналами данных и службами. С точки зрения пользователя данные просто перемещаются между приложениями.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] и Microsoft SharePoint 2010 предоставляют веб-каналы данных, которые могут быть использованы в книгах [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Сведения в данном разделе можно использовать для изучения доступа к веб-каналам данных из уже имеющихся отчетов и списков.  
  
 Этот раздел состоит из следующих подразделов.  
  
 [Предварительные требования](#prereq)  
  
 [Создание веб-канала данных из списка SharePoint](#sharepointlist)  
  
 [Создание веб-канала данных на основе отчета служб Reporting Services](#rsreport)  
  
 [Создание веб-канала данных на основе сервисного документа данных](#dsdoc)  
  
##  <a name="prereq"></a> Предварительные требования  
 Для импорта веб-канала данных в Excel 2010 требуется [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для Excel.  
  
 Необходима веб-служба или служба данных, которые поставляют данные в формате Atom 1.0. И службы [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , и SharePoint 2010 могут предоставлять данные в этом формате.  
  
 Перед экспортом списка SharePoint в качестве веб-канала данных необходимо установить на сервере SharePoint службы ADO.NET Data Services. Дополнительные сведения см. в разделе [Установка служб ADO.NET Data Services для поддержки экспорта списков SharePoint в виде веб-каналов данных](http://msdn.microsoft.com/ru-ru/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="sharepointlist"></a> Создание веб-канала данных из списка SharePoint  
 На ферме SharePoint 2010 список SharePoint имеет кнопку «Экспортировать как веб-канал данных» на ленте списка. Нажав ее, можно экспортировать лист в качестве канала. Для получения наилучших результатов на рабочей станции необходимо установить Excel 2010 с клиентским приложением [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . В ответ на экспорт веб-канала данных запускается клиентское приложение [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] и создается таблица [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , в которой содержится список.  
  
1.  Откройте список на сайте SharePoint.  
  
2.  В окне «Средства списков» нажмите кнопку **Список**.  
  
3.  В окне «Подключение и Экспорт» нажмите кнопку **Экспортировать как веб-канал данных**.  
  
    > [!NOTE]  
    >  Кнопка **Экспортировать как веб-канал данных** добавляется в SharePoint с помощью [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Если надстройка [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint не установлена или компонент [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] не активирован, эта кнопка будет недоступна.  
  
4.  Нажмите кнопку **Открыть** , если надстройка [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для Excel установлена локально, или кнопку **Сохранить** , чтобы сохранить ATOMSVC-документ на жесткий диск и импортировать операции позже.  
  
5.  Если выбрано **открытие документа**, используйте мастер импорта таблиц для импорта веб-канала данных на лист. Веб-канал данных будет добавлен в окно [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в виде новой таблицы.  
  
 Если службы ADO.NET Data Services 3.5.1 не установлены на сервере SharePoint, возникнет ошибка. Дополнительные сведения об ошибках и способах их устранения см. в статье [Установка служб ADO.NET Data Services для поддержки экспорта списков SharePoint в виде веб-каналов данных](http://msdn.microsoft.com/ru-ru/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="rsreport"></a> Создание веб-канала данных на основе отчета служб Reporting Services  
 Если на компьютере развернуты службы SQL Server 2008 R2 Reporting Services, можно использовать новый модуль подготовки отчетов Atom для создания веб-канала данных из существующего отчета. Для получения наилучших результатов на рабочей станции должно быть установлено приложение Excel 2010 с надстройкой [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для Excel. Клиентское приложение [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] запустится в ответ на экспорт канала данных, автоматически добавит и свяжет таблицы и столбцы по мере их поступления в поток.  
  
 Инструкции по экспорту потока данных из отчета см. в разделе [Формирование веб-каналов данных из отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) [справки по построителю отчетов](http://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Чтобы настроить повторяющееся обновление данных по расписанию, при котором выполняется повторный импорт данных отчетов в книгу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], опубликованную в библиотеке SharePoint, сервер отчетов должен быть настроен в режиме интеграции с SharePoint. Дополнительные сведения о совместном использовании [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint и Reporting Services см. в статье [Настройка и администрирование сервера отчетов (режим интеграции с SharePoint служб Reporting Services)](../../reporting-services/report-server-sharepoint/configuration and administration of a report server.md).  
  
##  <a name="dsdoc"></a> Создание веб-канала данных на основе сервисного документа данных  
 Если имеется пользовательская служба данных, которая формирует веб-каналы Atom, то можно настроить сервисный документ данных, чтобы сделать данные доступными для пользователей и приложений. В файле *сервисного документа данных* (ATOMSVC) указывается одно или несколько соединений с источниками в сети, которые публикуют данные в формате подключения Atom. Сервисные документы данных можно создать в *библиотеке каналов данных*, которая является специальной библиотекой, обеспечивающей точку общего доступа для поиска сервисных документов данных, опубликованных на сервере SharePoint. Информационные работники, имеющие разрешение на доступ к сервисным документам данных в библиотеке веб-каналов данных, могут использовать URL-адрес документа на SharePoint для импорта веб-каналов данных в свои книги и приложения.  
  
1.  Откройте библиотеку веб-каналов данных, которая создана администратором сайта. Дополнительные сведения см. в разделе [Создание или настройка библиотеки веб-каналов данных (PowerPivot для SharePoint)](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  В инструментах библиотеки выберите **Документы**.  
  
3.  Нажмите кнопку **Создать документ**.  
  
4.  Введите имя файла и описание.  
  
5.  Укажите один или несколько URL-адресов, по которым передается канал.  
  
    1.  **Базовый URL-адрес** является необязательным. Его следует указывать, если сервисный документ данных содержит несколько каналов. В базовом URL-адресе должна указываться часть URL-адреса, общая для всех каналов (например, имя сервера и сайт). Если создается сервисный документ данных для отчета служб Reporting Services, то базовым URL-адресом будет URL-адрес сервера отчетов и отчет.  
  
    2.  **URL-адрес веб-службы** является обязательным. В отсутствие базового URL-адреса это значение должно содержать http:// или https://. Если указан базовый URL-адрес, то URL-адрес веб-службы представляет часть URL-адреса, следующую за базовым адресом. Например, если полный URL-адрес имеет вид http://adventure-works/inventory/today.aspx, то базовым URL-адресом будет http://adventure-works/inventory, а URL-адресом веб-службы будет /today.aspx.  
  
         В URL-адрес веб-службы могут входить параметры, выполняющие фильтрацию или выбирающие подмножество данных. Приложение или служба, предоставляющие канал, должны поддерживать параметры, указываемые в URL-адресе.  
  
6.  Введите в поле **Имя таблицы**по одной таблице на каждый канал. Это значение обязательно. Имя таблицы используется клиентским приложением, получающим веб-канал данных. В [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для Excel имя таблицы используется для таблиц в окне [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , которые будут содержать импортируемые данные.  
  
## См. также  
 [Включение интеграции функций PowerPivot для семейств веб-сайтов в центре администрирования](../../analysis-services/power-pivot-sharepoint/activate power pivot integration for site collections in ca.md)   
 [Совместное использование веб-каналов данных PowerPivot с помощью библиотеки каналов данных (PowerPivot для SharePoint)](../../analysis-services/power-pivot-sharepoint/share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  