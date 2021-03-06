---
title: Создать резервную копию ключа шифрования (собственный режим служб SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: db573e1a070b110ff0f5224a6d079f3fe7c377ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061694"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Резервная копия ключа шифрования (службы Reporting Services в собственном режиме)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] использует ключ шифрования для защиты конфиденциальных данных, которые хранятся в базе данных сервера отчетов. Очень важно создать резервную копию этого ключа, чтобы обеспечить непрерывный доступ к зашифрованным строкам соединения и учетным данным. Наличие резервной копии этого ключа является обязательной при смене имени пользователя или пароля в учетной записи службы сервера отчетов или при переносе его базы данных на другой компьютер. Обе операции в процессе своего выполнения потребуют восстановления ключа из ранее созданной резервной копии.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в собственном режиме.  
  
 Чтобы открыть диалоговое окно «резервное копирование ключа шифрования», нажмите кнопку **ключи шифрования** в области навигации [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, а затем щелкните **резервного копирования**. Это диалоговое окно отображается также при обновлении учетной записи службы, используя страницу учетной записи службы в [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Дополнительные сведения о [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, см. в разделе [диспетчер конфигурации служб Reporting Services &#40;собственный режим&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Параметры  
 **Расположение файла**  
 Укажите имя файла и расположение для [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] симметричного ключа. Симметричный ключ никогда не хранится в виде простого текста. Необходимо ввести пароль для защиты файла.  
  
 **Пароль**  
 Введите пароль для защиты файла от несанкционированного доступа. Только пользователи, знающие пароль, смогут восстановить ключ из этого файла. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] применяют политику надежных паролей. Пароль должен содержать не менее 8 символов, состоять из сочетания прописных и строчных букв и цифр и содержать как минимум один специальный символ.  
  
 **Подтвердите пароль**  
 Еще раз введите тот же пароль.  
  
## <a name="see-also"></a>См. также  
 [Разделы справки F1 диспетчера конфигурации служб Reporting Services &#40;собственный режим служб SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Резервное копирование и восстановление ключей шифрования служб Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Удаление и повторное создание ключей шифрования (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Инициализация сервера отчетов &#40;диспетчер конфигурации служб SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Хранение зашифрованных данных сервера отчетов &#40;диспетчер конфигурации служб SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Ключи шифрования &#40;собственный режим служб SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
