---
title: Что такое контроллер?
titleSuffix: SQL Server big data clusters
description: В этой статье описывается контроллер кластера SQL Server 2019 больших данных (Предварительная версия).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a0623a920b060e4d5d1e7724f39e2eadb0bd2475
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387950"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>Что такое контроллер в кластере SQL Server больших данных?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

На контроллере размещены основную логику для развертывания и управления ими кластерам больших данных. Она отвечает за все взаимодействия с помощью Kubernetes, экземпляры SQL Server, которые являются частью кластера и другие компоненты, такие как HDFS и Spark.

Служба контроллера предоставляет следующие основные функции:

- Управление жизненным циклом кластера: начальная загрузка кластера и удаление, обновление конфигураций
- Управление главным экземплярам SQL Server
- Управление пулами вычисления, хранения и данных
- Предоставляют средства мониторинга для наблюдения за состоянием кластера
- Предоставляют средства устранения неполадок для обнаружения и устранения неожиданных неполадок
- Управление безопасностью кластера:
  - Убедитесь, конечные точки защищенного кластера
  - Управлять пользователями и ролями
  - Настройка учетных данных для обмена данными внутри кластера

## <a name="deploying-the-controller-service"></a>Развертывание службы контроллера

Контроллер развернут и размещенной в том же пространстве имен Kubernetes, где клиент хочет создать кластерам больших данных. Эта служба устанавливается администратором Kubernetes во время начальной загрузки, с помощью кластера **mssqlctl** программы командной строки. Дополнительные сведения см. в разделе [приступить к работе с кластерами больших данных в SQL Server](deploy-get-started.md).

Рабочий процесс занимались будет макета на основе Kubernetes полнофункциональные кластера больших данных SQL Server, включающий все компоненты, описанные в [Обзор](big-data-cluster-overview.md) статьи. Рабочего процесса начальной загрузки сначала создает службу контроллера, и после развертывания это служба контроллера будет координировать установку и настройку остальной части служб пулов master, вычислений, данных и хранилища.

## <a name="managing-the-cluster-through-the-controller-service"></a>Управление кластером через службу контроллера

Вы можете управлять кластером через службу контроллера, с помощью **mssqlctl** команды. При развертывании дополнительных объектов Kubernetes как POD, содержащихся в одном пространстве имен, они не управляются и наблюдение за службой контроллера. Можно также использовать **kubectl** команды для управления кластером, на уровне Kubernetes. Дополнительные сведения см. в разделе [мониторинг и устранение неполадок с кластерами больших данных SQL Server](cluster-troubleshooting-commands.md).

Контроллер и объекты Kubernetes (наборы с отслеживанием состояния, модулей, секреты и др.), созданные для работы с большими данными кластера размещаются в выделенном пространстве имен Kubernetes. Служба контроллера будет предоставлено разрешение, администратор кластера Kubernetes может управлять всеми ресурсами в этом пространстве имен.  Политики RBAC для этого сценария настраивается автоматически в рамках первоначального развертывания с помощью **mssqlctl**.

### <a name="mssqlctl"></a>mssqlctl

**mssqlctl** — программа командной строки, написанный на Python, что позволяет кластера администраторов для начальной загрузки и управление кластерами больших данных с помощью REST API, предоставляемые службой контроллера.

## <a name="controller-service-security"></a>Контроллер службы безопасности

Весь обмен данными с контроллером службы проводится через REST API по протоколу HTTPS. Самозаверяющий сертификат автоматически создается автоматически во время начальной загрузки. 

Проверка подлинности, в конечную точку службы контроллера основана на имя пользователя и пароль. Эти учетные данные подготавливаются во время начальной загрузки кластера, с помощью входных данных для переменных среды `CONTROLLER_USERNAME` и `CONTROLLER_PASSWORD`.

> [!NOTE]
> Необходимо указать пароль, который будет в соответствии с [требования к сложности пароля SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о кластерах больших данных SQL Server, см. следующие ресурсы:

- [Что такое кластеры SQL Server 2019 больших данных?](big-data-cluster-overview.md)
- [Семинар: Кластерами больших данных Microsoft SQL Server архитектуры](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
