---
title: Просмотр хранимой коллекции схем XML | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- schema collections [SQL Server], viewing
- XML schemas [SQL Server], viewing
- CREATE XML SCHEMA COLLECTION statement
- xml_schema_namespace function
- XML schema collections [SQL Server], viewing
- displaying XML schema collections
- viewing XML schema collections
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1560eb844657d806862d6a4e85bb9a52682b77d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301791"
---
# <a name="view-a-stored-xml-schema-collection"></a>Просмотр хранимой коллекции схем XML
  После импорта коллекции XML-схем с помощью команды [Создать коллекцию схем XML](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)компоненты схемы будут храниться в метаданных. Можно использовать внутреннюю функцию [xml_schema_namespace](/sql/t-sql/xml/xml-schema-namespace), чтобы повторно построить коллекцию XML-схем. Эта функция возвращает `xml` экземпляр типа данных.  
  
 Например, следующий запрос извлекает коллекцию XML-схем (`ProductDescriptionSchemaCollection`) в реляционной схеме продукции в базе данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 Если вы хотите увидеть только одну схему из коллекции схем XML, можно указать на языке XQuery `xml` результата, возвращенного типа `xml_schema_namespace`.  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 Например, следующий запрос находит сведения об XML-схеме поддержки и гарантий на продукт в коллекции XML-схем `ProductDescriptionSchemaCollection` .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 Также можно передать в качестве необязательного третьего параметра для `xml_schema_namespace` целевое пространство имен, чтобы получить из коллекции конкретную схему, как показано в следующем запросе:  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 Когда в базе данных создается коллекция XML-схем с помощью инструкции CREATE XML SCHEMA COLLECTION, она сохраняет компоненты схемы в метаданных. Обратите внимание, что сохраняются только те компоненты схемы, которые понимает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Любые комментарии, заметки или несоответствующие XSD-схеме атрибуты не сохраняются. Следовательно, схема, повторно сконструированная посредством функции **xml_schema_namespace** , функционально эквивалентна первоначальной схеме, но не обязательно будет выглядеть так же. Например, не будет тех же префиксов, которые были в первоначальной схеме. Схема, возвращаемая функцией **xml_schema_namespace** , использует префикс **t** для целевого пространства имен и префиксы **ns1**, **ns2**и так далее для всех остальных.  
  
 Если нужно сохранить точную копию XML-схем, следует сохранить схему в файл или в таблицу базы данных в столбец типа `xml`.  
  
 Представление каталога [sys.xml_schema_collections](/sql/relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql) также возвращает сведения о коллекциях XML-схем. Сюда входят, например сведения об имени коллекции, дате создания и владельце коллекции.  
  
## <a name="see-also"></a>См. также  
 [Коллекции XML-схем (SQL Server)](xml-schema-collections-sql-server.md)  
  
  