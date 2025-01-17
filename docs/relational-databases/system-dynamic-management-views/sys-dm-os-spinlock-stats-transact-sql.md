---
title: sys.dm_os_spinlock_stats (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
ms.assetid: ''
caps.latest.revision: ''
author: bluefooted
ms.author: pamela
manager: amitban
ms.workload: Inactive
ms.openlocfilehash: d26369b657848bf1ff092bc69fba1a6aa5850102
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/27/2019
ms.locfileid: "67420856"
---
# <a name="sysdmosspinlockstats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Возвращает сведения обо всех случаях ожидания спин-блокировки, упорядоченных по типу.  
  

|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|Имя типа спин-блокировки.|  
|конфликты|**bigint**|Сколько раз поток пытается получить спин-блокировки и заблокирована, так как другой поток в настоящее время содержит спин-блокировки.|  
|Выполняет прокрутки|**bigint**|Количество раз, когда поток выполняет цикл при попытке получить спин-блокировки.|  
|spins_per_collision|**real**|Отношение количества включается на конфликт.|  
|sleep_time|**bigint**|Количество времени в миллисекундах, затраченное что потоки в спящем режиме в случае задержки.|  
|как|**int**|Сколько раз поток, который находится «в состоянии» не удается получить спин-блокировки и освободив планировщик.|  


## <a name="permissions"></a>Разрешения  
На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Premium необходимо `VIEW DATABASE STATE` разрешение в базе данных. На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] уровней Standard и Basic, требует **администратора сервера** или **администратор Azure Active Directory** учетной записи.    
  
## <a name="remarks"></a>Примечания  
 
 sys.dm_os_spinlock_stats может использоваться для выявления источника состязания спин-блокировок. В некоторых ситуациях может быть способны разрешать и уменьшить количество конфликтов спин-блокировки. Но возможны и такие ситуации, когда будет необходимо обратиться в службу поддержки пользователей [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Вы можете сбросить содержимое sys.dm_os_spinlock_stats с помощью `DBCC SQLPERF` следующим образом:  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 В результате все счетчики будут обнулены.  
  
> [!NOTE]  
>  При перезапуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] эти статистические данные не сохраняются. Все данные представляют собой совокупные значения, полученные за время после последнего сброса статистических сведений или со времени запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="spinlocks"></a>Спин-блокировки  
 Спин-блокировки, является объектом упрощенной синхронизации, использованное для сериализации доступа к структурам данных, которые обычно хранятся на короткое время. Если поток пытается получить доступ к ресурсу, защищенному спин-блокировки, которая удерживается другим потоком, поток будет выполнять цикл, или «запустить» и повторите доступ к ресурсу, вместо того, чтобы немедленно получить планировщик, как и в случае с кратковременной блокировки или другому ресурсу Подождите. Поток продолжит вращающийся пока не доступен этот ресурс или завершения цикла, после чего поток yield планировщик и вернуться в очереди ожидания запуска. Такой подход позволяет сократить поток чрезмерного переключений контекста, но при высокой состязания спин-блокировки, могут наблюдаться значительные ЦП.
   
 Следующая таблица содержит краткое описание некоторых наиболее распространенных типов спин-блокировки.  
  
|Тип спин-блокировки|Описание|  
|-----------------|-----------------|  
|ABR|Только для внутреннего применения.|
|ADB_CACHE|Только для внутреннего применения.|
|ALLOC_CACHES_HASH|Только для внутреннего применения.|
|APPENDONLY_STORAGE|Только для внутреннего применения.|
|APRC_BACK_OFF_STATS|Только для внутреннего применения.|
|APRC_EVENT_LIST|Только для внутреннего применения.|
|APRC_QUEUE_LIST|Только для внутреннего применения.|
|APRC_VALIDATION_QUEUE_LIST|Только для внутреннего применения.|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|Только для внутреннего применения.|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|Только для внутреннего применения.|
|ASYNCSTATSLIST|Только для внутреннего применения.|
|BACKUP|Только для внутреннего применения.|
|BACKUP_COPY_CONTEXT|Только для внутреннего применения.|
|BACKUP_CTX|Только для внутреннего применения.|
|BASE_XACT_HASH|Только для внутреннего применения.|
|BLOCKER_ENUM|Только для внутреннего применения.|
|BPREPARTITION|Только для внутреннего применения.|
|BPWORKFILE|Только для внутреннего применения.|
|BUF_HASH|Только для внутреннего применения.|
|BUF_LINK|Только для внутреннего применения.|
|BUF_WRITE_LOG|Только для внутреннего применения.|
|CACHEOBJ_DBG|Только для внутреннего применения.|
|CHANNELFORCECLOSEMANAGER|Только для внутреннего применения.|
|CHECK_AGGREGATE_STATE|Только для внутреннего применения.|
|CLR_HOSTTASK|Только для внутреннего применения.|
|CLR_SPIN_LOCK|Только для внутреннего применения.|
|CMED_DATABASE|Только для внутреннего применения.|
|CMED_HASH_SET|Только для внутреннего применения.|
|COLUMNDATASETSESSIONLIST|Только для внутреннего применения.|
|COLUMNSTORE_HASHTABLE|Только для внутреннего применения.|
|COLUMNSTOREBUILDSTATE_LIST|Только для внутреннего применения.|
|COM_INIT|Только для внутреннего применения.|
|ФИКСИРУЕМУЮ|Только для внутреннего применения.|
|COMPPLAN_SKELETON|Только для внутреннего применения.|
|CONNECTION_MANAGER|Только для внутреннего применения.|
|ПОДКЛЮЧАЕТСЯ|Только для внутреннего применения.|
|CSIBUILDMEM|Только для внутреннего применения.|
|CURSOR|Только для внутреннего применения.|
|CURSQL|Только для внутреннего применения.|
|DATAPORTCONSUMER|Только для внутреннего применения.|
|DATAPORTSOURCEINFOCREDIT|Только для внутреннего применения.|
|DATAPORTSOURCEINFOQUEUE|Только для внутреннего применения.|
|DATASET_FREELIST|Только для внутреннего применения.|
|DBCC_CHECK|Только для внутреннего применения.|
|DBSEEDING_OPERATION|Только для внутреннего применения.|
|DBT_HASH|Только для внутреннего применения.|
|DBT_IO_LIST|Только для внутреннего применения.|
|DBTABLE|Управляет доступом к структуре данных в памяти для каждой базы данных в SQL Server, содержащий свойства для этой базы данных. См. в разделе [в этой статье](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789) Дополнительные сведения. |
|DEFERRED_WF_EXT_DROP|Только для внутреннего применения.|
|DEK_INSTANCE|Только для внутреннего применения.|
|DELAYED_PARTITIONED_STACK|Только для внутреннего применения.|
|DELETEBITMAP|Только для внутреннего применения.|
|DIAG_MANAGER|Только для внутреннего применения.|
|DIAG_OBJECT|Только для внутреннего применения.|
|DIGEST_CACHE|Только для внутреннего применения.|
|DINPBUF|Только для внутреннего применения.|
|DIRECTLOGCONSUMER|Только для внутреннего применения.|
|DP_LIST|Управляет доступом к списку "грязных" страниц для базы данных с косвенными контрольными точками, включен. См. в разделе [в этой статье](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510) Дополнительные сведения.|
|DROP|Только для внутреннего применения.|
|DROP_TEMPO|Только для внутреннего применения.|
|DROPPED_ALLOC_UNIT|Только для внутреннего применения.|
|DTC_HASHTABLE|Только для внутреннего применения.|
|DTT_LIST|Только для внутреннего применения.|
|ENDD_LIST|Только для внутреннего применения.|
|EXT_CACHE|Только для внутреннего применения.|
|EXTENT_ACTIVATION|Только для внутреннего применения.|
|FABRIC_DB_MGR_PTR|Только для внутреннего применения.|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|Только для внутреннего применения.|
|FABRIC_REPLICA_TRANSPORT|Только для внутреннего применения.|
|FABRIC_TVF_DATA_CONSUMER_LIST|Только для внутреннего применения.|
|FABRIC_TVF_LOAD_LIB|Только для внутреннего применения.|
|FCB_REPLICA_SYNC|Только для внутреннего применения.|
|FGCB_PRP_FILL|Только для внутреннего применения.|
|FILE_HANDLE_CACHE|Только для внутреннего применения.|
|FILE_TABLE|Только для внутреннего применения.|
|FILESTREAM_CHUNKER|Только для внутреннего применения.|
|FREE_SPACE_CACHE_ENTRY|Только для внутреннего применения.|
|FS_CONTAINER_LIST_WITH_DELETE|Только для внутреннего применения.|
|FS_DELETED_FOLDER_CLEANUP|Только для внутреннего применения.|
|FSAGENT|Только для внутреннего применения.|
|FSGHOST_STATUS|Только для внутреннего применения.|
|FT_INIT|Только для внутреннего применения.|
|GHOST_FREE|Только для внутреннего применения.|
|GHOST_HASH|Только для внутреннего применения.|
|GLOBAL_SCHEDULER_LIST|Только для внутреннего применения.|
|GLOBAL_TRACE_FLAGS|Только для внутреннего применения.|
|GLOBALTRANS|Только для внутреннего применения.|
|GROUP_COMMIT_FEEDBACK_LOOP|Только для внутреннего применения.|
|GUARDIAN|Только для внутреннего применения.|
|HADR_AGH_X_ACCESS|Только для внутреннего применения.|
|HADR_AR_CONTROLLER_COLLECTION|Только для внутреннего применения.|
|HADR_AR_DB_MGR|Только для внутреннего применения.|
|HADR_AR_TRANSPORT|Только для внутреннего применения.|
|HADR_COMPRESSION_MGR_POOL|Только для внутреннего применения.|
|HADR_FABRIC_FACTORY|Только для внутреннего применения.|
|HADR_PRIORITY_QUEUE|Только для внутреннего применения.|
|HADR_TRANSPORT_CONTROL|Только для внутреннего применения.|
|HADR_TRANSPORT_LIST|Только для внутреннего применения.|
|HADRSEEDINGLIST|Только для внутреннего применения.|
|HOBT_DROPPED|Только для внутреннего применения.|
|HOBT_HASH|Только для внутреннего применения.|
|HTTP|Только для внутреннего применения.|
|HTTP_CONNCACHE|Только для внутреннего применения.|
|HTTP_ENDPOINT|Только для внутреннего применения.|
|IDENTITY|Только для внутреннего применения.|
|INDEX_CREATE|Только для внутреннего применения.|
|IO_DISPENSER_PAUSE|Только для внутреннего применения.|
|IO_RG_VOLUME_HASHTABLE|Только для внутреннего применения.|
|IOREQ|Только для внутреннего применения.|
|ISSRESOURCE|Только для внутреннего применения.|
|KTM_ENLISTMENT|Только для внутреннего применения.|
|LANG_RES_LOAD|Только для внутреннего применения.|
|LIVE_TARGET_TVF|Только для внутреннего применения.|
|LOCK_FREE_LIST|Только для внутреннего применения.|
|LOCK_HASH|Защищает доступ к хэш-таблицы диспетчера блокировок, хранит сведения о блокировки, удерживаемые в базе данных. См. в разделе [в этой статье](https://support.microsoft.comkb/2926217) Дополнительные сведения.|
|LOCK_NOTIFICATION|Только для внутреннего применения.|
|LOCK_RESOURCE_ID|Только для внутреннего применения.|
|LOCK_RW_ABTX_HASH_SET|Только для внутреннего применения.|
|LOCK_RW_AGDB_HEALTH_DIAG|Только для внутреннего применения.|
|LOCK_RW_CMED_HASH_SET|Только для внутреннего применения.|
|LOCK_RW_DPT_TABLE|Только для внутреннего применения.|
|LOCK_RW_IN_ROW_TRACKER|Только для внутреннего применения.|
|LOCK_RW_LOGIN_RATE_STATS|Только для внутреннего применения.|
|LOCK_RW_PVS_PAGE_TRACKER|Только для внутреннего применения.|
|LOCK_RW_RBIO_REQ|Только для внутреннего применения.|
|LOCK_RW_SECURITY_CACHE|Только для внутреннего применения.|
|LOCK_RW_TEST|Только для внутреннего применения.|
|LOCK_RW_WPR_BUCKET|Только для внутреннего применения.|
|LOCK_SORT_STREAM|Только для внутреннего применения.|
|LOCK_SQLSATELLITE_MESSAGE|Только для внутреннего применения.|
|LOG_CONSOLIDATION|Только для внутреннего применения.|
|LOG_RG_GOVERNOR|Только для внутреннего применения.|
|LOGCACHE_ACCESS|Только для внутреннего применения.|
|LOGFLUSHQ|Только для внутреннего применения.|
|LOGIOSEQ|Только для внутреннего применения.|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|Только для внутреннего применения.|
|LOGLC|Только для внутреннего применения.|
|LOGLFM|Только для внутреннего применения.|
|LOGON_TRIGGER_CACHE|Только для внутреннего применения.|
|LOGPOOL_HASHBUCKET|Только для внутреннего применения.|
|LOGPOOL_REFCOUNTEDOBJECT|Только для внутреннего применения.|
|LOGPOOL_SHAREDCACHEBUFFER|Только для внутреннего применения.|
|LOGPOOL_SIZEPERRESOURCEPOOL|Только для внутреннего применения.|
|LPE_BATCH|Только для внутреннего применения.|
|LPE_SESSION|Только для внутреннего применения.|
|LPE_SXTP|Только для внутреннего применения.|
|LSID|Только для внутреннего применения.|
|LSLIST|Только для внутреннего применения.|
|LSNREFLIST|Только для внутреннего применения.|
|LSS_SYNC_DTC|Только для внутреннего применения.|
|MD_CHANGE_NOTIFICATION|Только для внутреннего применения.|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|Только для внутреннего применения.|
|MDB_REMOTE_SESSION_HASH_TABLE|Только для внутреннего применения.|
|MEM_MGR|Только для внутреннего применения.|
|MGR_CACHE|Только для внутреннего применения.|
|MIGRATION_BUF_LIST|Только для внутреннего применения.|
|NETCONN_ADDRESS|Только для внутреннего применения.|
|ONDEMAND_TASK|Только для внутреннего применения.|
|ONE_PROC_SIM_NODE_CONTEXT|Только для внутреннего применения.|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|Только для внутреннего применения.|
|ONE_PROC_SIM_REPLICA_CONTEXT|Только для внутреннего применения.|
|ONE_PROC_SIM_SERVICE_PARTITION|Только для внутреннего применения.|
|OPT_IDX_MISS_ID|Только для внутреннего применения.|
|OPT_IDX_MISS_KEY|Только для внутреннего применения.|
|OPT_IDX_STATS|Только для внутреннего применения.|
|OPT_INFO_MGR|Только для внутреннего применения.|
|PAGE_WORKITEMLIST|Только для внутреннего применения.|
|PAGECOPIER|Только для внутреннего применения.|
|PARALLELREDOCACHE|Только для внутреннего применения.|
|PARTITIONED_HEAP_FREE_LIST|Только для внутреннего применения.|
|PROGRESS_REPORT|Только для внутреннего применения.|
|QE_SHUTDOWN|Только для внутреннего применения.|
|QSCAN_CACHE|Только для внутреннего применения.|
|QUERY_EXEC_STATS|Только для внутреннего применения.|
|QUERY_STORE_ASYNC_PERSIST|Только для внутреннего применения.|
|QUERY_STORE_ASYNC_QUEUE_TLIST|Только для внутреннего применения.|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|Только для внутреннего применения.|
|QUERY_STORE_CAPTURE_POLICY_STATS|Только для внутреннего применения.|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|Только для внутреннего применения.|
|QUERY_STORE_CURRENT_INTERVAL|Только для внутреннего применения.|
|QUERY_STORE_HT_CACHE|Только для внутреннего применения.|
|QUERY_STORE_LIST|Только для внутреннего применения.|
|QUERY_STORE_PLAN_COMP_AGG|Только для внутреннего применения.|
|QUERY_STORE_PLAN_LIST|Только для внутреннего применения.|
|QUERY_STORE_READ_ONLY_FLAGS|Только для внутреннего применения.|
|QUERY_STORE_SELF_AGG|Только для внутреннего применения.|
|QUERY_STORE_STMT_COMP_AGG|Только для внутреннего применения.|
|QUERYEXEC|Только для внутреннего применения.|
|QUERYSCAN|Только для внутреннего применения.|
|RANGE_GENERATION|Только для внутреннего применения.|
|READ_AHEAD|Только для внутреннего применения.|
|REDOMGRSTATE|Только для внутреннего применения.|
|REMOTE_SESSION_CACHE|Только для внутреннего применения.|
|REMOTEBLOCKIO|Только для внутреннего применения.|
|REMOTEOP|Только для внутреннего применения.|
|REPL_LOGREADER_HISTORY_CACHE|Только для внутреннего применения.|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|Только для внутреннего применения.|
|RESMANAGER|Только для внутреннего применения.|
|РЕСУРС|Только для внутреннего применения.|
|RESQUEUE|Только для внутреннего применения.|
|RFS_THREAD_QUEUE|Только для внутреннего применения.|
|RG_TIMER|Только для внутреннего применения.|
|ROWGROUP_VERSIONS|Только для внутреннего применения.|
|RPCCHANNELPOOL|Только для внутреннего применения.|
|RPCPACKAGE|Только для внутреннего применения.|
|RPCREQUESTORCONTEXT|Только для внутреннего применения.|
|RWLOCK_LAST|Только для внутреннего применения.|
|SATELLITE_CONNECTION|Только для внутреннего применения.|
|SBS_CLIENT_ENDPOINTS|Только для внутреннего применения.|
|SBS_CLIENT_REQUESTS|Только для внутреннего применения.|
|SBS_DISPATCH|Только для внутреннего применения.|
|SBS_PENDING|Только для внутреннего применения.|
|SBS_SERVER_XACT_TASK_PROXY|Только для внутреннего применения.|
|SBS_TRANSPORT|Только для внутреннего применения.|
|SBS_UCS_DISPATCH|Только для внутреннего применения.|
|БЕЗОПАСНОСТЬ|Только для внутреннего применения.|
|SECURITY_CACHE|Только для внутреннего применения.|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|Только для внутреннего применения.|
|SEMANTIC_TICACHE|Только для внутреннего применения.|
|SEQUENCED_OBJECT|Только для внутреннего применения.|
|SEQUEUE_SIZED_THREADSAFE|Только для внутреннего применения.|
|SESSION_KILLER|Только для внутреннего применения.|
|SESSION_MANAGER|Только для внутреннего применения.|
|SESSION_SEC_CONTEXT|Только для внутреннего применения.|
|SETRANGE_SYNC|Только для внутреннего применения.|
|SHARABLE_SESSION_OBJECTS|Только для внутреннего применения.|
|SLO_INFO_LIST|Только для внутреннего применения.|
|SNI|Только для внутреннего применения.|
|SNI_NODE_PENDING_IO_QUEUE|Только для внутреннего применения.|
|SOAPSESSIONS|Только для внутреннего применения.|
|SOS_ABORT_TASK|Только для внутреннего применения.|
|SOS_ACTIVEDESCRIPTOR|Только для внутреннего применения.|
|SOS_BLOCKALLOCPARTIALLIST|Только для внутреннего применения.|
|SOS_BLOCKDESCRIPTORBUCKET|Только для внутреннего применения.|
|SOS_CACHESTORE|Синхронизирует доступ к различные кэши в памяти в SQL Server как кэш планов или временной таблицы кэша. Серьезный конфликт на этот тип спин-блокировки может означать многих различных факторов, в зависимости от конкретных кэша, который находится в конкуренции. Обратитесь к [!INCLUDE[msCoName](../../includes/msconame-md.md)] службой поддержки для получения справки по устранению этот тип спин-блокировки. |
|SOS_CACHESTORE_CLOCK|Только для внутреннего применения.|
|SOS_CLOCKALG_INTERNODE_SYNC|Только для внутреннего применения.|
|SOS_DEBUG_HOOK|Только для внутреннего применения.|
|SOS_DESCDATABUFFERLIST|Только для внутреннего применения.|
|SOS_LARGEPAGE_ALLOCATOR|Только для внутреннего применения.|
|SOS_MINITHREAD|Только для внутреннего применения.|
|SOS_NODE|Только для внутреннего применения.|
|SOS_OBJECT_POOL|Только для внутреннего применения.|
|SOS_OBJECT_STORE|Только для внутреннего применения.|
|SOS_OOM_CHECK|Только для внутреннего применения.|
|SOS_PHYS_PAGE_CACHE|Только для внутреннего применения.|
|SOS_RESOURCE_CLERK_LIST|Только для внутреннего применения.|
|SOS_RINGBUFFER_RECORD|Только для внутреннего применения.|
|SOS_RW|Только для внутреннего применения.|
|SOS_SATELLITE_USER_POOL|Только для внутреннего применения.|
|SOS_SCHEDULER|Только для внутреннего применения.|
|SOS_SELIST_SIZED_SLOCK|Только для внутреннего применения.|
|SOS_SUSPEND_QUEUE|Только для внутреннего применения.|
|SOS_SYSTHREAD|Только для внутреннего применения.|
|SOS_SYSTHREAD_DISPATCHER|Только для внутреннего применения.|
|SOS_TASK|Только для внутреннего применения.|
|SOS_TLIST|Только для внутреннего применения.|
|SOS_VM_LOW|Только для внутреннего применения.|
|SOS_WAIT_STATS|Только для внутреннего применения.|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|Только для внутреннего применения.|
|SPIN_EVENT_MUTEX|Только для внутреннего применения.|
|SPL_DISPATCHER_LIST|Только для внутреннего применения.|
|SPL_DISPATCHER_QUEUE|Только для внутреннего применения.|
|SPL_NONYIELD_ANALYSIS|Только для внутреннего применения.|
|SPL_QUERY_STORE_CTX_INITIALIZED|Только для внутреннего применения.|
|SPL_QUERY_STORE_EXEC_STATS_AGG|Только для внутреннего применения.|
|SPL_QUERY_STORE_EXEC_STATS_READ|Только для внутреннего применения.|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|Только для внутреннего применения.|
|SPL_SOS_DISPATCHER|Только для внутреннего применения.|
|SPL_TDS_PKT_QUEUE|Только для внутреннего применения.|
|SPL_XE_BUFFER_MGR|Только для внутреннего применения.|
|SPL_XE_DISPATCHER_QUEUE|Только для внутреннего применения.|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|Только для внутреннего применения.|
|SPL_XE_SESSION_EVENT_MGR|Только для внутреннего применения.|
|SPL_XE_SESSION_MGR|Только для внутреннего применения.|
|SPL_XE_SESSION_TARGET_MGR|Только для внутреннего применения.|
|SPT_PROFILE|Только для внутреннего применения.|
|SQL_MGR|Только для внутреннего применения.|
|SQL_NORM|Только для внутреннего применения.|
|SQLTRACE_FILE_BUFFER|Только для внутреннего применения.|
|SRVPROC|Только для внутреннего применения.|
|STACK_HASHER|Только для внутреннего применения.|
|SUBLATCH|Только для внутреннего применения.|
|SUBPDESC|Только для внутреннего применения.|
|SUBPDESC_LIST|Только для внутреннего применения.|
|SVC_BROKER_CTRL|Только для внутреннего применения.|
|SVC_BROKER_DEBUG_LIST|Только для внутреннего применения.|
|SVC_BROKER_LIST|Только для внутреннего применения.|
|SVC_BROKER_OBJECT|Только для внутреннего применения.|
|SYNCPOINT_RESOURCE|Только для внутреннего применения.|
|TaskElapsedExecutionMonitor|Только для внутреннего применения.|
|TDS_TVP|Только для внутреннего применения.|
|TESTTEAM|Только для внутреннего применения.|
|TESTTEAMEXPONENTIAL|Только для внутреннего применения.|
|TESTTEAMEXPONENTIALTASTAS|Только для внутреннего применения.|
|TESTTEAMTASTAS|Только для внутреннего применения.|
|TMP_SESS_KEY|Только для внутреннего применения.|
|TSQL_DEBUG|Только для внутреннего применения.|
|TXFRM_REPL|Только для внутреннего применения.|
|VDI_OPERATION|Только для внутреннего применения.|
|WINFAB_REPORT_FAULT|Только для внутреннего применения.|
|WRITE_PAGE_RECORDER|Только для внутреннего применения.|
|X_PACKET_LIST|Только для внутреннего применения.|
|X_PIPE|Только для внутреннего применения.|
|X_PIPE_DEMAND|Только для внутреннего применения.|
|X_PORT|Только для внутреннего применения.|
|XACT_LOCK_INFO|Только для внутреннего применения.|
|XACT_LOCKINFO_TASK|Только для внутреннего применения.|
|XACT_WORKSPACE|Только для внутреннего применения.|
|XCB|Только для внутреннего применения.|
|XCB_FREE_LIST|Только для внутреннего применения.|
|XCB_HASH|Только для внутреннего применения.|
|XCHNG_TRACE|Только для внутреннего применения.|
|XDES|Только для внутреннего применения.|
|XDES_HASH|Только для внутреннего применения.|
|XDESMGR|Только для внутреннего применения.|
|XDESTABLELIST|Только для внутреннего применения.|
|XE_RATE_LIMITER_STRETCHDB|Только для внутреннего применения.|
|XE_SESSION_STORAGE|Только для внутреннего применения.|
|XID_ARRAY|Только для внутреннего применения.|
|XIO_BLOCKLIST|Только для внутреннего применения.|
|XIO_REQSTR|Только для внутреннего применения.|
|XIO_SEQNUMBUMP|Только для внутреннего применения.|
|XIOSTATS|Только для внутреннего применения.|
|XTP_RT_DATA_LIST|Только для внутреннего применения.|
|XTS_MGR|Только для внутреннего применения.|
|XVB_CSN|Только для внутреннего применения.|
|XVB_LIST|Только для внутреннего применения.|
 

  
## <a name="see-also"></a>См. также  
 
 [DBCC SQLPERF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [Динамические административные представления, относящиеся к операционной системе SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [При спин-блокировки значительные драйвер из ЦП в SQL Server?](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [Диагностика и устранение состязания спин-блокировок в SQL Server](https://www.microsoft.com/download/details.aspx?id=26666)
  
  


