---
title: Преобразования из SQL в C | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 094a968fb48c9eabf554bfdccb89efc69e12391a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427973"
---
# <a name="conversions-from-sql-to-c"></a>Преобразования из SQL в C
  В следующей таблице приводится список вопросов, которые следует учитывать при преобразовании типов даты-времени [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в типы языка C.  
  
## <a name="conversions"></a>Преобразования  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_TYPE_DATE|OK|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|OK|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|OK|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|OK|21|16|16|  
  
## <a name="key-to-symbols"></a>Расшифровка символов  
  
|Символ|Значение|  
|------------|-------------|  
|OK|Проблемы преобразования отсутствуют.|  
|1|Применяются правила, использовавшиеся до [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|2|Начальные и конечные пробелы пропускаются.|  
|3|Выполняется синтаксический анализ строки, при котором из нее извлекается дата, время, часовой пояс или смещение часового пояса, при этом допускается точность задания долей секунды до 9 десятичных знаков. Если при анализе обнаруживается смещение часового пояса, то время преобразуется к часовому поясу клиента. При возникновении ошибки во время преобразования, то диагностики создается запись с ошибкой SQLSTATE 22018 и сообщением «Переполнение поля Datetime».|  
|4|Если значение не является действительной датой, отметкой времени или значением timestampoffset, то формируется диагностическая запись с ошибкой SQLSTATE 22018 и сообщением «Недопустимое символьное значение для спецификации приведения».|  
|5|Если значение времени не равно нулю, то создается запись диагностики с кодом SQLSTATE 01S07 и сообщением «Частичное усечение».|  
|6|Если значение не является действительным значением времени, отметкой времени или значением timestampoffset, то формируется диагностическая запись с ошибкой SQLSTATE 22018 и сообщением «Недопустимое символьное значение для спецификации приведения».|  
|7|Компонент даты не учитывается.|  
|8|Если значение долей секунды не равно нулю, то создается диагностическая запись с кодом SQLSTATE 01S07 и сообщением «Частичное усечение».|  
|9|Если значение не является действительным значением даты, времени, отметкой времени или значением timestampoffset, то формируется диагностическая запись с ошибкой SQLSTATE 22018 и сообщением «Недопустимое символьное значение для спецификации приведения».|  
|10|Если значение является действительным значением времени, то компонент даты принимает значение текущей даты на стороне клиента.|  
|11|Если значение является действительным значением даты, то для времени устанавливается значение, равное нулю.|  
|12|Создается запись диагностики с кодом SQLSTATE 07006 и сообщением «Нарушение атрибута ограниченного типа данных».|  
|13|Время установлено в нуль.|  
|14|Если буфер недостаточно велик для значения SQL_DATE_STRUCT, то формируется диагностическая запись с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона».|  
|15|Дата устанавливается равной текущей дате на стороне клиента.|  
|16|Если буфер недостаточно велик для преобразованного строкового значения, но не помещается только дробное значение секунд, то происходит усечение долей секунд и формируется диагностическая запись с ошибкой SQLSTATE 01004 и сообщением «Строковые данные, усечение справа». Если буфер недостаточно велик для помещения строкового значения без усечения компонентов даты, времени или смещения, то формируется диагностическая запись с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона». Учтите, что для значений типа timestampoffset и значений даты невозможна ошибка SQLSTATE 01004, поскольку крайняя правая часть преобразованной строки не содержит долей секунды. Поэтому при любом усечении неизбежна потеря данных.|  
|17|Если буфер недостаточно велик для значения SQL_SS_TIME2_STRUCT, то формируется диагностическая запись с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона».|  
|18|Если значение времени не равно нулю, то создается запись диагностики с кодом SQLSTATE 01S07 и сообщением «Частичное усечение».|  
|19|Если серверный тип — datetime или smalldatetime, то значение соответствует формату потока табличных данных и будет 4-байтовым значением для smalldatetime или 8-байтовым для datetime.<br /><br /> Если типом данных на стороне сервера является datetime2, то значение возвращается в виде SQL_TIMESTAMP_STRUCT. Если буфер недостаточно велик для возвращенного значения, то формируется диагностическая запись с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона».|  
|20|Время приводится к часовому поясу клиента. Если во время этого преобразования возникла ошибка, создается запись диагностики с кодом SQLSTATE 22008 и сообщением «Переполнение поля datetime».|  
|21|Если буфер недостаточно велик для значения SQL_SS_TIMESTAMPOFFSET_STRUCT, то значение возвращается в виде SQL_SS_TIMESTAMPOFFSET_STRUCT. В противном случае формируется диагностическая запись с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона».|  
|22|Это значение приводится к часовому поясу клиента до извлечения даты. Тем самым обеспечивается согласованность с другими преобразованиями с типами timestampoffset. Если во время этого преобразования возникла ошибка, создается запись диагностики с кодом SQLSTATE 22008 и сообщением «Переполнение поля datetime». В результате может быть получена дата, отличающаяся от значения, получаемого простым усечением.|  
  
 Таблица в этом разделе описывает преобразования между типами, возвращаемыми клиенту, и типами в привязке. Для выходных параметров Если серверный тип, заданный в SQLBindParameter не соответствует фактическому типу на сервере, сервер выполнит неявное преобразование и тип, возвращаемый клиенту будет совпадать с типом, заданные с помощью функции SQLBindParameter. Это может привести к непредвиденным результатам преобразования, если правила преобразования сервера отличаются от правил, приведенных в предыдущей таблице. Например, если необходима дата по умолчанию, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует не текущую дату, а 01.01.1900.  
  
## <a name="see-also"></a>См. также  
 [Дата и время улучшения &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  