---
title: "--(Комментарий) (многомерные Выражения) | Документы Microsoft"
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
- --
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- -- (comment character)
ms.assetid: 02aec133-6809-4829-b9a2-102c376e21da
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 720b1d7c90e65dbfdd365e5cabf5368e27da7ef8
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="comment---mdx-operator-reference"></a>Комментарий - Справочник по операторам многомерных Выражений
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Обозначает текст комментариев пользователя.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Параметры  
 *Comment_Text*  
 Строка, содержащая текст комментария.  
  
## <a name="remarks"></a>Замечания  
 Комментарии могут занимать отдельную строку, добавляться в конец строк скрипта многомерных выражений или входить в инструкцию многомерных выражений. Сервер не обрабатывает комментарий.  
  
 Этот оператор используется для однострочных или вложенных комментариев. Комментарии, вставленные с помощью символов --, продолжаются до символа новой строки.  
  
 Длина комментариев не ограничена.  
  
## <a name="examples"></a>Примеры  
 В следующем примере демонстрируется использование этого оператора.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>См. также:  
 [Комментарий &#40; Многомерные Выражения &#41;](../mdx/comment-mdx.md)   
 [&#40; Комментарий &#41; &#40; Многомерные Выражения &#41;](../mdx/comment-mdx-double-slash.md)   
 [Справочник по операторам Многомерных &#40; Многомерные Выражения &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
