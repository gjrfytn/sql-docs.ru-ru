---
title: Диалоговое окно свойств набора данных, поля | Документация Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f4c0f4f06dd9d61b7a53b39f2ebcf3085029b233
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291862"
---
# <a name="dataset-properties-dialog-box-fields"></a>Диалоговое окно «Свойства набора данных» — «Поля»
  Чтобы изменить коллекцию полей для набора данных отчета, перейдите на вкладку **Поля** в диалоговом окне **Свойства набора данных** . Список полей формируется автоматически, но с помощью вкладки **Поля** можно добавлять, изменять и удалять поля запросов и вычисляемые поля.  
  
## <a name="options"></a>Параметры  
 **Добавить**  
 Добавляет в набор данных новое поле запроса или вычисляемое поле.  
  
 **Удаление**  
 Удалить выбранное поле из набора данных.  
  
 **Имя поля**  
 Введите имя для поля. Имя поля должно быть уникально в пределах набора данных. Имя каждого существующего поля в запросе набора данных заполняется заранее.  
  
 **Источник поля**  
 Введите значение для поля.  
  
 Для вычисляемого поля источник должен иметь имя существующего поля, возвращаемого запросом набора данных, или имя выражения, создаваемого пользователем. Например, чтобы создать поле, представляющее удесятеренное значение поля Sales в запросе, используйте выражение `=10 * Fields!Sales.Value`.  
  
 Для поля запроса источник должен иметь имя существующего поля, возвращаемого запросом набора данных.  
  
 **Выражение (fx)**  
 Добавляет или изменяет выражение для вычисляемого поля. Эта кнопка появляется, только если нажать кнопку **Добавить** и выбрать пункт **Вычисляемое поле**.  
  
## <a name="see-also"></a>См. также  
 [Коллекция полей набора данных (построитель отчетов и службы SSRS)](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Выражения (построитель отчетов и службы SSRS)](report-design/expressions-report-builder-and-ssrs.md)  
  
  
