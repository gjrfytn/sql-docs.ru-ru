---
title: Добавление заметки для транзакции (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0f5de1290998e6129e94bc849278554121ed8a9e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229324"
---
# <a name="annotate-a-transaction-master-data-services"></a>Добавление заметки для транзакции (Master Data Services)
  Службы [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]позволяют добавить к транзакции заметку, если необходимо предоставление дополнительных сведений о транзакции для архивных целей.  
  
> [!NOTE]  
>  Заметки нельзя удалить.  
  
## <a name="prerequisites"></a>предварительные требования  
  
-   Для добавления заметок к созданным транзакциям необходимы права на доступ к функциональной области **Браузер** и как минимум разрешение **Обновление** на объект модели, к которому добавляется заметка.  
  
-   Чтобы снабдить заметками транзакции всех пользователей, необходимо иметь разрешение на доступ к функциональной области **Управление версиями** и являться администратором модели. Дополнительные сведения см. в статье [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>Добавление заметки к транзакции в браузере  
  
1.  На домашней странице [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] выберите модель в списке **Модель** .  
  
2.  Выберите версию из списка **Версия** .  
  
3.  Нажмите кнопку **Браузер**.  
  
4.  На панели меню наведите указатель на пункт **Сущности** и выберите сущность, содержащую элемент с транзакцией, к которой необходимо добавить заметку.  
  
5.  На сетке щелкните строку элемента.  
  
6.  Нажмите кнопку **Просмотреть транзакции**.  
  
7.  В диалоговом окне **Просмотр транзакций** выберите транзакцию, к которой необходимо добавить заметку.  
  
8.  Введите заметку в поле в нижней части диалогового окна.  
  
9. Нажмите кнопку **Добавить заметку**. Заметка отображается на панели **Заметки** .  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>Добавление заметки к транзакции в управлении версиями (только администраторы)  
  
1.  На домашней странице [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] нажмите **Управление версиями**.  
  
2.  В строке меню выберите пункт **Транзакции**.  
  
3.  На панели **Транзакции** щелкните строку в сетке, соответствующую транзакции, которую необходимо снабдить заметкой.  
  
4.  На панели **Заметки транзакции** в поле **Заметка** введите заметку.  
  
5.  Нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также  
 [Заметки &#40;службы Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)   
 [Транзакции (службы Master Data Services)](../../2014/master-data-services/transactions-master-data-services.md)  
  
  