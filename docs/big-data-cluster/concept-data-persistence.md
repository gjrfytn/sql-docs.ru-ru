---
title: Сохранение данных в Kubernetes
titleSuffix: SQL Server big data clusters
description: Дополнительные сведения о работе в кластере SQL Server 2019 больших данных постоянного хранения.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f8cddaeca6c6bcc7eb32c28fa852566bb7dcf331
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860280"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Сохранение данных с кластером больших данных SQL Server в Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Постоянные тома](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) предоставляют модель подключаемого модуля для хранения в Kubernetes, где, как предоставляется хранилища завершается не зависит от его потребления. Таким образом можно использовать собственное хранилище высокой доступности и подключить его к кластеру кластера SQL Server больших данных. Это дает полный контроль над тип хранилища, доступности и производительности, которые нужны. Kubernetes поддерживает различные типы решений хранения, включая Azure диски и файлы, NFS, локальное хранилище и многое другое.

## <a name="configure-persistent-volumes"></a>Настройка постоянные тома

— Способ работы с большими данными кластера SQL Server использует эти постоянные тома с помощью [классы хранения](https://kubernetes.io/docs/concepts/storage/storage-classes/). Можно создать классы хранения для разных видов хранилища и указать их во время развертывания кластера больших данных. Вы можете настроить какой класс хранилища должен использоваться для какой цели (пул). Кластер SQL Server больших данных создает [утверждения постоянного тома](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) с именем класса указанное хранилище для каждого pod, требующий постоянные тома. Затем он подключает соответствующие постоянные тома в pod.

> [!NOTE]
> Для CTP-версии 2.4, только `ReadWriteOnce` поддерживается режим доступа для всего кластера.

## <a name="deployment-settings"></a>Параметры развертывания

Чтобы использовать постоянное хранилище во время развертывания, настройте **USE_PERSISTENT_VOLUME** и **STORAGE_CLASS_NAME** переменные среды перед запуском `mssqlctl cluster create` команды. **USE_PERSISTENT_VOLUME** присваивается `true` по умолчанию. Можно переопределить значение по умолчанию и присвойте ему значение `false` и, таким образом, большие данные кластера SQL Server использует emptyDir подключение. 

> [!WARNING]
> Работа без постоянного хранения может работать в тестовой среде, но может произойти в кластере не работает. После перезапуска pod кластера метаданных и/или пользователя данные будут утеряны окончательно.

Если пользователем задан флаг в значение true, необходимо также указать **STORAGE_CLASS_NAME** как параметр во время развертывания.

## <a name="aks-storage-classes"></a>Классы хранения в AKS

AKS поставляется с [два класса встроенного хранилища](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **по умолчанию** и **управляемых premium** вместе с динамическое средство подготовки для их. Можно указать одним из них или создать свой собственный класс хранения для развертывания кластера больших данных с помощью включено постоянное хранилище.

## <a name="minikube-storage-class"></a>Класс хранения Minikube

Minikube поставляется с встроенного хранилища класс с именем **стандартный** вместе с динамической подготовки для него. Обратите внимание, что на minikube, если `USE_PERSISTENT_VOLUME=true` (по умолчанию), необходимо также переопределить значение по умолчанию для **STORAGE_CLASS_NAME** переменной среды, так как значение по умолчанию отличается. Задайте значение `standard`: 

В Windows используйте следующую команду:

```cmd
SET STORAGE_CLASS_NAME=standard
```

В Linux используйте следующую команду:

```cmd
export STORAGE_CLASS_NAME=standard
```

Кроме того, можно отключить использование постоянных томов на minikube, установив `USE_PERSISTENT_VOLUME=false`.

## <a name="kubeadm"></a>Kubeadm

Kubeadm не поставляется с классом встроенного хранилища. Вы можете создавать собственные постоянные тома и классы хранения с помощью локального хранилища или Ваш предпочитаемый средство подготовки, например [ладья](https://github.com/rook/rook). В этом случае можно установить **STORAGE_CLASS_NAME** для класса хранения, вы настроили. Кроме того, можно задать `USE_PERSISTENT_VOLUME=false` в тестовой среде, но Обратите внимание, приведенное выше предупреждение в **параметры развертывания** этой статьи.  

## <a name="on-premises-cluster"></a>Локальный кластер

Кластеры локальных очевидно не поставляются с любого класса встроенных хранилища, поэтому необходимо настроить [постоянные тома](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[виртуальную](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/) заранее и затем используйте соответствующий классы хранения во время развертывания кластера больших данных в SQL Server.

## <a name="customize-storage-size-for-each-pool"></a>Настройка размера хранилища для каждого пула
По умолчанию размер постоянного тома, выделенные для каждого из модулей, подготовленных в кластере — 6 ГБ. Это можно настроить, задав переменную среды `STORAGE_SIZE` другое значение. Например, можно выполнить следующую команду, чтобы задать значение до 10 ГБ, перед запуском `mssqlctl cluster create --name command`.

```bash
export STORAGE_SIZE=10Gi
```

Также может иметь различные конфигурации для настройки постоянного хранилища, такие размеры постоянного тома для разных пулов в кластер и имя класса хранения. Например можно настроить постоянные тома, предоставляемым параметр ниже переменные среды перед развертыванием кластера для пула носителей, применяется другой класс хранения и пропускную способность:

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=managed-premium
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

Ниже приведен полный список переменных среды, связанных с настройкой постоянное хранилище для больших данных кластера SQL Server:

| Переменная среды | Значение по умолчанию | Описание |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` для использования утверждения постоянного тома Kubernetes для хранения pod. `false` Использование временных узлов хранилища для хранения pod. |
| **STORAGE_CLASS_NAME** | значение по умолчанию | Если `USE_PERSISTENT_VOLUME` является `true` это указывает на имя класса хранения Kubernetes для использования. |
| **STORAGE_SIZE** | 6gi | Если `USE_PERSISTENT_VOLUME` является `true`, это указывает размер постоянного тома для каждого модуля. |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Использование постоянного тома Kubernetes утверждения для групп POD в пул данных. `false` Использование временных узлов хранилища для модулей POD пула данных. |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | Указывает имя класса хранения Kubernetes для постоянного тома, связанные с модулей пула данных.|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |Указывает размер постоянного тома для каждого модуля в пуле данных. |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Использование постоянного тома Kubernetes утверждений для модулей в пуле носителей. `false` Использование временных узлов хранилища для модулей POD пула хранения.|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | TIndicates имя класса хранения Kubernetes для постоянного тома, связанные с модулей пула хранения. |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | Указывает размер постоянного тома для каждого модуля в пуле носителей. |

## <a name="next-steps"></a>Следующие шаги

Полную документацию о томах в Kubernetes см. в разделе [документации по Kubernetes на томах](https://kubernetes.io/docs/concepts/storage/volumes/).

Дополнительные сведения о развертывании кластера больших данных в SQL Server, см. в разделе [развертывание сервера SQL, большие данные кластера в Kubernetes](deployment-guidance.md).

