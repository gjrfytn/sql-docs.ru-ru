---
title: Задание изображения для указателя на датчике (построитель отчетов и службы SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1929ed08c53d0ec1b979c26ba3a885d9623b4486
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285712"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>Задание изображения для указателя на датчике (построитель отчетов и службы SSRS)
  Датчик содержит три встроенных стиля, которые используются для настройки внешнего вида указателя. Для радиальных датчиков существуют следующие стили: стрелка, маркер и черта. Для линейных датчиков существуют следующие стили: маркер, черта и термометр. Если пользователю требуется особый указатель, он может создать и задать изображение, которое будет использоваться в качестве полностью функционального указателя.  
  
 При указании изображения для указателя оно должно отвечать следующим требованиям.  
  
-   Исходная точка указателя, или центр вращения, должна находиться наверху изображения.  
  
-   Конечная точка указателя должна показывать вниз.  
  
 Поскольку указатель имеет неправильную форму, необходимо задать цвет прозрачности, чтобы скрыть ненужные части изображения. Рекомендуется применять тот цвет прозрачности, который не будет отображаться на датчике, поскольку заданный цвет не появится на датчике.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>Установка изображения в качестве указателя датчика  
  
1.  В режиме конструктора щелкните указатель датчика.  
  
2.  (Необязательно) Если в датчике нет указателя, щелкните правой кнопкой мыши датчика и выберите **добавить указатель**. К датчику добавится указатель.  
  
3.  Нажмите кнопку **вставить** вкладке на ленте и дважды щелкните значок с изображением. Откроется диалоговое окно **Свойства изображения**.  
  
4.  Добавьте изображение к отчету. Дополнительные сведения см. в разделе [внедрение изображения в отчете &#40;построитель отчетов и службы SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Откройте панель «Свойства».  
  
6.  Щелкните указатель в области конструктора. На панели «Свойства» отобразятся свойства указателя.  
  
7.  Разверните узел PointerImage.  
  
8.  В **источника**выберите **внедренное** из раскрывающегося списка.  
  
    > [!NOTE]  
    >  Если изображение хранится в базе данных или в Интернете, для этого свойства можно задать соответствующий параметр. Дополнительные сведения см. в разделе [диалоговое окно «Свойства изображения» — Общие &#40;построитель отчетов и службы SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. В **значение**, выберите имя образа из раскрывающегося списка.  
  
10. В **цвет прозрачности**, выберите значение цвета, который требуется удалить из образа. Таким образом, создается цельное изображение указателя на датчике.  
  
## <a name="see-also"></a>См. также  
 [Форматирование указателей на датчике &#40;построитель отчетов и службы SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Добавление датчика в отчет &#40;построитель отчетов и службы SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Форматирование линий, цветов и изображений (построитель отчетов и службы SSRS)](report-design/images-report-builder-and-ssrs.md)   
 [Датчики (построитель отчетов и службы SSRS)](report-design/gauges-report-builder-and-ssrs.md)  
  
  
