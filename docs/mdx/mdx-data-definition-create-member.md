---
title: "Инструкция CREATE MEMBER (многомерные Выражения) | Документы Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MEMBER
- CREATE MEMBER
- Member
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CREATE MEMBER statement
- calculated members [MDX]
ms.assetid: 49379217-be2c-4139-a206-1168078b9b76
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6f3a183648dca9be0962559d15e2e5619480d930
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-member"></a>Определения данных многомерных Выражений — создать элемент
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает вычисляемый элемент.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Аргументы  
 *Cube_Name*  
 Допустимое строковое выражение, содержащее имя куба, в котором будет создан элемент.  
  
 *Member_Name*  
 Допустимое строковое выражение, возвращающее имя элемента. Укажите полное имя, чтобы создать элемент в измерении, отличном от измерения мер. Если этого не сделать, элемент будет создан в измерении мер.  
  
 *MDX_Expression*  
 Допустимое многомерное выражение.  
  
 *Property_name*  
 Допустимое строковое выражение, представляющее имя свойства вычисляемого элемента.  
  
 *Property_Value*  
 Допустимое скалярное выражение, представляющее значение свойства вычисляемого элемента.  
  
## <a name="remarks"></a>Замечания  
 Инструкция CREATE MEMBER определяет вычисляемые элементы, которые доступны для всего сеанса и могут использоваться в нескольких запросах в данном сеансе. Дополнительные сведения см. в разделе [Creating Session-Scoped вычисляемые элементы &#40; Многомерные Выражения &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 Можно также определить вычисляемый элемент для использования только в одном запросе. Для определения вычисляемого элемента, ограниченного рамками одного запроса, используется предложение WITH в инструкции SELECT. Дополнительные сведения см. в разделе [слова вычисляемые элементы &#40; Многомерные Выражения &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 *Property_name* могут ссылаться на свойства либо стандартным или дополнительным вычисляемого элемента. Стандартные свойства элементов перечислены далее в этом разделе. Вычисляемые элементы, созданные инструкцией CREATE MEMBER без **СЕАНСА** имеют сеансовую область. Кроме того, строки в определениях вычисляемых элементов разделяются двойными кавычками. В OLE DB определен другой метод, указывающий, что строки должны разделяться одиночными кавычками.  
  
 При указании куба, отличного от текущего подключенного куба, возникает ошибка. Поэтому для обращения к текущему кубу вместо указания имени куба рекомендуется использовать переменную CURRENTCUBE.  
  
 Дополнительные сведения о свойствах элементов, определенных в OLE DB, см. в документации OLE DB.  
  
## <a name="scope"></a>Область действия  
 Вычисляемый элемент может встречаться в одной из областей действия, перечисленных ниже.  
  
 Область запроса  
 Видимость и время жизни этого вычисляемого элемента ограничиваются данным запросом. Вычисляемый элемент определен в одном запросе. Область запроса имеет приоритет по сравнению с областью сеанса. Дополнительные сведения см. в разделе [слова вычисляемые элементы &#40; Многомерные Выражения &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 Область сеанса  
 Видимость и время жизни этого вычисляемого элемента ограничиваются сеансом, в котором создан элемент. (Время жизни может быть меньше длительности сеанса, если по отношению к вычисляемому элементу выдана инструкция DROP MEMBER.) Инструкция CREATE MEMBER создает вычисляемый элемент с областью сеанса.  
  
### <a name="scope-isolation"></a>Изоляция на уровне области  
 Если скрипт многомерных выражений куба содержит вычисляемые элементы, то по умолчанию они вычисляются до выполнения любых вычислений области сеанса и вычислений, определенных в запросе.  
  
> [!NOTE]  
>  В некоторых сценариях [Aggregate (MDX)](../mdx/aggregate-mdx.md) функции и [VisualTotals (многомерные Выражения)](../mdx/visualtotals-mdx.md) функция режиме не работают.  
  
 Эта особенность позволяет обычным клиентским приложениям работать с кубами, которые содержат сложные вычисления, не вдаваясь в конкретную реализацию вычислений. Однако в некоторых сценариях может потребоваться выполнение сеанса или вычисляемых элементов с областью действия запроса перед определенные вычисления в кубе и ни один **статистические** функция ни **VisualTotals** функция применимы. Чтобы сделать это, воспользуйтесь свойством вычисления SCOPE_ISOLATION.  
  
#### <a name="example"></a>Пример  
 Ниже приведен пример скрипта, в котором для получения правильного результата используется свойство вычисления SCOPE_ISOLATION.  
  
 **Сценарии многомерных Выражений куба:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **Запрос многомерных Выражений:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 В результате предыдущего запроса требовалось определить долю продаж в США, без штата Вашингтон (чтобы сохранить стоимость для США без штата Вашингтон). Предыдущий запрос не вернул ожидаемого результата. Возвращенным результатом была доля США за вычетом доли штата Вашингтон, что лишено смысла. Для достижения желаемого результата можно воспользоваться свойством вычисления SCOPE_ISOLATION.  
  
 **Запрос многомерных Выражений, с помощью вычисления SCOPE_ISOLATION:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>Стандартные свойства  
 У каждого вычисляемого элемента есть набор стандартных свойств. При подключении клиентского приложения к [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], свойства по умолчанию, поддерживаемых или доступны для поддержки, администратор выбирает.  
  
 Дополнительные свойства могут быть доступны в зависимости от определения куба. Следующие свойства отражают сведения, относящиеся к уровню измерения в данном кубе.  
  
|Идентификатор свойства|Значение|  
|-------------------------|-------------|  
|SOLVE_ORDER|Порядок, в котором этот вычисляемый элемент будет вычисляться в случаях, когда один вычисляемый элемент ссылается на другой (то есть когда вычисляемые элементы пересекаются друг с другом).|  
|FORMAT_STRING|Строка форматирования [!INCLUDE[msCoName](../includes/msconame-md.md)] Office, используемая клиентским приложением для отображения значений ячеек.|  
|VISIBLE|Значение, определяющее видимость вычисляемого элемента в наборе строк схемы. Видимые вычисляемые элементы могут добавляться к набору функцией [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) функции. Ненулевое значение указывает, что данный вычисляемый элемент видим. Значение по умолчанию для этого свойства — *Visible*.<br /><br /> Невидимые вычисляемые элементы (для которых значение свойства равно нулю) обычно используются как промежуточные этапы при вычислении более сложных элементов. К таким вычисляемым элементам могут также обращаться другие типы элементов, например меры.|  
|NON_EMPTY_BEHAVIOR|Мера или набор, используемые для определения поведения вычисляемых элементов при разрешении пустых ячеек.<br /><br /> **\*\*Предупреждение \* \***  это свойство является устаревшим. Не задавайте его. Дополнительные сведения см. в разделе [Нерекомендуемые функции служб Analysis Services в SQL Server 2016](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).|  
|CAPTION|Строка, используемая клиентским приложением в качестве заголовка элемента.|  
|DISPLAY_FOLDER|Строка, определяющая путь к папке отображения, которую клиентское приложение использует для демонстрации элемента. Разделитель уровней вложенности папок определяется клиентским приложением. Для средств и клиентов, входящих в [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], обратная косая черта (\\) является разделитель уровней вложенности. Чтобы указать для определенного элемента несколько папок отображения, используйте точку с запятой (;) для разделения папок.|  
|ASSOCIATED_MEASURE_GROUP|Имя группы мер, с которой связан элемент.|  
  
## <a name="see-also"></a>См. также:  
 [Инструкция DROP MEMBER &#40; Многомерные Выражения &#41;](../mdx/mdx-data-definition-drop-member.md)   
 [Инструкция UPDATE MEMBER &#40; Многомерные Выражения &#41;](../mdx/mdx-data-definition-update-member.md)   
 [Инструкции определения данных &#40; Многомерные Выражения &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
