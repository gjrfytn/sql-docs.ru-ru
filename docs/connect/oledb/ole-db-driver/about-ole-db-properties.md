---
title: О свойствах OLE DB | Документы Microsoft
description: О свойствах OLE DB
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 038b9571202e6d01a17fbabbdb8c599823e9020f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2018
---
# <a name="about-ole-db-properties"></a>О свойствах OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Потребитель может устанавливать значения свойств, чтобы запросить определенное поведение объекта. Например, потребитель использует свойства для указания интерфейса, который должен предоставить набор строк. Потребители получают значения свойств для определения возможностей объекта, например набора строк, сеанса или объекта источника данных.  
  
 Каждое свойство имеет значение, тип, описание и атрибут чтения/записи, а для свойств набора строк — признак того, применим ли набор строк к отдельным столбцам.  
  
 Свойство определяется по идентификатору GUID и целому числу, представляющему идентификатор свойства. Набор свойств — это набор всех свойств с одинаковым идентификатором GUID. Помимо стандартных наборов свойств OLE DB драйвер OLE DB для SQL Server реализует наборы свойств от поставщика и свойства в них. Каждое свойство принадлежит одной или нескольким группам свойств. Группа свойств — это группа всех свойств, применимых к определенному объекту. Группой свойств может быть группа свойств инициализации, группа свойств источника данных, группа свойств сеанса, группа свойств набора строк, группа свойств таблицы и группа свойств столбца. Ниже представлены свойства каждой из этих групп свойств.  
  
 Установка значения свойства предполагает следующее.  
  
1.  Определения свойств, которым присваиваются значения.  
  
2.  Определение набора свойств, содержащего идентифицированные свойства.  
  
3.  Выделение ресурсов для массива структур DBPROPSET — по одной на каждый идентифицированный набор свойств.  
  
4.  Выделение ресурсов для массива структур DBPROP для каждого набора свойств. Количество элементов в каждом массиве определяется числом свойств (идентифицированных на шаге 1), принадлежащих конкретному набору свойств.  
  
5.  Заполнение структуры DBPROP для каждого свойства.  
  
6.  Заполнение сведений (идентификатор GUID, счетчик числа элементов и указатель на соответствующий массив DBPROP) в структуре DBPROPSET для каждого набора свойств.  
  
7.  Вызов метода для установки свойств и передачи счетчика и массива структур DBPROPSET.  
  
## <a name="see-also"></a>См. также  
 [Создание драйвером OLE DB для приложения SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Свойства (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=112207)  
  
  