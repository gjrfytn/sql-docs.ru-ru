---
title: Редактор задачи очереди сообщений (страница "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7668cf38f01f049b95423547430e1027a4ab6090
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375862"
---
# <a name="message-queue-task-editor-general-page"></a>Редактор задачи «Очередь сообщений» (страница «Общие»)
   **Страница «Общие»** диалогового окна **Редактор задачи «Очередь сообщений»** позволяет задавать имя и описывать задачу «Очередь сообщений», определять формат сообщений, а также указывать, будет ли задача отправлять или получать сообщения.  
  
 Дополнительные сведения об этой задаче см. в разделе [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Параметры  
 **Название**  
 Задайте уникальное имя задаче «Очередь сообщений». Это имя используется в качестве метки для значка задачи.  
  
> [!NOTE]  
>  Имена задач в пределах пакета должны быть уникальными.  
  
 **Описание**  
 Введите описание задачи «Очередь сообщений».  
  
 **Use2000Format**  
 Укажите, нужно ли использовать формат 2000 службы очередей сообщений (MSMQ). Значение по умолчанию — `False`.  
  
 **MSMQConnection**  
 Выберите существующий диспетчер подключений MSMQ или щелкните \<**Создать соединение...**>, чтобы создать диспетчер.  
  
 **См. также**: [Диспетчер соединений MSMQ](connection-manager/msmq-connection-manager.md), [редактор диспетчера соединений MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)  
  
 **Сообщение**  
 Указывает, будет ли задача «Очередь сообщений» отправлять или получать сообщения. При выборе режима **Отправить сообщение**на левой панели диалогового окна появляется страница «Отправка», при выборе режима **Получить сообщение**появляется страница «Получение». По умолчанию, устанавливается режим **Отправить сообщение**.  
  
## <a name="see-also"></a>См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Редактор задачи "Очередь сообщений" (страница "Получение")](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Редактор задачи "Очередь сообщений" (страница "Отправка")](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [Страница «Выражения»](expressions/expressions-page.md)  
  
  
