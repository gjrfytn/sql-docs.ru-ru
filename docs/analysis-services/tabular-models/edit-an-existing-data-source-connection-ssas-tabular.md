---
title: "Изменение существующего соединения с источником данных (табличные службы SSAS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.selexistconn.f1"
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# Изменение существующего соединения с источником данных (табличные службы SSAS)
  В этом разделе описано изменение свойств существующего соединения с источником данных в табличной модели.  
  
 После создания соединения с внешним источником данных это соединение можно изменить несколькими способами.  
  
-   Можно изменить сведения о соединении (включая файл, канал или базу данных, которая используется как источник), его свойства или другие параметры, зависящие от поставщика.  
  
-   Можно изменять сопоставления таблиц и столбцов, а также удалять ссылки на столбцы, которые более не используются.  
  
-   Можно изменить таблицы, представления или столбцы, которые получаются из внешнего источника данных.  
  
## Изменение соединения  
 Эта процедура описывает, как изменить соединение с источником данных базы данных. Некоторые параметры для работы с источниками данных зависят от типа источника данных, однако можно легко определить эти различия.  
  
#### Изменение внешнего источника данных, который используется текущим соединением  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]в меню **Модель** выберите пункт **Существующие соединения**.  
  
2.  Выберите соединение с источником данных, которое необходимо изменить, и нажмите кнопку **Изменить**.  
  
3.  В диалоговом окне **Изменить соединение** нажмите кнопку **Обзор** , чтобы выбрать другую базу данных того же типа с другим именем или в другом расположении.  
  
     Как только происходит изменение файла базы данных, появляется сообщение о том, что необходимо сохранить и обновить таблицы для просмотра новых данных.  
  
4.  Нажмите кнопку **Сохранить**, а затем кнопку **Закрыть**.  
  
5.  В среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]выберите в меню **Модель**пункт **Обработать**, а затем **Обработать все**.  
  
     Таблицы будут повторно обработаны с использованием нового источника данных, но с первоначальным выбором данных.  
  
    > [!NOTE]  
    >  Если новый источник данных содержит дополнительные таблицы, которых не было в первоначальном источнике данных, то необходимо повторно открыть измененное соединение и добавить эти таблицы.  
  
## Изменение сопоставлений таблиц и столбцов (привязки)  
 Эта процедура описывает порядок изменения сопоставлений после изменения источника данных.  
  
#### Изменение сопоставлений столбцов после изменения источника данных  
  
1.  В конструкторе моделей выберите таблицу.  
  
2.  Выберите в меню **Таблица** пункт **Свойства таблицы**.  
  
     Имя выбранной таблицы отображается в поле **Имя таблицы** . Поле **Имя источника** содержит имя таблицы во внешнем источнике данных. Если столбцы названы по-разному в источнике и модели, можно выбрать между двумя наборами имен столбцов с помощью выбора одного из вариантов **Источник** или **Модель**.  
  
3.  Для изменения таблицы, которая используется в качестве источника данных в поле **Имя источника**, выберите другую таблицу, отличную от текущей.  
  
4.  При необходимости измените сопоставления столбцов.  
  
    1.  Чтобы добавить столбцы, которые есть в источнике, но отсутствуют в модели, установите флажок рядом с именем столбца.  
  
         Фактические данные будут загружены в модель при следующем обновлении.  
  
    2.  Если некоторые столбцы в модели больше недоступны в текущем источнике данных, в области уведомлений появляется сообщение, в котором перечисляются недопустимые столбцы. Другие действия не требуются.  
  
5.  Чтобы применить изменения к модели, нажмите кнопку **Сохранить** .  
  
     При сохранении текущего набора свойств таблицы может появиться сообщение, указывающее на необходимость обработки таблиц. Чтобы загрузить обновленные данные в модель, нажмите кнопку **Обработать** .  
  
## См. также  
 [Обработка данных (табличные службы SSAS)](../../analysis-services/tabular-models/process-data-ssas-tabular.md)   
 [Поддерживаемые источники данных (табличные службы SSAS)](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  