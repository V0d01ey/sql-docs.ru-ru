---
title: dbo.sysjobactivity (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77b434a20f408aa79e8d75b03ea9bce0a9f2e6b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470968"
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Регистрирует текущее действие и состояние задания агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Эта таблица хранится в **msdb** базы данных.
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Идентификатор сеанса, хранящихся в **syssessions** в таблицу **msdb** базы данных.|  
|**job_id**|**uniqueidentifier**|Идентификатор задания.|  
|**run_requested_date**|**datetime**|Дата и время последнего запроса на выполнение задания.|  
|**run_requested_source**|**sysname(nvarchar(128))**|Источник запроса на выполнение задания.<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|Дата и время последней постановки задания в очередь. Если задание запускается немедленно, значение этого столбца равно NULL.|  
|**start_execution_date**|**datetime**|Дата и время последнего выполнения задания по расписанию.|  
|**last_executed_step_id**|**int**|Идентификатор последнего выполненного шага задания.|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|Дата и время начала выполнения последнего шага задания.|  
|**stop_execution_date**|**datetime**|Дата и время завершения выполнения задания.|  
|**job_history_id**|**int**|Используется для идентификации строки в **sysjobhistory** таблицы.|  
|**next_scheduled_run_date**|**datetime**|Дата и время следующего выполнения задания по расписанию.|  

## <a name="example"></a>Пример
Этот пример возвращает состояние времени выполнения для всех заданий агента SQL Server.  Выполните приведенный ниже код [!INCLUDE[tsql](../../includes/tsql-md.md)] в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```sql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>См. также  
 [dbo.sysjobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
