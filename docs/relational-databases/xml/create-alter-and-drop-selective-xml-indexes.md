---
title: "Создание, изменение и удаление селективных XML-индексов | Документация Майкрософт"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cff16890d58c610a08e7bbe0d5958de2e821b0a5
ms.lasthandoff: 04/11/2017

---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>Создание, изменение и удаление селективных XML-индексов
  Описывает способы создания нового селективного XML-индекса, изменения или удаления существующего селективного XML-индекса.  
  
 Дополнительные сведения о селективных XML-индексах см. в разделе [Выборочный XML-индекс (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
##  <a name="create"></a> Создание селективного XML-индекса  
  
### <a name="how-to-create-a-selective-xml-index"></a>Инструкции. Создание селективного XML-индекса  
 **Создание нового селективного XML-индекса с помощью Transact-SQL**  
 Создание селективного XML-индекса путем вызова инструкции CREATE SELECTIVE XML INDEX. Дополнительные сведения см. в разделе [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
 **Пример**  
  
 В следующем примере показан синтаксис для создания селективного XML-индекса. Он также содержит несколько вариантов синтаксиса для описания индексируемых путей с указаниями по оптимизации.  
  
```tsql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
##  <a name="alter"></a> Изменение селективного XML-индекса  
  
### <a name="how-to-alter-a-selective-xml-index"></a>Инструкции. Изменение селективного XML-индекса  
 **изменить селективный XML-индекс с помощью Transact-SQL**  
 Измените существующий селективный XML-индекс с помощью инструкции ALTER INDEX. Дополнительные сведения см. в разделе [ALTER INDEX (селективные XML-индексы)](../../t-sql/statements/alter-index-selective-xml-indexes.md).  
  
 **Пример**  
  
 В следующем примере показана инструкция ALTER INDEX. Эта инструкция добавляет путь `'/a/b/m'` в часть XQuery индекса и удаляет путь `'/a/b/e'` из части SQL индекса, созданного в примере в разделе [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md). Путь для удаления определяется по имени, указанному при его создании.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
##  <a name="drop"></a> Удаление селективного XML-индекса  
  
### <a name="how-to-drop-a-selective-xml-index"></a>Инструкции. Удаление селективного XML-индекса  
 **Удаление селективного XML-индекса с помощью Transact-SQL**  
 Удалите селективный XML-индекс с помощью инструкции DROP INDEX. Дополнительные сведения см. в разделе [DROP INDEX (селективные XML-индексы)](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Пример**  
  
 В следующем примере показана инструкция DROP INDEX.  
  
```tsql  
DROP INDEX sxi_index ON tbl  
```  
  
  
  