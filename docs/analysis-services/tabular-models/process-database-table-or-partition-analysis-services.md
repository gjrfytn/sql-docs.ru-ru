---
title: Обработка базы данных, таблицы или секции (службы Analysis Services) | Документы Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3fbaa230d4db635b5c3f6c232fa50ae0cf88aec1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044018"
---
# <a name="process-database-table-or-partition-analysis-services"></a>Обработка базы данных, таблицы или секции (службы Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  В этом разделе описывается, как обработка базы данных табличной модели, таблицы или секций вручную с помощью **процесс \<объекта >** диалоговое окно в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Дополнительные сведения об обработке табличной модели см. в разделе [обработки данных](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_process_tasks"></a> Задания  
  
###  <a name="bkmk_process_db"></a> Обработка базы данных  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]щелкните правой кнопкой мыши базу данных, которую необходимо обработать, и выберите команду **Обработать базу данных**.  
  
2.  В диалоговом окне **Обработка базы данных** выберите один из следующих режимов обработки из списка **Режим** :  
  
    |Режим|Description|  
    |----------|-----------------|  
    |**Обработка. По умолчанию**|Определяет состояние обработки объектов баз данных и выполняет обработку, необходимую для преобразования необработанных или частично обработанных объектов в полностью обработанное состояние. Выполняется загрузка данных для пустых таблиц и секций; иерархии, вычисляемые столбцы и связи строятся или перестраиваются (повторно вычисляются).|  
    |**Обработка. Полная**|Обрабатывает базу данных и все объекты, которые в ней содержатся. Если объект, который обрабатывается методом полной обработки, уже был обработан, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] удаляют все данные объекта, а затем обрабатывают его. Этот тип обработки требуется при внесении структурных изменений в объект. Этот вариант требует больше всего ресурсов.|  
    |**Обработка с очисткой**|Удаляет все данные из объектов базы данных.|  
    |**Обработка с повторным вычислением**|Обновляет и повторно вычисляет иерархии, связи и вычисляемые столбцы.|  
  
3.  В столбце флажков **Обработка** выберите секции для обработки в текущем режиме и нажмите кнопку **ОК**.  
  
###  <a name="bkmk_process_table"></a> Обработка таблицы  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]в базе данных табличной модели, которая содержит обрабатываемую таблицу, разверните узел **Таблицы** , затем щелкните правой кнопкой мыши таблицу, которую необходимо обработать, и выберите команду **Обработать таблицу**.  
  
2.  В диалоговом окне **Обработка таблицы** выберите один из следующих режимов обработки из списка **Режим** :  
  
    |Режим|Description|  
    |----------|-----------------|  
    |**Обработка. По умолчанию**|Определяет состояние обработки объекта таблицы и выполняет обработку, необходимую для того, чтобы преобразовать необработанные или частично обработанные объекты в полностью обработанное состояние. Выполняется загрузка данных для пустых таблиц и секций; иерархии, вычисляемые столбцы и связи строятся или перестраиваются (повторно вычисляются).|  
    |**Обработка. Полная**|Обрабатывает объект таблицы и все объекты, которые в нем содержатся. Если объект, который обрабатывается методом полной обработки, уже был обработан, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] удаляют все данные объекта, а затем обрабатывают его. Этот тип обработки требуется при внесении структурных изменений в объект. Этот вариант требует больше всего ресурсов.|  
    |**Обработка данных**|Выполняется загрузка данных в таблицу без перестроения иерархий или связей и без повторного вычисления вычисляемых столбцов и мер.|  
    |**Обработка с очисткой**|Удаляет все данные из таблицы и ее секций.|  
    |**Обработка с дефрагментацией**|Дефрагментирует индексы вспомогательных таблиц.|  
  
3.  В столбце флажков таблицы проверьте таблицу и при необходимости выберите дополнительные таблицы, которые необходимо обработать, после чего нажмите кнопку **ОК**.  
  
###  <a name="bkmk_process_partition"></a> Обработка одной или нескольких секций  
  
1.  В [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]щелкните правой кнопкой мыши таблицу, в которой есть секции для обработки, и выберите пункт **Секции**.  
  
2.  В диалоговом окне **Секции** на вкладке **Секции**нажмите кнопку «Обработать».  
  
3.  В диалоговом окне **Обработка секции** выберите один из следующих режимов обработки из списка **Режим** :  
  
    |Режим|Description|  
    |----------|-----------------|  
    |**Обработка. По умолчанию**|Обнаруживает состояние обработки объекта секции и выполняет обработку, необходимую для перевода необработанных или частично обработанных объектов секции в полностью обработанное состояние. Выполняется загрузка данных для пустых таблиц и секций; иерархии, вычисляемые столбцы и связи строятся или перестраиваются (повторно вычисляются).|  
    |**Обработка. Полная**|Обрабатывает объект секций и все объекты, которые в нем содержатся. Если объект, который обрабатывается методом полной обработки, уже был обработан, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] удаляют все данные объекта, а затем обрабатывают его. Этот тип обработки требуется при внесении структурных изменений в объект.|  
    |**Обработка данных**|Выполняется загрузка данных в секцию или таблицу без перестроения иерархий или связей или повторного вычисления вычисленных столбцов и мер.|  
    |**Обработка с очисткой**|Удаляет все данные из секции.|  
    |**Обработка с добавлением**|Постепенно обновляет секцию с включением новых данных.|  
  
4.  В столбце флажков **Обработка** выберите секции для обработки в текущем режиме и нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также  
 [Секции табличных моделей](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Создание секций табличной модели и управление ими](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
