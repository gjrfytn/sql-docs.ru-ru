---
title: Установка служб Analysis Services в табличном режиме | Документация Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8690c252ddb1b91cd939044ee4f0ccc3a6f4a60
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214654"
---
# <a name="install-analysis-services-in-tabular-mode"></a>Установка служб Analysis Services в табличном режиме
  Если службы Analysis Services устанавливаются для использования новых функций табличных моделей, необходимо устанавливать их в серверном режиме с поддержкой соответствующего типа модели. Серверный режим — табличный, он настраивается во время установки.  
  
 После установки сервера в этом режиме можно использовать его для размещения решений, создаваемых в конструкторе табличных моделей. Сервер в табличном режиме необходим, если требуется сетевой доступ к данным табличной модели.  
  
 Табличный режим можно задать в мастере установки или в программе установки из командой строки. В приведенных ниже разделах описан каждый из этих способов.  
  
## <a name="installation-wizard"></a>Мастер установки  
 В следующем списке приведены страницы в мастере установки SQL Server, используемые при установке служб Analysis Services в табличном режиме.  
  
1.  Выберите **Службы Analysis Services** в дереве компонентов в программе установки.  
  
     ![Дерево компонентов программы установки со службами Analysis Services](../../../sql-server/install/media/ssas-setupas.gif "дерево компонентов программы установки со службами Analysis Services")  
  
2.  На странице "Настройка служб Analysis Services", не забудьте выбрать **табличном режиме**.  
  
     ![Страница установки с параметрами конфигурации служб Analysis Services](../../../sql-server/install/media/ssas-setupasconfig.gif "страница установки с параметрами конфигурации служб Analysis Services")  
  
 Табличный режим использует подсистему VertiPaq аналитики в памяти xVelocity, которая является хранилищем по умолчанию для табличных моделей, развертываемых в службах Analysis Services. После развертывания решений табличных моделей на сервере можно выборочно настроить в табличных решениях использование дискового хранилища DirectQuery в качестве альтернативы хранилищу, размещенному в оперативной памяти.  
  
## <a name="command-line-setup"></a>Установка из командной строки  
 В программе установки SQL Server предусмотрен новый параметр (`ASSERVERMODE`), указывающий режим сервера. В приведенном ниже примере показана установка служб Analysis Services в табличном режиме сервера из командной строки.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` должна быть менее 17 символов.  
  
 Все заполнители значений учетных записей должны быть заменены на действительные учетные записи и пароли.  
  
 Такие средства, как среда SQL Server Management Studio или [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], не устанавливаются при использовании приведенного примера синтаксиса командной строки. Дополнительные сведения о добавлении компонентов см. в разделе [Установка SQL Server 2014 из командной строки](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 `ASSERVERMODE` учитывается регистр.  Все значения должны задаваться в верхнем регистре. В следующей таблице приведены допустимые значения параметра `ASSERVERMODE`.  
  
|Значение|Описание|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Это значение по умолчанию. Если вы не установите `ASSERVERMODE`, сервер будет установлен в многомерном режиме сервера.|  
|POWERPIVOT|Это значение является необязательным. На практике, если задан параметр `ROLE`, то режим сервера автоматически получает значение 1, что делает `ASSERVERMODE` необязательным в установке PowerPivot для SharePoint. Дополнительные сведения см. в разделе [Установка PowerPivot из командной строки](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md).|  
|TABULAR|Это значение является обязательным при установке служб Analysis Services в табличном режиме из командной строки.|  
  
## <a name="see-also"></a>См. также  
 [Определение режима работы сервера экземпляра служб Analysis Services](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Настройте в памяти или доступа DirectQuery для базы данных табличной модели](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [Табличное моделирование &#40;табличные службы SSAS&#41;](../../tabular-models/tabular-models-ssas.md)  
  
  
