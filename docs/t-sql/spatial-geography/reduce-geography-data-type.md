---
title: "Уменьшить (тип данных geography) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5b174f3f4b8daf99c402b110ba10d95345783d7
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geography-data-type-"></a>Reduce (тип данных geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает приближение заданного **geography** экземпляра, полученное путем выполнения алгоритма Дугласа-Пекера для экземпляра с заданным допуском.  
  
 Это **geography** поддерживает метод тип **FullGlobe** экземпляры или Пространственные экземпляры, размер которых превышает полусферу.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Аргументы  
  
|||  
|-|-|  
|Термин|Определение|  
|*отказоустойчивость*|Значение типа **float**. *Отклонение* представляет собой допуск, передаваемую в алгоритм Дугласа-Пекера. *Отклонение* должно быть положительным числом.|  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Тип возвращаемого значения: **geography**  
  
 Возвращаемый тип CLR: **SqlGeography**  
  
## <a name="remarks"></a>Замечания  
 Для типов коллекции этот алгоритм работает независимо для каждого **geography** содержащиеся в экземпляре. Этот алгоритм не изменяет **точки** экземпляров.  
  
 Этот метод выполнит попытку сохранения конечных точек **LineString** экземпляров, но не сможет сделать это для сохранения действительного результата.  
  
 Если `Reduce()` вызывается с отрицательным значением, то будет вызвано **ArgumentException**. Отклонения, используемые в функции `Reduce()`, должны быть положительными.  
  
 Применяется алгоритм Дугласа-Пекера для каждой кривой или кольца в **geography** экземпляра путем удаления всех точек, за исключением начальной и конечной точки. Каждая удаленная точка затем добавляется обратно, начиная с самой удаленной точки, пока не останется точек более чем *отклонения* из результата. После этого результат преобразуется в допустимый при необходимости, поскольку гарантируется получение допустимого результата.  
  
 В [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], этот метод расширен для **FullGlobe** экземпляров.  
  
 Этот метод не является точным.  
  
## <a name="examples"></a>Примеры  
 В следующем примере создается экземпляр `LineString` и используется метод `Reduce()` для упрощения этого экземпляра.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>См. также:  
 [Расширенные методы в экземплярах географических объектов](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  