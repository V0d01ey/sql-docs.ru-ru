---
title: sys.dm_os_latch_stats (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_latch_stats_TSQL
- dm_os_latch_stats_TSQL
- dm_os_latch_stats
- sys.dm_os_latch_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_latch_stats dynamic management view
ms.assetid: 2085d9fc-828c-453e-82ec-b54ed8347ae5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb61a77aca509393143d4abae98af0a9efb5e888
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048048"
---
# <a name="sysdmoslatchstats-transact-sql"></a>sys.dm_os_latch_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает сведения обо всех случаях ожидания кратковременных блокировок, систематизированных по классам.  
  
> [!NOTE]  
>  Вызывать его из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], используйте имя **sys.dm_pdw_nodes_os_latch_stats**.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|latch_class|**nvarchar(120)**|Имя класса кратковременных блокировок.|  
|waiting_requests_count|**bigint**|Число ожиданий кратковременных блокировок в данном классе. Этот счетчик увеличивается в начале ожидания кратковременной блокировки.|  
|wait_time_ms|**bigint**|Общее время ожидания кратковременных блокировок в данном классе в миллисекундах.<br /><br /> **Примечание.** Этот столбец обновляется каждые пять минут, во время ожидания кратковременной блокировки и в конце ожидания кратковременной блокировки.|  
|max_wait_time_ms|**bigint**|Максимальный период времени ожидания данной кратковременной блокировки объектом памяти. Если данное значение неестественно велико, это может указывать на взаимоблокировку.|  
|pdw_node_id|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение является на.|  
  
## <a name="permissions"></a>Разрешения  

На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], требуется `VIEW DATABASE STATE` разрешение в базе данных.   
  
## <a name="remarks"></a>Примечания  
 Представление динамического управления sys.dm_os_latch_stats может быть использовано для выявления источника состязания между кратковременными блокировками путем исследования относительного числа ожиданий и времени ожидания для различных классов кратковременных блокировок. В некоторых ситуациях возможно устранение состязания между кратковременными блокировками или снижение его остроты. Но возможны и такие ситуации, когда будет необходимо обратиться в службу поддержки пользователей [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Очистить содержимое представления sys.dm_os_latch_stats с помощью инструкции `DBCC SQLPERF` можно следующим образом.  
  
```  
DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR);  
GO  
```  
  
 В результате все счетчики будут обнулены.  
  
> [!NOTE]  
>  При перезапуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] эти статистические данные не сохраняются. Все данные представляют собой совокупные значения, полученные за время после последнего сброса статистических сведений или со времени запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="latches"></a>Кратковременные блокировки  
 Кратковременная блокировка — это облегченный объект синхронизации, используемый различными компонентами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Кратковременные блокировки используются прежде всего для синхронизации страниц баз данных. Каждая кратковременная блокировка ассоциируется с одной единицей распределения.  
  
 Ожидание кратковременной блокировки происходит в случаях, когда запрос на кратковременную блокировку не может быть удовлетворен немедленно, поскольку эта кратковременная блокировка удерживается другим потоком в конфликтующем режиме. В отличие от обычной блокировки, кратковременная блокировка высвобождается немедленно по завершении операции, даже если это операция записи.  
  
 Кратковременные блокировки группируются в классы по компонентам и по способам использования. В любой момент времени на том или ином экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может существовать любое число кратковременных блокировок определенного класса.  
  
> [!NOTE]  
>  sys.dm_os_latch_stats не отслеживает запросы на кратковременные блокировки, которые были представлены немедленно или которые завершились неудачей без периода ожидания.  
  
 В следующей таблице содержатся краткие описания различных классов кратковременных блокировок.  
  
|Класс кратковременных блокировок|Описание|  
|-----------------|-----------------|  
|ALLOC_CREATE_RINGBUF|Используется внутренними механизмами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для инициализации синхронизации процесса создания кольцевого буфера размещения.|  
|ALLOC_CREATE_FREESPACE_CACHE|Используется для инициализации синхронизации кэшей свободного внутреннего пространства для куч.|  
|ALLOC_CACHE_MANAGER|Используется для синхронизации проверок внутренней связности.|  
|ALLOC_FREESPACE_CACHE|Используется для синхронизации доступа к кэшу страниц со свободным пространством для размещения куч и больших двоичных объектов (BLOBs). Состязание за доступ к кратковременным блокировкам этого класса может происходить в случаях, когда несколько соединений одновременно пытаются ввести строки в кучу или в BLOB. Снизить состязание можно с помощью секционирования соответствующего объекта. Каждая секция имеет собственную кратковременную блокировку. В ходе секционирования вставки будут распределены по нескольким кратковременным блокировкам.|  
|ALLOC_EXTENT_CACHE|Используется для синхронизации доступа к кэшу экстентов, который содержит нераспределенные страницы. Состязание за доступ к кратковременным блокировкам этого класса может происходить в случаях, когда несколько соединений одновременно пытаются выделить страницы данных в одну и ту же единицу распределения. Снизить состязание можно с помощью секционирования объекта, в состав которого входит данная единица распределения.|  
|ACCESS_METHODS_DATASET_PARENT|Используется для синхронизации доступа дочернего набора данных к родительскому набору данных при выполнении параллельных операций.|  
|ACCESS_METHODS_HOBT_FACTORY|Используется для синхронизации доступа к внутренней хэш-таблице.|  
|ACCESS_METHODS_HOBT|Используется для синхронизации доступа к хранимому в памяти представлению HoBt.|  
|ACCESS_METHODS_HOBT_COUNT|Используется для синхронизации доступа к памяти HoBt и к счетчикам строк.|  
|ACCESS_METHODS_HOBT_VIRTUAL_ROOT|Используется для синхронизации доступа к абстракции корневой страницы внутреннего сбалансированного дерева.|  
|ACCESS_METHODS_CACHE_ONLY_HOBT_ALLOC|Используется для синхронизации доступа к рабочим таблицам.|  
|ACCESS_METHODS_BULK_ALLOC|Используется для синхронизации доступа между механизмами массового выделения пространства.|  
|ACCESS_METHODS_SCAN_RANGE_GENERATOR|Используется для синхронизации доступа к генератору диапазонов при выполнении параллельного сканирования.|  
|ACCESS_METHODS_KEY_RANGE_GENERATOR|Используется для синхронизации доступа к операциям упреждающего чтения при выполнении параллельного просмотра важнейших диапазонов.|  
|APPEND_ONLY_STORAGE_INSERT_POINT|Используется для синхронизации вставок в быстродействующие блоки памяти, заполняемые только путем присоединения новых записей.|  
|APPEND_ONLY_STORAGE_FIRST_ALLOC|Используется для синхронизации первого размещения в блоке памяти, заполняемом только путем присоединения новых записей.|  
|APPEND_ONLY_STORAGE_UNIT_MANAGER|Используется для синхронизации доступа к структурам внутренних данных внутри диспетчера быстродействующих блоков памяти, заполняемых только путем присоединения новых записей.|  
|APPEND_ONLY_STORAGE_MANAGER|Используется для синхронизации операций сжатия в диспетчере быстродействующих блоков памяти, заполняемых только путем присоединения новых записей.|  
|BACKUP_RESULT_SET|Используется для синхронизации параллельных резервных копий результирующих наборов.|  
|BACKUP_TAPE_POOL|Используется для синхронизации пулов лент резервных копий.|  
|BACKUP_LOG_REDO|Используется для синхронизации операций повтора журнала резервного копирования.|  
|BACKUP_INSTANCE_ID|Используется для синхронизации создания ID экземпляров счетчиков системного монитора резервного копирования.|  
|BACKUP_MANAGER|Используется для синхронизации внутреннего диспетчера резервного копирования.|  
|BACKUP_MANAGER_DIFFERENTIAL|Используется для синхронизации операций разностных резервных копий с DBCC.|  
|BACKUP_OPERATION|Используется для синхронизации внутренней структуры данных при проведении операций резервного копирования, таких как резервное копирование базы данных, журналов или файлов.|  
|BACKUP_FILE_HANDLE|Используется для синхронизации операций по открытию файлов при выполнении операций восстановления.|  
|BUFFER|Используется для синхронизации краткосрочного доступа к страницам баз данных. Кратковременная блокировка буфера необходима перед считыванием или модификацией любой страницы базы данных. Конфликт кратковременной блокировки буферов может указывать на наличие ряда проблем, в числе которых — «горячие» страницы и низкая производительность подсистемы ввода-вывода.<br /><br /> Этот класс кратковременных блокировок охватывает все возможные способы использования кратковременных блокировок страниц. sys.dm_os_wait_stats устанавливает различие между ожиданиями кратковременных блокировок, вызванных операций ввода-вывода и чтения и записи операций на странице.|  
|BUFFER_POOL_GROW|Используется для синхронизации внутреннего диспетчера буферов при выполнении операций увеличения буферного пула.|  
|DATABASE_CHECKPOINT|Используется для сериализации контрольных точек внутри базы данных.|  
|CLR_PROCEDURE_HASHTABLE|Только для внутреннего применения.|  
|CLR_UDX_STORE|Только для внутреннего применения.|  
|CLR_DATAT_ACCESS|Только для внутреннего применения.|  
|CLR_XVAR_PROXY_LIST|Только для внутреннего применения.|  
|DBCC_CHECK_AGGREGATE|Только для внутреннего применения.|  
|DBCC_CHECK_RESULTSET|Только для внутреннего применения.|  
|DBCC_CHECK_TABLE|Только для внутреннего применения.|  
|DBCC_CHECK_TABLE_INIT|Только для внутреннего применения.|  
|DBCC_CHECK_TRACE_LIST|Только для внутреннего применения.|  
|DBCC_FILE_CHECK_OBJECT|Только для внутреннего применения.|  
|DBCC_PERF|Используется для синхронизации счетчиков внутреннего системного монитора.|  
|DBCC_PFS_STATUS|Только для внутреннего применения.|  
|DBCC_OBJECT_METADATA|Только для внутреннего применения.|  
|DBCC_HASH_DLL|Только для внутреннего применения.|  
|EVENTING_CACHE|Только для внутреннего применения.|  
|FCB|Используется для синхронизации доступа к блоку управления файлами.|  
|FCB_REPLICA|Только для внутреннего применения.|  
|FGCB_ALLOC|Используется для синхронизации доступа к данным, размещенным внутри файловой группы в порядке круговой очереди.|  
|FGCB_ADD_REMOVE|Используйте для синхронизации доступа к файловым группам для add, drop, увеличение и сжатие операций с файлами.|  
|FILEGROUP_MANAGER|Только для внутреннего применения.|  
|FILE_MANAGER|Только для внутреннего применения.|  
|FILESTREAM_FCB|Только для внутреннего применения.|  
|FILESTREAM_FILE_MANAGER|Только для внутреннего применения.|  
|FILESTREAM_GHOST_FILES|Только для внутреннего применения.|  
|FILESTREAM_DFS_ROOT|Только для внутреннего применения.|  
|LOG_MANAGER|Только для внутреннего применения.|  
|FULLTEXT_DOCUMENT_ID|Только для внутреннего применения.|  
|FULLTEXT_DOCUMENT_ID_TRANSACTION|Только для внутреннего применения.|  
|FULLTEXT_DOCUMENT_ID_NOTIFY|Только для внутреннего применения.|  
|FULLTEXT_LOGS|Только для внутреннего применения.|  
|FULLTEXT_CRAWL_LOG|Только для внутреннего применения.|  
|FULLTEXT_ADMIN|Только для внутреннего применения.|  
|FULLTEXT_AMDIN_COMMAND_CACHE|Только для внутреннего применения.|  
|FULLTEXT_LANGUAGE_TABLE|Только для внутреннего применения.|  
|FULLTEXT_CRAWL_DM_LIST|Только для внутреннего применения.|  
|FULLTEXT_CRAWL_CATALOG|Только для внутреннего применения.|  
|FULLTEXT_FILE_MANAGER|Только для внутреннего применения.|  
|DATABASE_MIRRORING_REDO|Только для внутреннего применения.|  
|DATABASE_MIRRORING_SERVER|Только для внутреннего применения.|  
|DATABASE_MIRRORING_CONNECTION|Только для внутреннего применения.|  
|DATABASE_MIRRORING_STREAM|Только для внутреннего применения.|  
|QUERY_OPTIMIZER_VD_MANAGER|Только для внутреннего применения.|  
|QUERY_OPTIMIZER_ID_MANAGER|Только для внутреннего применения.|  
|QUERY_OPTIMIZER_VIEW_REP|Только для внутреннего применения.|  
|RECOVERY_BAD_PAGE_TABLE|Только для внутреннего применения.|  
|RECOVERY_MANAGER|Только для внутреннего применения.|  
|SECURITY_OPERATION_RULE_TABLE|Только для внутреннего применения.|  
|SECURITY_OBJPERM_CACHE|Только для внутреннего применения.|  
|SECURITY_CRYPTO|Только для внутреннего применения.|  
|SECURITY_KEY_RING|Только для внутреннего применения.|  
|SECURITY_KEY_LIST|Только для внутреннего применения.|  
|SERVICE_BROKER_CONNECTION_RECEIVE|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSMISSION|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSMISSION_UPDATE|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSMISSION_STATE|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSMISSION_ERRORS|Только для внутреннего применения.|  
|SSBXmitWork|Только для внутреннего применения.|  
|SERVICE_BROKER_MESSAGE_TRANSMISSION|Только для внутреннего применения.|  
|SERVICE_BROKER_MAP_MANAGER|Только для внутреннего применения.|  
|SERVICE_BROKER_HOST_NAME|Только для внутреннего применения.|  
|SERVICE_BROKER_READ_CACHE|Только для внутреннего применения.|  
|SERVICE_BROKER_WAITFOR_MANAGER| Используется для синхронизации уровня картой экземпляров очередей ожидающий объект. Каждого кортежа идентификатор версии базы данных и идентификатор очереди базы данных имеется одна очередь. Состязание за кратковременную блокировку этого класса может возникнуть при, число подключений: В WAITFOR(RECEIVE) ожидания состояния; вызов WAITFOR(RECEIVE); Превышение времени ожидания WAITFOR; Получение сообщения; Фиксация или откат транзакции, содержащей WAITFOR(RECEIVE); Можно снизить количество конфликтов за счет сокращения числа потоков в состоянии ожидания WAITFOR(RECEIVE). |  
|SERVICE_BROKER_WAITFOR_TRANSACTION_DATA|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSMISSION_TRANSACTION_DATA|Только для внутреннего применения.|  
|SERVICE_BROKER_TRANSPORT|Только для внутреннего применения.|  
|SERVICE_BROKER_MIRROR_ROUTE|Только для внутреннего применения.|  
|TRACE_ID|Только для внутреннего применения.|  
|TRACE_AUDIT_ID|Только для внутреннего применения.|  
|трассировка|Только для внутреннего применения.|  
|TRACE_CONTROLLER|Только для внутреннего применения.|  
|TRACE_EVENT_QUEUE|Только для внутреннего применения.|  
|TRANSACTION_DISTRIBUTED_MARK|Только для внутреннего применения.|  
|TRANSACTION_OUTCOME|Только для внутреннего применения.|  
|NESTING_TRANSACTION_READONLY|Только для внутреннего применения.|  
|NESTING_TRANSACTION_FULL|Только для внутреннего применения.|  
|MSQL_TRANSACTION_MANAGER|Только для внутреннего применения.|  
|DATABASE_AUTONAME_MANAGER|Только для внутреннего применения.|  
|UTILITY_DYNAMIC_VECTOR|Только для внутреннего применения.|  
|UTILITY_SPARSE_BITMAP|Только для внутреннего применения.|  
|UTILITY_DATABASE_DROP|Только для внутреннего применения.|  
|UTILITY_DYNAMIC_MANAGER_VIEW|Только для внутреннего применения.|  
|UTILITY_DEBUG_FILESTREAM|Только для внутреннего применения.|  
|UTILITY_LOCK_INFORMATION|Только для внутреннего применения.|  
|VERSIONING_TRANSACTION|Только для внутреннего применения.|  
|VERSIONING_TRANSACTION_LIST|Только для внутреннего применения.|  
|VERSIONING_TRANSACTION_CHAIN|Только для внутреннего применения.|  
|VERSIONING_STATE|Только для внутреннего применения.|  
|VERSIONING_STATE_CHANGE|Только для внутреннего применения.|  
|KTM_VIRTUAL_CLOCK|Только для внутреннего применения.|  
  
## <a name="see-also"></a>См. также  
 
 [DBCC SQLPERF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [Динамические административные представления, относящиеся к операционной системе SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


