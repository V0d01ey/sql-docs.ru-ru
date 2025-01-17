---
title: Использование пороговых значений предупреждений и оповещений в метриках производительности зеркального отображения | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- thresholds [SQL Server]
- database mirroring [SQL Server], managing in SQL Server Management Studio
- alerts [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
- warnings [database mirroring]
ms.assetid: 8cdd1515-0bd7-4f8c-a7fc-a33b575e20f6
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: fcf22dd79fb19585f1f62ddfd52b89420b135380
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795101"
---
# <a name="use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server"></a>Использование пороговых значений предупреждений и оповещений в метриках производительности зеркального отображения (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В этом разделе содержатся сведения о событиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , для которых можно настраивать пороговые значения предупреждений и управлять ими для зеркального отображения базы данных. Это можно сделать с помощью монитора зеркального отображения баз данных или хранимых процедур **sp_dbmmonitorchangealert**, **sp_dbmmonitorhelpalert**и **sp_dbmmonitordropalert** . В этом разделе содержатся также сведения о настройке предупреждений о событиях зеркального отображения баз данных.  
  
 После того как установлено наблюдение в зеркальной базе данных, системный администратор может настроить пороговые значения предупреждений по нескольким метрикам производительности, а также предупреждения для этих и других событий зеркального отображения базы данных.  
  
 **В этом разделе:**  
  
-   [Метрики производительности и пороговые значения предупреждений](#PerfMetricsAndWarningThresholds)  
  
-   [Установка и управление пороговыми значениями предупреждений](#SetUpManageWarningThresholds)  
  
-   [Использование предупреждений для зеркальной базы данных](#UseAlerts)  
  
-   [Связанные задачи](#RelatedTasks)  
  
##  <a name="PerfMetricsAndWarningThresholds"></a> Метрики производительности и пороговые значения предупреждений  
 В следующей таблице перечислены метрики производительности, для которых можно настроить предупреждения, описаны пороговые значения и перечислены соответствующие им метки монитора зеркального отображения баз данных.  
  
|Метрика производительности|Пороговое значение предупреждения|Метка монитора зеркального отображения баз данных|  
|------------------------|-----------------------|--------------------------------------|  
|Неотправленный журнал|Указывает, какое количество килобайтов (КБ) неотправленного журнала формирует предупреждение в экземпляре основного сервера. Это предупреждение помогает измерить объем возможных потерь данных в килобайтах и особенно подходит для режима высокой производительности, Однако это предупреждение также уместно в режиме высокой безопасности, когда зеркальное отображение приостановлено или прекращено, потому что участники были разъединены.|**Предупреждать, если размер неотправленного журнала превышает пороговое значение.**|  
|Невосстановленный журнал|Указывает, какое количество килобайтов (КБ) невосстановленного журнала формирует предупреждение в экземпляре зеркального сервера. Это предупреждение помогает вычислить время отработки отказа. *Время отработки отказа* в основном состоит из времени, необходимого бывшему зеркальному серверу для наката всех журналов, оставшихся в его очереди повторов, и небольшого дополнительного времени.<br /><br /> Примечание. Время, которое потребуется системе, чтобы заметить ошибку, не зависит от времени отработки отказа, если она выполняется автоматически.<br /><br /> Дополнительные сведения см. в статье [Оценка прерывания обслуживания во время переключения ролей (зеркальное отображение базы данных)](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|**Предупреждать, если размер невосстановленного журнала превысил пороговое значение.**|  
|Самая старая неотправленная транзакция|Указывает количество транзакций за минуту, которые могут накопиться в очереди передачи перед тем, как будет сформировано предупреждение в экземпляре основного сервера. Это предупреждение помогает измерить возможные потери времени, что особенно актуально для режима высокой производительности, Однако это предупреждение также уместно в режиме высокой безопасности, когда зеркальное отображение приостановлено или прекращено, потому что участники были разъединены.|**Предупреждать, если время хранения самой старой неотправленной транзакции превысило пороговое значение.**|  
|Затраты на фиксирование изменений на зеркальном сервере|Указывает количество миллисекунд средней задержки транзакции, которая допустима перед формированием предупреждения на основном сервере. Задержка — это объем дополнительной нагрузки во время ожидания экземпляром основного сервера экземпляра зеркального сервера для добавления записи журнала транзакции в очередь повтора. Это значение уместно только в режиме высокой безопасности.|**Предупреждать, если затраты на фиксирование изменений на зеркальном сервере превысили пороговое значение.**|  
  
 Администратор может задать в зеркальной базе данных пороговое значение для любой из этих метрик производительности. Дополнительные сведения см. в подразделе [Установка пороговых значений предупреждений и управление ими](#SetUpManageWarningThresholds)ниже в этом разделе.  
  
##  <a name="SetUpManageWarningThresholds"></a> Установка и управление пороговыми значениями предупреждений  
 Системным администратором может быть настроено одно или несколько пороговых значений предупреждений для ключевых метрик производительности зеркального отображения. Рекомендуется это делать на обоих участниках, чтобы гарантировать сохранение предупреждения при переходе базы данных на другой ресурс. Соответствующее пороговое значение на каждом из участников зависит от производительности системы на нем.  
  
 Пороговые значения предупреждений можно настраивать и контролировать одним из следующих способов.  
  
-   Монитор зеркального отображения баз данных.  
  
     В мониторе зеркального отображения баз данных администратор может одновременно просматривать текущую конфигурацию предупреждений для выделенной базы данных на экземплярах как основного, так и зеркального сервера, выбрав страницу со вкладками **Предупреждения** . Доступное на странице диалоговое окно **Установка пороговых значений предупреждений** позволяет включить и настроить одно или несколько пороговых значений предупреждений.  
  
     Основные сведения об интерфейсе монитора зеркального отображения баз данных см. в разделе [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md). Сведения о запуске монитора зеркального отображения базы данных см. в разделе [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md).  
  
-   Системные хранимые процедуры  
  
     Следующий набор системных хранимых процедур позволяет администратору устанавливать пороговые значения предупреждений и управлять ими в зеркальной базе данных одного из участников.  
  
    |Процедура|Описание|  
    |---------------|-----------------|  
    |[sp_dbmmonitorchangealert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)|Добавляет или изменяет пороговое значение предупреждения для указанной метрики производительности зеркального отображения баз данных.|  
    |[sp_dbmmonitorhelpalert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)|Возвращает сведения о порогах предупреждения для одной или всех ключевых метрик производительности монитора зеркального отображения базы данных.|  
    |[sp_dbmmonitordropalert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)|Удаляет предупреждение для указанной метрики производительности.|  
  
## <a name="performance-threshold-events-sent-to-the-windows-event-log"></a>Пороговые события производительности, отправляемые в журнал событий Windows  
 Если для метрики производительности определено пороговое значение предупреждения, то при обновлении таблицы состояния последнее значение сравнивается с пороговым. Если оно достигнуто, процедура обновления **sp_dbmmonitorupdate** создает для метрики информационное событие — *пороговое событие производительности* — и записывает его в журнал событий [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. В следующей таблице приведены идентификаторы пороговых событий производительности.  
  
|Метрика производительности|Идентификатор события|  
|------------------------|--------------|  
|Неотправленный журнал|32042|  
|Невосстановленный журнал|32043|  
|Самая старая неотправленная транзакция|32040|  
|Затраты на фиксирование изменений на зеркальном сервере|32044|  
  
> [!NOTE]  
>  Администратор может определить оповещения для одного или нескольких таких событий. Дополнительные сведения см. в подразделе [Использование предупреждений для зеркальной базы данных](#UseAlerts)ниже в этом  
>   
>  разделе.  
  
##  <a name="UseAlerts"></a> Использование предупреждений для зеркальной базы данных  
 Существенной частью наблюдения за зеркальной базой данных является настройка предупреждений о важных событиях зеркального отображения базы данных. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] формирует следующие типы событий зеркального отображения базы данных.  
  
-   Пороговые события производительности  
  
     Дополнительные сведения см. выше в разделе «Пороговые события производительности, отправляемые в журнал событий Windows».  
  
-   События изменения состояния  
  
     Это события инструментария управления Windows (WMI), которые возникают при изменениях внутреннего состояния сеанса зеркального отображения базы данных.  
  
    > [!NOTE]  
    >  Дополнительные сведения см. в разделе [Основные понятия о поставщике WMI для событий сервера](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 Системный администратор может настроить оповещения об этих событиях с помощью агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или других приложений (например [!INCLUDE[msCoName](../../includes/msconame-md.md)] Operations Manager).  
  
 При определении оповещений о событиях зеркального отображения базы данных рекомендуется задавать пороговые значения предупреждений и оповещения на обоих экземплярах сервера-участника. Отдельные события формируются и на основном, и на зеркальном сервере, но каждый из участников в любой момент времени может выполнять любую роль. Чтобы гарантировать работу оповещений после отработки отказа, они должны быть определены на обоих участниках.  
  
> [!IMPORTANT]  
>  Для всех сеансов зеркального отображения настоятельно рекомендуется настроить базу данных для отправки предупреждений обо всех событиях изменения состояния. Такое событие означает, что произошло нечто, способное скомпрометировать данные, если это не изменение, связанное с ручной настройкой базы данных. Чтобы защитить данные, необходимо определить и устранить причину непредвиденного изменения состояния.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Создание предупреждения в среде SQL Server Management Studio**  
  
-   [Создание предупреждения по номеру сообщения](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Создание предупреждения о событии WMI](../../ssms/agent/create-a-wmi-event-alert.md)  
  
 **Слежение за зеркальным отображением базы данных**  
  
-   [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitoraddmonitoring (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>См. также:  
 [Зеркальное отображение базы данных (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Наблюдение за зеркальным отображением базы данных (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
