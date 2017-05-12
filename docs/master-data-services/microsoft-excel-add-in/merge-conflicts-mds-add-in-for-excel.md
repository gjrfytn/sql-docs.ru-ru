---
title: "Слияние конфликтов (надстройка MDS для Excel) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Слияние конфликтов (надстройка MDS для Excel)
  В надстройке [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] для Excel попытка публикации данных, измененных на сервере другим пользователем, завершится ошибкой из-за конфликта. Чтобы устранить эту ошибку, можно выполнить слияние конфликтов и повторно опубликовать изменения.  
  
## Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   Необходимо иметь разрешение на доступ к функциональной области **Обозреватель** .  
  
-   Как минимум, необходимо разрешение на обновление для конечного объекта модели для сущности, которую нужно обновить.  
  
-   Необходимо наличие данных, управляемых MDS, на активном листе в Excel.  
  
-   На активном листе должна возникнуть ошибка конфликта после попытки публикации изменений.  
  
### Слияние конфликтов  
  
1.  На листе выберите строку или ячейку, содержащую ошибку конфликта.  
  
2.  В группе меню **Опубликовать и проверить** выберите пункт **Объединить конфликты**, чтобы открыть диалоговое окно **Объединить конфликты**.  
  
3.  В диалоговом окне **Объединить конфликты** можно выполнить одно из указанных ниже действий.  
  
    -   Выберите **Последний** и нажмите кнопку **Применить**, чтобы отменить ожидающие изменения и повторно загрузить последнюю версию с сервера.  
  
    -   Выберите **Исходный** и нажмите кнопку **Применить**, чтобы применить исходную версию на листе.  
  
    -   Выберите **Ваш** и нажмите кнопку **Применить**, чтобы сохранить существующие локальные изменения.  
  
4.  Нажав кнопку **Применить**, можно внести дополнительные изменения и опубликовать данные снова. Можно также нажать кнопку **Отменить**, чтобы отменить обновление и повторно загрузить последнюю версию с сервера.  
  
## См. также:  
 [Обзор импорта данных из Excel (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  