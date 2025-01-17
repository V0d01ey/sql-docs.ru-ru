---
title: Подписка, вкладка "Нераспространенные команды" (транзакционная подписка) | Документация Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac1111c3f6f5756b03b2a852776bc86e93264b78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62752258"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>Подписка, вкладка "Нераспространенные команды" (транзакционная подписка)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  На вкладке **Нераспространенные команды** отображаются сведения о количестве команд в базе данных распространителя, которые не были доставлены выбранному подписчику, и приблизительное время для доставки этих команд. Дополнительные сведения о просмотре этих команд в базе данных распространителя см. в статье [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md).  
  
## <a name="options"></a>Параметры  
 **Число команд в базе данных распространителя, которые ожидают применения к этому подписчику.**  
 Количество команд в базе данных распространителя, которые не были доставлены выбранному подписчику. Команда состоит из одной инструкции языка обработки данных (DML) или одной инструкции языка определения данных (DDL) языка Transact-SQL.  
  
 **Расчетное время применения этих команд, вычисленное по результатам предыдущего выполнения.**  
 Примерное количество времени, необходимое для доставки команд на подписчик. Если это значение превышает количество времени, требуемое для создания и применения моментального снимка на подписчике, рассмотрите возможность повторной инициализации подписчика. Дополнительные сведения см. в статье [Повторная инициализация подписок](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Наблюдение за производительностью с помощью монитора репликации](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
