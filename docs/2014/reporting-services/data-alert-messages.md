---
title: Предупреждающие сообщения | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e71c7e2c933afc0da1a09adbb26cc5e08bc9747f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035635"
---
# <a name="data-alert-messages"></a>Предупреждающие сообщения
  Предупреждения об изменении данных служб [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] предусматривают два типа предупреждающих сообщений, отправляемых по электронной почте. Сообщения с результатами предупреждения об изменении данных и сообщения с описанием ошибки. Сообщения с результатами информируют всех получателей об изменениях в данных отчетов, представляющих для них интерес и важных для принятия бизнес-решений. Если по какой-то причине произошла ошибка и результаты оказались недоступны, вместо сообщения с результатами будет отправлено сообщение об ошибке.  
  
 Владельцы определений предупреждений об изменении данных также могут просматривать сведения об экземплярах предупреждений об изменении данных в диспетчере предупреждения об изменении данных. Дополнительные сведения см. в статье [Data Alert Manager for SharePoint Users](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md).  
  
##  <a name="DataAlertMessages"></a> Предупреждающие сообщения  
 На изображениях ниже показаны предупреждающее сообщение с результатами и предупреждающее сообщение с описанием ошибки.  
  
 **Сообщение с результатами**  
  
 ![Сообщение электронной почты предупреждения о данных с результатами](media/rs-alertmessageresults.gif "Сообщение электронной почты предупреждения о данных с результатами")  
  
 **Сообщение об ошибке**  
  
 ![Сообщение предупреждения о данных с сообщением об ошибке](media/rs-alertmessageerrror.gif "Сообщение предупреждения о данных с сообщением об ошибке")  
  
 Эти сообщения включают в себя те же типы информации.  
  
1.  Поле**От имени** содержит имя пользователя, создавшего определение предупреждения об изменении данных.  
  
2.  Если в определении предупреждения включено описание, оно будет отображено ниже в поле **От имени**.  
  
3.  Поле**Результаты предупреждения** отображает строки в веб-канале данных, удовлетворяющие определению предупреждения, в табличном формате или отображает сообщение об ошибке. Ограничения на количество отображаемых строк не существует.  
  
4.  **Перейти к отчету** — это ссылка на отчет, на основе которого построено определение предупреждения. Если ссылка недействительна из-за того, что отчет был перемещен или удален, будет отображено сообщение об ошибке.  
  
5.  В поле**Правила** перечисляются правила и предложения из определения предупреждения. Эти сведения помогают проверить и понять результаты предупреждения и определить правила определения предупреждения об изменении данных, которые можно изменить для расширения или сужения объема возвращаемых результатов.  
  
6.  В поле**Параметры отчета** перечисляются параметры и значения параметров, используемые при запуске отчета. Параметры и значения параметров помогают понять результаты предупреждения.  
  
7.  В поле**Контекстуальные значения** перечисляются имена и значения элементов отчета, которые находятся вне областей данных отчета. Обычно элементами являются текстовые поля. Например, текстовое поле с постоянным значением — тема или описание отчета.  
  
 Единственным различием между двумя типами сообщений является элемент 5, **Результаты предупреждения**. Если при создании экземпляра предупреждения об изменении данных или предупреждающего сообщения происходит ошибка, в поле **Результаты предупреждения** отображается сообщение об ошибке, описывающее проблему. Сообщение об ошибке, отправленное всем получателям, позволяет им узнать, что ожидаемые результаты предупреждений, которые могли быть необходимы для принятия бизнес-решений, недоступны.  
  
 
  
##  <a name="HowTo"></a> Связанные задачи  
 В этом разделе перечисляются процедуры, показывающие, как можно создавать и редактировать определения предупреждений об изменении данных, предоставляющие большинство сведений, доступных в предупреждающих сообщениях.  
  
-   [Создание предупреждения данных в конструкторе предупреждений](create-a-data-alert-in-data-alert-designer.md)  
  
-   [изменить предупреждение в конструкторе предупреждений](edit-a-data-alert-in-alert-designer.md)  
  

  
## <a name="see-also"></a>См. также  
 [Конструктор предупреждений данных](../../2014/reporting-services/data-alert-designer.md)   
 [Предупреждения об изменении данных в службах Reporting Services](../ssms/agent/alerts.md)  
  
  
