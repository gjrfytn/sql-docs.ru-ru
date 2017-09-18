---
title: "Изменения в поведении | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5709d3ef8d186d0dcc0fb56f27829298f74e2b0c
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="behavioral-changes"></a>Изменения поведения
Изменения поведения являются эти изменения, для которого *синтаксис* интерфейса остается тем же, но *семантику* были изменены. Прежде чем эти изменения функции, используемые в ODBC 2. *x* ведет себя иначе, чем те же функциональные возможности в ODBC 3.* x*.  
  
 Является ли приложение демонстрирует ODBC 2. *x* поведение или ODBC 3.* x* поведение определяется с помощью атрибута SQL_ATTR_ODBC_VERSION среды. Это 32-разрядное значение имеет значение SQL_OV_ODBC2 которых ODBC 2. *x* поведение и SQL_OV_ODBC3 которых ODBC 3.* x* поведение.  
  
 Атрибут SQL_ATTR_ODBC_VERSION среды устанавливается с помощью вызова **SQLSetEnvAttr**. После приложение вызывает **SQLAllocHandle** выделить дескриптор среды, необходимо вызвать**SQLSetEnvAttr** немедленно, чтобы задать поведение, он демонстрирует. (В результате не существует в новой среде состояние для описания дескриптора среды в выделенного, но versionless, состояние.) Дополнительные сведения см. в разделе [приложение б: ODBC состояния перехода таблицы](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Приложение указано, какое поведение, он демонстрирует атрибутом SQL_ATTR_ODBC_VERSION среды, но атрибут не оказывает влияния на подключение приложения ODBC 2. *x* или ODBC 3.* x* драйвера. ODBC 3. *x* приложение может подключаться к либо ODBC 2.* x* или 3.* x* драйвера, независимо от того, какой параметр атрибута среды.  
  
 ODBC 3. *x* приложения никогда не должен вызывать **SQLAllocEnv**. В результате, если диспетчер драйверов получает вызов **SQLAllocEnv**, он распознает, что приложение ODBC 2.* x* приложения.  
  
 Атрибут SQL_ATTR_ODBC_VERSION влияет на трех различных аспектов ODBC 3. *x* поведение драйвера:  
  
-   атрибуты SQLSTATE  
  
-   Типы данных для даты, времени и отметок времени  
  
-   *CatalogName* аргумент в **SQLTables** принимает шаблонов поиска в ODBC 3.* x*, но не в ODBC 2.* x*  
  
 Не влияет на параметр атрибута среды SQL_ATTR_ODBC_VERSION **SQLSetParam** или **SQLBindParam**. **SQLColAttribute** также не влияет на этот бит. Несмотря на то что **SQLColAttribute** возвращает атрибуты, которые затрагиваются по версии ODBC (тип date, точность, масштаб и длина), подобное поведение определяется по значению *FieldIdentifier*аргумент. Когда *FieldIdentifier* равен SQL_DESC_TYPE, **SQLColAttribute** возвращает ODBC 3.* x* коды для даты, времени и отметку времени; если *FieldIdentifier* равен SQL_COLUMN_TYPE, **SQLColAttribute** возвращает ODBC 2.* x* коды для даты, времени и отметок времени.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Сопоставления SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Изменение типов данных даты и времени](../../../odbc/reference/develop-app/datetime-data-type-changes.md)