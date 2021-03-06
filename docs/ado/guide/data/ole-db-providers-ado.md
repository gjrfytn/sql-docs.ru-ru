---
title: Поставщики OLE DB (ADO) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f4f1d4efed51a8f9e3b5eaf3bd4a2c7f385e75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613812"
---
# <a name="ole-db-providers-ado"></a>Поставщики OLE DB (ADO)
OLE DB определяет набор COM-интерфейсы для предоставления приложениям стандартизированный доступ к данным, которые хранятся в различных источниках. Такой подход позволяет источнику данных для совместного использования данных через интерфейсы, поддерживающие объем архиватора соответствующие к источнику данных. По своей структуре высокопроизводительных архитектуры OLE DB основан на его использование модели гибкий, основанный на компонент службы. Вместо того, предписанное число промежуточных слоев между приложением и данных, OLE DB требуется только в том случае, как многие компоненты, которые необходимы для выполнения конкретной задачи.  
  
 Например предположим, что пользователь хочет выполнить запрос. Рассмотрим следующие сценарии.  
  
-   Данные находятся в реляционной базе данных, для которого в настоящее время существует драйвера ODBC, но нет собственного поставщика OLE DB: приложение использует ADO для взаимодействия с поставщиком OLE DB для ODBC, который затем загружает соответствующий драйвер ODBC. Драйвер передает инструкции SQL для СУБД, который извлекает данные.  
  
-   Данные находятся в Microsoft SQL Server, для которого имеется собственный поставщик OLE DB: приложение использует ADO напрямую обмениваться данными с поставщиком OLE DB для Microsoft SQL Server. Без посредников являются обязательными.  
  
-   Данные находятся в Microsoft Exchange Server, для которой имеется поставщик OLE DB, но не предоставляет механизм для процесса SQL-запросы: приложения, использующего ADO для взаимодействия с поставщиком OLE DB для Microsoft Exchange и вызывает обработчик запросов OLE DB компонент для обработки запроса.  
  
-   Данные находятся в файловой системе Microsoft NTFS в виде документов: данным осуществляется с помощью собственного поставщика OLE DB по службе индексирования, который индексирует содержимое и свойства документов в файловой системе, чтобы эффективно содержимое выполняет поиск.  
  
 В приведенных выше примерах приложение может запросить данные. Пользователя требованиям с минимальным набором компонентов. В каждом случае дополнительных компонентов используются только в том случае, если требуется, и вызываются только необходимые компоненты. Загрузка компонентов многократного использования и совместного использования этого по требованию вносит значительный вклад для высокой производительности при использовании OLE DB.  
  
 Поставщики делятся на две категории: те, предоставляющая данные и их предоставления служб. Поставщик данных владеет собственными данными и передают их в табличную форму в приложение. Поставщик услуг инкапсулирует службы, создания и использования данных, дополнение функции в приложениях ADO. Поставщик услуг можно также детализировать как компонент службы, которой необходимо работать совместно с других поставщиков служб или компонентов.  
  
 ADO предоставляет согласованный, выше уровня интерфейс для различных поставщиков OLE DB.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Поставщики данных](../../../ado/guide/data/data-providers.md)  
  
-   [Поставщики служб и компоненты](../../../ado/guide/data/service-providers-and-components.md)
