---
title: "ENCRYPTBYKEY (Transact-SQL) | Документы Microsoft"
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
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 17b9b4aea4916cfb74efbead6d06c830698a4167
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Производит шифрование данных при использовании симметричного ключа.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 *key_GUID*  
 Идентификатор GUID ключа, используемый для шифрования *текстом*. **uniqueidentifier**.  
  
 "*текстом*"  
 Данные, которые шифруются ключом.  
  
 @cleartext  
 Переменная типа **nvarchar**, **char**, **varchar**, **двоичных**, **varbinary**, или **nchar** , содержащий данные, зашифрованные с помощью ключа.  
  
 *add_authenticator*  
 Указывает, будет ли средство проверки подлинности зашифровано вместе с *текстом*. При использовании структуры проверки подлинности аргумент должен иметь значение 1. **int**.  
  
 @add_authenticator  
 Указывает, будет ли средство проверки подлинности зашифровано вместе с *текстом*. При использовании структуры проверки подлинности аргумент должен иметь значение 1. **int**.  
  
 *Средство проверки подлинности*  
 Данные, на основе которых формируется структура проверки подлинности. **sysname**.  
  
 @authenticator  
 Переменная, содержащая данные, на основе которых формируется структура проверки подлинности.  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **varbinary** с максимальным размером 8 000 байт.  
  
 Возвращает значение NULL, если ключ не открыт, не существует или является устаревшим ключом RC4, а база данных не находится на уровне совместимости 110 или выше.  
  
## <a name="remarks"></a>Замечания  
 Функция EncryptByKey использует симметричный ключ. Этот ключ должен быть открыт. Если симметричный ключ уже открыт в текущем сеансе, не нужно открывать его снова в контексте запроса.  
  
 Структура проверки подлинности позволяют исключить прямую подмену зашифрованных полей. Например, рассмотрим следующую таблицу с платежной ведомостью.  
  
|ИД_сотрудника|Стандартная_должность|Базовый_оклад|  
|------------------|---------------------|---------------|  
|345|Помощник копировщика|Fskj%7^edhn00|  
|697|Финансовый директор|M0x8900f56543|  
|694|Контролер ввода данных|Cvc97824%^34f|  
  
 Не взламывая шифр, злоумышленник может получить важные сведения из контекста, в котором хранятся зашифрованные данные. Но, поскольку оплата труда финансового директора заведомо выше, чем оплата труда помощника копировщика, из этого следует, что значение, зашифрованное как «M0x8900f56543», должно быть больше, чем значение, зашифрованное как «Fskj%7^edhn00». В таком случае любой пользователь с разрешением ALTER для данной таблицы может дать помощнику копировщика повышение, заменив его данные в поле Базовый_оклад простым копированием данных из поля Базовый_оклад финансового директора. Этот прием называется прямой подменой и обходит шифрование как таковое.  
  
 Атаку методом подмены значения целиком можно предотвратить, добавив к данным перед шифрованием сведения о контексте. Эти сведения будут использоваться для гарантии того, что открытый текст не был перенесен с другого места.  
  
 Если при шифровании данных указана структура проверки подлинности, то для дешифровки данных функцией DecryptByKey потребуются эти же данная структура проверки подлинности. При шифровании хэш данных проверки подлинности шифруется вместе с данными. При дешифровке эта же структура проверки подлинности должны быть переданы функции DecryptByKey. Если эти данные не совпадают, дешифровка завершится ошибкой. Это будет означать, что значение перемещено с другого места со времени шифрования. В качестве структуры проверки подлинности рекомендуется использовать столбец, содержащий уникальное и неизменное значение. Если значение структуры проверки подлинности изменится, можно утратить доступ к данным.  
  
 Симметричное кодирование и декодирование осуществляется относительно быстро и подходит для работы с большими объемами данных.  
  
> [!IMPORTANT]  
>  Использование функций шифрования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] совместно с параметром ANSI_PADDING OFF может привести к потере данных из-за неявных преобразований. Дополнительные сведения о параметре ANSI_PADDING см. в разделе [SET ANSI_PADDING &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
## <a name="examples"></a>Примеры  
 Возможности, продемонстрированные в следующих примерах работают с ключами и сертификатами, созданными в [How To: шифрование столбца данных](../../relational-databases/security/encryption/encrypt-a-column-of-data.md).  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. Шифрование строки симметричным ключом  
 Следующий пример показывает, как добавить столбец к таблице `Employee`, а затем зашифровать значение номера социального страхования, который хранится в столбце `NationalIDNumber`.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>Б. Шифрование записи вместе со значением проверки подлинности  
  
```  
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard.   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES &#40; Transact-SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  