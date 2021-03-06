---
title: Параметры (преобразование) (AccessToSQL) проекта | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2489442eb8de9d8d0ebfb5d8ed902dd2792e22f2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675603"
---
# <a name="project-settings-conversion-accesstosql"></a>Параметры проекта (преобразование) (AccessToSQL)
Параметры проекта преобразования позволяют настроить, как объекты преобразуются из объектов базы данных Access для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или объекты базы данных SQL Azure.  
  
Область преобразования доступна в **параметры проекта** и **параметры проекта по умолчанию** диалоговым окнам.  
  
-   Используйте **параметры проекта** диалоговое окно, чтобы задать параметры конфигурации для текущего проекта. Чтобы открыть параметры преобразования в **средства** меню, выберите **параметры проекта**, нажмите кнопку **Общие** в нижней части левой панели, а затем выберите  **Преобразование**.  
  
-   Используйте **параметры проекта по умолчанию** диалоговое окно, чтобы задать параметры конфигурации для всех проектов. Чтобы открыть параметры преобразования, в **средства** меню, выберите **параметры проекта по умолчанию**, выберите тип проекта миграции, для которого требуются параметры просмотра или изменения из  **Целевой версии миграции** раскрывающийся список, нажмите кнопку **Общие** в нижней части левой панели, а затем выберите **преобразования**.  
  
## <a name="options"></a>Параметры  
**Добавить первичный ключ**  
Создает новый первичный ключ в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или таблицу SQL Azure, если в таблице Access не имеет первичного ключа или уникального индекса.  
  
-   **Режим по умолчанию**: False  
  
-   **Режим оптимистичного**: False  
  
-   **Полный режим**: True  
  
При подключении к SQL Azure, это по умолчанию True. **Добавить столбцы отметок времени**  
Указывает, должен ли SSMA создавать значение метки времени, если это необходимо.  
  
-   **Режим по умолчанию**: решить, разрешить SSMA  
  
-   **Режим оптимистичного**: никогда  
  
-   **Полный режим**: решить, разрешить SSMA  
  
**Включить отчет оценки данных с помощью отчетов с оценкой преобразования**  
Оценка данных включает в отчет об оценке.  
  
-   **Режим по умолчанию**: True  
  
-   **Режим оптимистичного**: False  
  
-   **Полный режим**: True  
  
**Тип сообщения, если первичный ключ содержит столбцы со значениями NULL**  
Указывает тип сообщения (предупреждение, ошибка или ничего), в котором SSMA отображается в области вывода, если он находит первичные ключи столбцов со значением NULL.  
  
-   **Режим по умолчанию**: предупреждение  
  
-   **Режим оптимистичного**: нет сообщений  
  
-   **Полный режим**: ошибка  
  
**Тип сообщения, если внешние ключевые столбцы имеют различные размеры**  
Указывает тип сообщения (предупреждение, ошибка или ничего), в котором SSMA отображается в области вывода, если найдет неверный внешний ключ текста.  
  
-   **Режим по умолчанию**: предупреждение  
  
-   **Режим оптимистичного**: нет сообщений  
  
-   **Полный режим**: ошибка  
  
**Тип сообщения, когда столбцов типа memo индексируются**  
Указывает тип сообщения (предупреждение, ошибка или ничего), в котором SSMA отображается в области вывода, если найдет индекс, содержащий **memo** столбца.  
  
-   **Режим по умолчанию**: предупреждение  
  
-   **Режим оптимистичного**: нет сообщений  
  
-   **Полный режим**: ошибка  
  
**Предупреждать, если сложный запрос использует символ-шаблон (\&#42;)**  
Отображает предупреждение в области вывода и список ошибок, когда имя столбца в инструкции SELECT является подстановочным знаком (*).  
  
-   **Режим по умолчанию**: True  
  
-   **Режим оптимистичного**: False  
  
-   **Полный режим**: True  
  
**Предупреждать при изменении имени идентификатора**  
Отображает сообщение в отчет об оценке и в области вывода, при изменении имени идентификатора объекта с SSMA.  
  
-   **Режим по умолчанию**: True  
  
-   **Режим оптимистичного**: False  
  
-   **Полный режим**: True  
  
**Предупреждать, если будет заключаться в кавычки идентификатор**  
Отображает сообщение в отчет об оценке и в области вывода, когда имя идентификатора объекта указываются в SSMA. Заключения в кавычки идентификаторов необходим в том случае, если имя является ключевым словом или содержит специальные символы.  
  
-   **Режим по умолчанию**: True  
  
-   **Режим оптимистичного**: False  
  
-   **Полный режим**: True  
  
## <a name="see-also"></a>См. также  
[Reference(Access) интерфейса пользователя](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
