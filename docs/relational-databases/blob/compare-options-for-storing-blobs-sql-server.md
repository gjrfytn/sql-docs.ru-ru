---
title: "Сравнение вариантов хранения больших двоичных объектов (SQL Server) | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 98538bd77f81cd6a1f16857b70a866ee3f6d171a
ms.lasthandoff: 04/11/2017

---
# <a name="compare-options-for-storing-blobs-sql-server"></a>Сравнение параметров для хранения больших двоичных объектов (SQL Server)
  Рассматриваются и сравниваются параметры, доступные для хранения файлов и документов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="Expectations"></a> Хранение файлов в базе данных — преимущества и ожидания  
 Большая часть корпоративных данных является по своей природе неструктурированной и обычно хранится в виде файлов и документов в файловой системе. Большая часть этих данных производится, управляется и используется приложениями, осуществляющими доступ к файлам через API-интерфейсы Windows. Обычно компании хранят эти данные в файловой системе, а метаданные для них — в реляционной базе данных.  
  
 Интеграция неструктурированных данных в реляционную базу данных дает большие преимущества. К таким преимуществам относятся следующие.  
  
-   Возможности интегрированного хранения и управления данными, например резервное копирование.  
  
-   Интегрированные службы, такие как полнотекстовый поиск и семантический поиск в данных и метаданных.  
  
-   Простота администрирования и управления политиками для неструктурированных данных.  
  
 Однако в большинстве случаев нет смысла хранить такие неструктурированные данные в реляционных базах данных. До сих пор не было возможности запускать существующие приложения Windows поверх реляционных систем. Переписывать работающие приложения (Microsoft Word, Adobe Reader и т. д.) для обеспечения возможности работать поверх API-интерфейсов реляционной базы данных непрактично. Этим приложениям просто нужно, чтобы данные были доступны через API-интерфейсы Windows. Иными словами, имеются следующие ожидания.  
  
-   Приложения Windows не поддерживают транзакции в базах данных и не требуют их.  
  
-   Приложения Windows требуют совместимости с API-интерфейсами файловой системы для данных из файлов и каталогов.  
  
##  <a name="Filestream"></a> FILESTREAM  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] уже имеется функция FILESTREAM, обеспечивающая эффективное хранение, управление и потоковую передачу неструктурированных данных, хранящихся в виде файлов в файловой системе. Тем не менее для решения FILESTREAM требуется дополнительное программирование, оно не удовлетворяет требованиям полной совместимости с приложениями Windows, описанным выше.  
  
##  <a name="FileTables"></a> Таблицы FileTable  
 Функция FileTable строится поверх существующих возможностей FILESTREAM, позволяя корпоративным клиентам хранить неструктурированные данные файлов и иерархии папок в базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , и выполняет требования по доступу к данным без транзакций и совместимости приложений Windows с данными, хранящимися в файлах.  
  
##  <a name="CompareFileTable"></a> Сравнение FILESTREAM и таблиц FileTable  
  
|Компонент|Файловый сервер и решение для базы данных|Решение FILESTREAM|Решение FileTable|  
|-------------|---------------------------------------|-------------------------|------------------------|  
|**Одно решение для задач управления**|Нет|Да|**Да**|  
|**Один набор служб**: поиск, отчеты, запросы и т. д.|Нет|Да|**Да**|  
|**Интегрированная модель безопасности**|Нет|Да|**Да**|  
|**Обновление на месте для данных FILESTREAM**|Да|Нет|**Да**|  
|**Иерархия каталогов и файлов сохраняется в базе данных**|Нет|Нет|**Да**|  
|**Совместимость с приложениями Windows**|Да|Нет|**Да**|  
|**Реляционный доступ к атрибутам файлов**|Нет|Нет|**Да**|  
  
##  <a name="CompareRBS"></a> Сравнение FILESTREAM и удаленного хранилища больших двоичных объектов (RBS)  
 Сравнение этих двух средств см. в статье в блоге группы RBS: [SQL Server Remote BLOB Store and FILESTREAM feature comparison](http://go.microsoft.com/fwlink/?LinkId=210317).  
  
##  <a name="more"></a> Дополнительные сведения  
 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)  
 [FileTables (SQL Server)](../../relational-databases/blob/filetables-sql-server.md)  
 [Удаленное хранилище больших двоичных объектов (RBS) (SQL Server)](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  