---
title: "Редактор преобразования &#171;Нечеткий уточняющий запрос&#187; (вкладка &#171;Ссылочная таблица&#187;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzylookuptransformation.referencetable.f1"
helpviewer_keywords: 
  - "редактор преобразования «Нечеткий уточняющий запрос»"
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Редактор преобразования &#171;Нечеткий уточняющий запрос&#187; (вкладка &#171;Ссылочная таблица&#187;)
  Вкладка **Ссылочная таблица** в диалоговом окне **Редактор преобразования «Нечеткий уточняющий запрос»** позволяет указать исходную таблицу и индекс поиска. Эталонный источник данных должен быть таблицей в базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Преобразование «Нечеткий уточняющий запрос» создает рабочую копию ссылочной таблицы. В этой рабочей таблице описанные ниже индексы создаются с помощью специальной таблицы, а не обычных индексов [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Преобразование не изменяет существующие исходные таблицы, если не выбран параметр **Поддерживать хранимый индекс**. Если параметр выбран, в таблице ссылок создается триггер, который обновляет рабочую таблицу и таблицу индекса уточняющего запроса при изменениях в ссылочной таблице.  
  
> [!NOTE]  
>  Свойства **Exhaustive** и **MaxMemoryUsage** преобразования «Нечеткий уточняющий запрос» недоступны в диалоговом окне **Редактор преобразования «Нечеткий уточняющий запрос»**, но могут быть заданы с помощью диалогового окна **Расширенный редактор**. К тому же значения параметра **MaxOutputMatchesPerInput** больше 100 могут быть заданы только в окне **Расширенный редактор**. Дополнительные сведения об этих свойствах см. в подразделе «Преобразование "Нечеткий уточняющий запрос"» раздела [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Дополнительные сведения о преобразовании «Нечеткий уточняющий запрос» см. в разделе [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## Параметры  
 **диспетчер соединений OLE DB**  
 Выберите существующий диспетчер соединений OLE DB из списка или создайте новое подключение, выбрав пункт **Создать**.  
  
 **Создать**  
 Позволяет создать новое соединение с помощью диалогового окна **Настройка диспетчера соединений OLE DB**.  
  
 **Сформировать новый индекс**  
 Укажите в том случае, если преобразование должно создавать новый индекс уточняющего запроса.  
  
 **Имя ссылочной таблицы**  
 Выберите таблицу, которая будет использоваться в качестве таблицы ссылок (уточняющего запроса).  
  
 **Сохранить новый индекс**  
 Выберите этот параметр, если требуется сохранить новый индекс уточняющего запроса.  
  
 **Имя нового индекса**  
 Если выбран параметр сохранения нового индекса уточняющего запроса, введите описательное имя индекса.  
  
 **Поддерживать хранимый индекс**  
 Если выбран параметр сохранения нового индекса уточняющего запроса, укажите, должен ли [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживать этот индекс.  
  
> [!NOTE]  
>  Если выбрать параметр **Поддерживать хранимый индекс** в **редакторе преобразования «Нечеткий уточняющий запрос»** на вкладке **Ссылочная таблица**, представление будет поддерживать хранимый индекс с помощью управляемых хранимых процедур. Эти управляемые хранимые процедуры используют функцию интеграции со средой CLR, доступную в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. По умолчанию в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] отключена интеграция со средой CLR. Чтобы использовать функцию **Поддерживать хранимый индекс** , необходимо включить интеграцию со средой CLR. Дополнительные сведения см. в статье [Enabling CLR Integration](../Topic/Enabling%20CLR%20Integration.md).  
>   
>  Поскольку для параметра **Поддерживать хранимый индекс** необходима интеграция со средой CLR, эта функция работает, только если ссылочная таблица выбрана на экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на котором включена интеграция со средой CLR.  
  
 **Использовать существующий индекс**  
 Выберите, если преобразование будет использовать для уточняющего запроса существующий индекс.  
  
 **Имя существующего индекса**  
 Выберите из списка ранее созданный индекс уточняющего запроса.  
  
## См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Столбцы")](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Дополнительно")](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  