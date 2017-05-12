---
title: "Общие сведения о службах Master Data Services (MDS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "what is master data"
helpviewer_keywords: 
  - "Master Data Services, обзор"
  - "Службы Master Data Services"
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
caps.latest.revision: 28
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 27
---
# Общие сведения о службах Master Data Services (MDS)
  В этом разделе описаны ключевые функции организации данных и управления ими с помощью [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. 
  
 >  Описание архитектуры [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] см. в статье [Master Data Services — основы](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) на сайте simple-talk.com. Сведения о новых функциях [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] см. на странице [Новые возможности Master Data Services (MDS)](../master-data-services/what-s-new-in-master-data-services-mds.md).  
   **Инструкции по установке [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], настройке базы данных и веб-сайта и развертыванию образцов моделей см. в статье **[Установка и конфигурация служб Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
  
 В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]модель является наивысшим уровнем контейнера в структуре основных данных. Можно создать модель для управления группами сходных данных, например для управления данными продуктов в сети. В модели содержится одна или несколько сущностей, а сущности содержат элементы, которые являются записями данных. Сущность похожа на таблицу.  
  
 Модель продукта в сети может содержать сущности, такие как продукт, цвет и стиль. Сущность цвета может содержать элементы для красного, серебряного и черного цвета.  
  
 ![Color entity](../master-data-services/media/mds-productmodel-colorentity-composite.png "Color entity")  
  
 Модели также содержат атрибуты, определенные в сущностях. Атрибут содержит значения, которые помогают описывать элементы сущности. Существуют атрибуты в свободной форме и атрибуты на основе домена.  Атрибут на основе домена содержит значения, которые заполняются элементами из сущности и могут использоваться как значения атрибутов для других сущностей.  
  
 Например, в сущности продукта могут иметься атрибуты в свободной форме для стоимости и веса. В то же время там может быть атрибут на основе домена для цвета ![Number 1](../master-data-services/media/mds-number1.png "Number 1"), значения которого заполняются элементами сущности цвета. Этот основной список цветов используется в качестве значений атрибута для сущности продукта ![Number 2](../master-data-services/media/mds-number2.png "Number 2").  
  
 ![Domain-based attribute for color](../master-data-services/media/mds-productentity-color-domainattribute.png "Domain-based attribute for color")  
  
 Производные иерархии происходят от связей между сущностями в модели. Это связи атрибутов на основе домена. Например, в модели продукта может быть производная иерархия цвета ![Number 1](../master-data-services/media/mds-number1.png "Number 1"), происходящая от связи между сущностями цвета ![Number 2](../master-data-services/media/mds-number2.png "Number 2") и продукта ![Number 3](../master-data-services/media/mds-number3.png "Number 3").  
  
 ![Color derived hierarchy](../master-data-services/media/mds-derivedhierarchy.png "Color derived hierarchy")  
  
 После определения базовой структуры данных можно начать добавление записей данных (элементов) с помощью функции импорта. Загрузите данные в промежуточные таблицы, проверьте данные с помощью бизнес-правил и загрузите данные в таблицы MDS.  Также можно использовать бизнес-правила для задания значений атрибутов.  
  
 В следующей таблице описываются основные задачи [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Если не указано другое, для всех следующих процедур необходимо иметь права администратора модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
> [!NOTE]  
>  Следующие задачи можно выполнить в тестовой среде и использовать предложенные образцы данных при установке служб [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Дополнительные сведения см. в разделе [Развертывание моделей (службы Master Data Services)](../master-data-services/deploying-models-master-data-services.md).  
  
|Действие|Сведения|См. также|  
|------------|-------------|--------------------|  
|Создание модели|При создании модели она считается версией VERSION_1.|[Модели (службы Master Data Services)](../master-data-services/models-master-data-services.md)<br /><br /> [Создание модели (службы Master Data Services)](../master-data-services/create-a-model-master-data-services.md)|  
|Создание сущностей|Создавайте столько сущностей, сколько необходимо для хранения элементов.|[Сущности (службы Master Data Services)](../master-data-services/entities-master-data-services.md)<br /><br /> [Создание сущности (службы Master Data Services)](../master-data-services/create-an-entity-master-data-services.md)|  
|Создание сущностей для использования в качестве атрибутов на основе домена|Чтобы создать атрибут на основе домена, сначала нужно создать сущность для заполнения списка значений атрибута.|[Атрибуты на основе домена (службы Master Data Services)](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [Создание атрибута на основе домена (службы Master Data Services)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Создание атрибутов для сущностей|Атрибуты создаются для описания элементов. Атрибуты Name и Code автоматически включаются в каждую сущность, и их нельзя удалить. Можно создать другие атрибуты в свободной форме для хранения текста, дат, чисел или файлов.|[Атрибуты (службы Master Data Services)](../master-data-services/attributes-master-data-services.md)<br /><br /> [Создание текстового атрибута (службы Master Data Services)](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [Создание числового атрибута (службы Master Data Services)](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [Создание атрибута даты (службы Master Data Services)](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [Создание атрибута ссылки (службы Master Data Services)](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [Создание файлового атрибута (службы Master Data Services)](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|Создание групп атрибутов|При наличии четырех или пяти атрибутов для сущности можно создавать группы атрибутов. Эти группы представлены вкладками наверху сетки в **Обозревателе** и упрощают навигацию за счет группирования атрибутов на отдельных вкладках.|[Группы атрибутов (службы Master Data Services)](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [Создание группы атрибутов (службы Master Data Services)](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Импорт элементов для поддерживающих сущностей|Данные для поддерживающих сущностей импортируются с использованием промежуточного процесса. Для модели Product это может означать импорт цветов или размеров. Элементы также можно создавать вручную.<br /><br /> <br /><br /> Примечание. Пользователи могут создавать элементы в [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , если у них есть как минимум разрешение на **обновление** конечного объекта модели сущности и доступ к функциональной области **Обозреватель** .|[Обзор: импорт данных из таблиц (службы Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [Создание конечного элемента (службы Master Data Services)](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Создание и применение бизнес-правил, обеспечивающих высокое качество данных|Для гарантии точности данных создаются и публикуются бизнес-правила. Бизнес-правила можно использовать в следующих целях:<br /><br /> установка значений атрибута по умолчанию;<br /><br /> изменение значений атрибута;<br /><br /> отправка уведомлений по электронной почте, если данные не проходят проверку на соответствие бизнес-правилам.|[Бизнес-правила (службы Master Data Services)](../master-data-services/business-rules-master-data-services.md)<br /><br /> [Создание и публикация бизнес-правила (службы Master Data Services)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [Подтверждение конкретных членов, обнаруженных при проверке на соответствие бизнес-правилам (службы Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [Настройка уведомления электронной почты (службы Master Data Services)](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [Настройка в бизнес-правилах отправки уведомлений (службы Master Data Services)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Импорт элементов для основных сущностей и применение бизнес-правил|Элементы для основных сущностей импортируются с использованием промежуточного процесса. По окончании импорта следует проверить версию, что включает применение бизнес-правил ко всем элементам версии модели.<br /><br /> После этого можно исправить выявленные проблемы с проверкой соответствия бизнес-правилам.|[Проверка (службы Master Data Services)](../master-data-services/validation-master-data-services.md)<br /><br /> [Подтверждение исправления проблемы, обнаруженной при проверке на соответствие бизнес-правилам (службы Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [Проверка хранимых процедур (службы Master Data Services)](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|Создание производных иерархий|Производные иерархии можно обновлять по мере изменения бизнес-потребностей для обеспечения учета всех элементов на соответствующем уровне.|[Производные иерархии (службы Master Data Services)](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [Создание производной иерархии (службы Master Data Services)](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Создание явных иерархий при необходимости|При необходимости использовать иерархии, отличные от многоуровневых, которые включают элементы из одной сущности, можно создавать явные иерархии.|[Явные иерархии (службы Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [Создание явной иерархии (службы Master Data Services)](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Создание коллекций при необходимости|Если необходимо представить разные группы элементов для отчетов или анализа и не нужно создавать полную иерархию, используются коллекции.<br /><br /> <br /><br /> Примечание. Пользователи могут создавать элементы в [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , если у них есть как минимум разрешение на **обновление** объекта модели коллекции и доступ к функциональной области **Обозреватель** .|[Коллекции (службы Master Data Services)](../master-data-services/collections-master-data-services.md)<br /><br /> [Создание коллекции (службы Master Data Services)](../master-data-services/create-a-collection-master-data-services.md)|  
|Создание определяемых пользователем метаданных|Для описания объектов модели в модель добавляются пользовательские метаданные. Эти метаданные могут включать владельца объекта или источник данных.|[Метаданные (службы Master Data Services)](../Topic/Metadata%20\(Master%20Data%20Services\).md)|  
|Блокировка версии модели и назначение флага версии|Версия модели может блокироваться, чтобы запретить изменять элементы всем пользователям, кроме администраторов. После проверки данных версии на соответствие бизнес-правилам можно зафиксировать версию, чтобы запретить всем пользователям изменять элементы.<br /><br /> Создание и назначение флага версии модели. Флаги помогают пользователям и системам-подписчикам определять используемую версию модели.|[Версии (службы Master Data Services)](../master-data-services/versions-master-data-services.md)<br /><br /> [Блокировка версии (службы Master Data Services)](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [Создание флага версии (службы Master Data Services)](../master-data-services/create-a-version-flag-master-data-services.md)|  
|Создание представлений подписки|Чтобы системы подписки использовали основные данные, нужно создать представления подписки, которые создают стандартные представления в базе данных [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Обзор. Экспорт данных (службы Master Data Services)](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [Создание представления подписки для экспорта данных (службы Master Data Services)](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Настройка разрешений для пользователей и групп|Разрешения для пользователей и групп нельзя копировать из тестовой в рабочую среду. Однако тестовую среду можно использовать для определения уровня безопасности, который необходимо будет использовать в производственной среде.|[Безопасность (службы Master Data Services)](../master-data-services/security-master-data-services.md)<br /><br /> [Добавление группы (службы Master Data Services)](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [Добавление пользователя (службы Master Data Services)](../master-data-services/add-a-user-master-data-services.md)|  
  
 По окончании можно развернуть модель в рабочей среде с данными или без них. Дополнительные сведения см. в разделе [Развертывание моделей (службы Master Data Services)](../master-data-services/deploying-models-master-data-services.md).  
  
  