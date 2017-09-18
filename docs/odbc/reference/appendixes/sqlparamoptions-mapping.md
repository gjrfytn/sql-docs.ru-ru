---
title: "Сопоставление SQLParamOptions | Документы Microsoft"
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
- mapping deprecated functions [ODBC], SQLParamOptions
- SQLParamOptions function [ODBC], mapping
ms.assetid: 57ed65f6-9620-4738-b331-19d2a2b5cae4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce00768c82299f17546aac2d9c01eea32f8841f1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamoptions-mapping"></a>Сопоставление SQLParamOptions
Если приложение вызывает **SQLParamOptions** через ODBC 3*.x* драйвера, вызов  
  
```  
SQLParamOptions(hstmt, crow, piRow);  
```  
  
 будут сопоставлены с двумя вызовы **SQLSetStmtAttr** следующим образом:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, crow, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, piRow, 0);  
```