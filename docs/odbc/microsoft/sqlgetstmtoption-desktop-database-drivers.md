---
title: "SQLGetStmtOption (для настольных баз данных драйверы) | Документы Microsoft"
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
- SQLGetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: f9ed31af-2fa9-4a0c-9639-08b63199b092
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b39d5b3971d316e65e21a86f76c1dcf5338d9b46
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetstmtoption-desktop-database-drivers"></a>SQLGetStmtOption (драйверы для настольных баз данных)
Закладки, возвращенных *fOption* из SQL_GETBOOKMARK допустимы только при открытом запроса, а также становятся недействительными, при повторной выдаче запроса. Постоянные закладки не поддерживаются.