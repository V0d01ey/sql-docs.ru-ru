---
title: Заметки о выпуске SQL Server 2016 | Документация Майкрософт
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 63bbff09e8f9d7ca6fa4658369194c9caee26648
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658288"
---
# <a name="sql-server-2016-release-notes"></a>Заметки о выпуске SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  В этой статье описываются ограничения и проблемы, связанные с выпусками SQL Server 2016, включая пакеты обновления. Сведения о новых возможностях см. в разделе [Что нового в SQL Server 2016](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016).

- [![Скачать на странице центра оценки](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Скачать SQL Server 2016 на странице **[центра оценки](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
- [![Маленький значок виртуальной машины Azure](../includes/media/azure-vm.png)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016) Есть ли учетная запись Azure?  Тогда перейдите **[сюда](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016)** , чтобы запустить виртуальную машину с уже установленным SQL Server 2016 с пакетом обновления 1 (SP1).
- [![Скачать SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) Чтобы получить последнюю версию среды SQL Server Management Studio, перейдите на страницу **[Скачивание SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)**.

## <a name="bkmk_2016sp2"></a>SQL Server 2016 с пакетом обновления 2 (SP2)

![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 с пакетом обновления 2 (SP2) включает все накопительные обновления, выпущенные после версии 2016 с пакетом обновления 1 (SP1), вплоть до накопительного пакета обновления 8 включительно.

- [![Центр загрузки Майкрософт](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?linkid=869608) [Скачать SQL Server 2016 с пакетом обновления 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- Полный список обновлений см. в разделе [Сведения о выпуске SQL Server 2016 с пакетом обновления 2 (SP2)](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)

После установки SQL Server 2016 с пакетом обновления 2 (SP2) может потребоваться перезагрузка. Мы рекомендуем запланировать и выполнить перезагрузку после установки SQL Server 2016 с пакетом обновления 2 (SP2).

Улучшения, связанные с производительностью и масштабируемостью, включенные в SQL Server 2016 с пакетом обновления 2 (SP2).

|Компонент|Описание|Дополнительные сведения|
|---|---|---|
|Улучшенная процедура очистки базы данных распространителя |   Превышение размера у таблиц базы данных распространителя приводило к блокировкам и взаимоблокировкам. Улучшенная процедура очистки позволит исключить некоторые из этих сценариев. |   [KB4040276](https://support.microsoft.com/help/4040276/fix-indirect-checkpoints-on-the-tempdb-database-cause-non-yielding)  |
|Очистка отслеживания изменений    |   Усовершенствована и сделана более эффективной очистка в функции отслеживания изменений при работе с ее таблицами.    |   [KB4052129](https://support.microsoft.com//help/4052129/update-for-manual-change-tracking-cleanup-procedure-in-sql-server-2016) |
|Использование времени ожидания ЦП для отмены запроса Resource Governor   |   Улучшена обработка запросов за счет фактической отмены запроса по достижении пороговых значений ЦП для запроса. Такое поведение включается с флагом трассировки 2422. |   [KB4038419](https://support.microsoft.com/help/4038419/add-cpu-timeout-to-resource-governor-request-max-cpu-time-sec)   |
|SELECT INTO для создания целевой таблицы в файловой группе    |   Начиная с SQL Server 2016 с пакетом обновления 2 (SP2), синтаксис T-SQL SELECT INTO поддерживает загрузку таблицы в файловую группу, отличную от файловой группы по умолчанию для пользователя, с помощью ключевого слова ON <Filegroup name> в синтаксисе T-SQL. |       |
|Улучшены косвенные контрольные точки для TempDB    |   Улучшена возможность назначения косвенных контрольных точек, позволяющая свести к минимуму состязания спин-блокировок в DPList. В этом случае рабочая нагрузка TempDB в SQL Server 2016 поддерживает масштабирование без дополнительной настройки, если для TempDB включено назначение косвенных контрольных точек.    |   [KB4040276](https://support.microsoft.com/help/4040276) |
|Повышена производительность резервного копирования баз данных на компьютерах с большим объемом памяти  |   В SQL Server 2016 с пакетом обновления 2 (SP2) оптимизирован процесс выполнения текущих операций ввода-вывода во время резервного копирования, что приводит к существенному повышению производительности резервного копирования небольших и средних баз данных. При создании резервных копий системной базы данных на компьютере с объемом памяти 2 ТБ мы отметили более чем стократное улучшение производительности. Выигрыш в производительности снижается по мере увеличения размера базы данных, так как резервное копирование страниц и операции ввода-вывода для резервного копирования занимают больше времени по сравнению с итерацией буферного пула. Это изменение поможет повысить производительность резервного копирования в средах клиентов с несколькими небольшими базами данных, размещенными на крупных высокопроизводительных серверах с большим объемом памяти.    |       |
|Поддержка сжатия резервных копий VDI для баз данных с включенным прозрачным шифрованием данных   |   В SQL Server 2016 с пакетом обновления 2 (SP2) добавлена поддержка VDI, позволяющая решениям резервного копирования VDI использовать сжатие для баз данных с включенным прозрачным шифрованием данных. В рамках этого улучшения представлен новый формат резервных копий для поддержки сжатия резервных копий у баз данных с включенным прозрачным шифрованием данных. При восстановлении данных из резервных копий ядро SQL Server будет прозрачно обрабатывать новые и старые форматы.   |       |
|Динамическая загрузка параметров для профилей агентов репликации    |   Это новое усовершенствование обеспечивает динамическую загрузку параметров агентов репликации без необходимости перезапуска агента. Оно применяется только к наиболее часто используемым параметрам профилей агентов. |       |
|Поддержка параметра MAXDOP для создания или изменения статистики |    Это улучшение позволяет указывать параметр MAXDOP для инструкции CREATE/UPDATE STATISTICS, а также гарантирует, что при изменении статистики для всех типов индексов в процессе создания или перестроения используется правильный параметр MAXDOP (если таковой имеется).   |   [KB4041809](https://support.microsoft.com/help/4041809) |
|Улучшена функция автоматического обновления для добавочной статистики |    Когда в определенных сценариях происходит ряд изменений в нескольких секциях в таблице, так что значение счетчика общих изменений добавочной статистики превышает пороговое значение автообновления, но ни одна из секций не превышает пороговое значение автообновления, обновление статистики может быть отложено до появления существенно большего количества изменений в таблице. Это поведение исправлено с флагом трассировки 11024.   |       |

Улучшения, относящиеся к обеспечению поддержки и диагностики, включенные в SQL Server 2016 с пакетом обновления 2 (SP2).

|Компонент|Описание|Дополнительные сведения|
|---|---|---|
|Полная поддержка DTC для баз данных в группе доступности    |   Межбазовые транзакции для баз данных, которые входят в группу доступности, сейчас не поддерживаются для SQL Server 2016. С выходом SQL Server 2016 с пакетом обновления 2 (SP2) мы представляем полную поддержку распределенных транзакций для баз данных в группе доступности.   |       |
|Обновление столбца sys.databases is_encrypted для точного отражения состояния шифрования TempDB |   Значение столбца is_encryptedcolumn в представлении sys.databases равно 1 для базы данных TempDB даже после отключения шифрования всех пользовательских баз данных и перезапуска SQL Server. Ожидается, что теперь это значение будет равно 0, так как TempDB больше не шифруется в этой ситуации. Начиная с SQL Server 2016 с пакетом обновления 2 (SP2), sys.databases.is_encrypted точно отражает состояние шифрования для TempDB.  |       |
|Новые параметры DBCC CLONEDATABASE для создания проверенного клона и резервной копии   |   В SQL Server 2016 с пакетом обновления 2 (SP2) у команды DBCC CLONEDATABASE есть два новых параметра: создавать проверенный клон и создавать клон резервной копии. При создании клонированной базы данных с помощью параметра WITH VERIFY_CLONEDB происходит создание и проверка согласованного клона базы данных, который будет поддерживаться корпорацией Майкрософт для использования в рабочей среде. Для проверки того, является ли клон проверенным, предлагается новое свойство — SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone'). Если клон создан с помощью параметра BACKUP_CLONEDB, в одной папке с файлом данных создается резервная копия, что упрощает перемещение клона на другой сервер или его отправку в службу поддержки пользователей Майкрософт (CSS) для устранения неполадок.  |       |
|Поддержка компонента Service Broker (SSB) для DBCC CLONEDATABASE    |   Улучшена команда DBCC CLONEDATABASE для создания скриптов объектов SSB.  |   [KB4092075](https://support.microsoft.com/help/4092075) |
|Новое динамическое административное представление (DMV) для наблюдения за использованием пространства хранилища версий TempDB    |   В SQL Server 2016 с пакетом обновления 2 (SP2) добавлено новое представление DMV sys.dm_tran_version_store_space_usage для наблюдения за использованием пространства хранилища версий TempDB. Теперь администраторы баз данных могут заранее планировать изменение размера базы данных TempDB на основе требований к использованию хранилища версий для каждой работающей на производственных серверах базы данных без потери производительности. |       |
|Поддержка полных дампов для агентов репликации | Если агенты репликации сталкиваются сейчас с необработанным исключением, они по умолчанию создают мини-дамп симптомов исключения. Это значительно усложняет процедуру устранения неполадок с необработанными исключениями. С этим изменением мы представляем новый раздел реестра, который позволит создавать полный дамп для агентов репликации.  |       |
|Усовершенствование расширенных событий при ошибке маршрутизации для чтения для группы доступности |   Ранее событие xEvent read_only_rout_fail возникало при наличии списка маршрутизации, если в нем не было серверов, доступных для подключения. С выходом SQL Server 2016 с пакетом обновления 2 (SP2) вы получите дополнительную информацию для более эффективного устранения неполадок, а также развернутые сведения о точках в коде, где возникает это событие XEvent.  |       |
|Новое динамическое административное представление для отслеживания журнала транзакций |   Добавлено новое динамическое административное представление sys.dm_db_log_stats, которое возвращает сводные атрибуты и сведения о файлах журнала транзакций для баз данных. |       |
|Новое динамическое административное представление (DMV) для наблюдения за сведениями виртуального файла журнала |   В SQL Server 2016 с пакетом обновления 2 (SP2) добавлено новое представление DMV sys.dm_db_log_info для предоставления сведений о виртуальных файлах журнала (аналогично DBCC LOGINFO) для отслеживания возможных проблем с журналами транзакций, оповещения об этих проблемах и их предотвращения.    |       |
|Сведения о процессоре в представлении sys.dm_os_sys_info|   В представление DMV sys.dm_os_sys_info добавлены новые столбцы для предоставления относящихся к процессору сведений, таких как socket_count и cores_per_numa.  |       |
|Сведения об измененных экстентах в представлении sys.dm_db_file_space_usage| В представление sys.dm_db_file_space_usage добавлен новый столбец для отслеживания количества экстентов, измененных с момента последнего полного резервного копирования.  |       |
|Сведения о сегментах в представлении sys.dm_exec_query_stats |   В представление sys.dm_exec_query_stats были добавлены новые столбцы, такие как total_columnstore_segment_reads и total_columnstore_segment_skips, для отслеживания количества пропущенных и считанных сегментов columnstore.   |   [KB4051358](https://support.microsoft.com/help/4051358) |
|Установка правильного уровня совместимости для базы данных распространителя  |   После установки пакета обновления уровень совместимости базы данных распространителя менялся на 90. Это происходило из-за пути к коду в хранимой процедуре sp_vupgrade_replication. Теперь пакет обновления задает корректный уровень совместимости для базы данных распространителя.   |       |
|Предоставление сведений о последнем успешном выполнении инструкции DBCC CHECKDB    |   Добавлен новый параметр базы данных для программного возвращения даты последнего успешного выполнения инструкции DBCC CHECKDB. Пользователи теперь могут выполнить запрос DATABASEPROPERTYEX([база данных], 'lastgoodcheckdbtime'), чтобы получить единое значение, представляющее дату и время последнего успешного выполнения инструкции DBCC CHECKDB в указанной базе данных.  |       |
|Усовершенствования Showplan XML| [Сведения, на основании которых статистика использовалась для компиляции плана запроса](https://blogs.msdn.microsoft.com/sql_server_team/sql-server-2017-showplan-enhancements/), включая имя статистики, счетчик изменений, процент выборки и время последнего обновления статистики. Обратите внимание, что эта возможность добавлена только для моделей CE 120 и более поздних версий. Так, она не поддерживается для CE 70.| |
| |Если оптимизатор запросов использует логику "цель строки" (или целевое число строк), в Showplan XML добавляется новый атрибут [EstimateRowsWithoutRowgoal](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-row-goal/).| |
| |В реальный Showplan XML добавлены новые атрибуты среды выполнения [UdfCpuTime и UdfElapsedTime](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-udfs/) для отслеживания времени, прошедшего в скалярных определяемых пользователем функциях.| |
| |В реальном Showplan XML в [список 10 ведущих возможных ожиданий](https://blogs.msdn.microsoft.com/sql_server_team/new-showplan-enhancements/) добавлен тип ожидания CXPACKET — при параллельном выполнении запросов часто используются ожидания CXPACKET, но этот тип ожидания не упоминался в реальном Showplan XML. |       |
| |Расширено предупреждение о сбросе среды выполнения. Теперь в нем указывается количество страниц, записанных в базу данных TempDB во время сброса оператора параллелизма.| |
|Поддержка репликации для баз данных с параметрами сортировки дополнительных символов  |   Теперь репликация поддерживается в базах данных, использующих параметры сортировки дополнительных символов. |       |
|Улучшенное взаимодействие с Service Broker при отработке отказа группы доступности |   В текущей реализации, если компонент Service Broker включен для баз данных группы доступности, во время отработки отказа группы доступности все подключения Service Broker, созданные в первичной реплике, остаются открытыми. Теперь во время отработки отказа группы доступности такие открытые подключения будут закрыты. |       |
|Улучшено устранение неполадок ожиданий параллелизма |   за счет добавления нового ожидания [CXCONSUMER](https://blogs.msdn.microsoft.com/sql_server_team/making-parallelism-waits-actionable/).   |       |
|Улучшена согласованность между динамическими административными представлениями (DMV) для предоставления одинаковых сведений |   Теперь представление DMV sys.dm_exec_session_wait_stats отслеживает ожидания CXPACKET и CXCONSUMER согласованно с представлением DMV sys.dm_os_wait_stats. |       |
|Улучшено устранение неполадок взаимоблокировок параллелизма внутри запроса | Новое расширенное событие exchange_spill для предоставления сведений о количестве страниц, записанных в базу данных TempDB во время сброса оператора параллелизма, в поле xEvent worktable_physical_writes.| |
| |Теперь столбцы сбросов (например, total_spills) в представлениях DMV sys.dm_exec_query_stats, sys.dm_exec_procedure_stats и sys.dm_exec_trigger_stats также содержат данные, сброшенные операторами параллелизма.| |
| |Улучшен граф взаимоблокировок XML для сценариев взаимоблокировки параллелизма. В ресурс exchangeEvent добавлены дополнительные атрибуты.| |
| |Улучшен граф взаимоблокировок XML для взаимоблокировок, использующих операторы пакетного режима. В ресурс SyncPoint добавлены дополнительные атрибуты.| |
|Динамическая перезагрузка некоторых параметров профилей агентов репликации |   В текущей реализации агентов репликации для любого изменения параметра профиля агента требуется остановить и перезапустить агент. Эти улучшения позволяют выполнять динамическую перезагрузку параметров без перезапуска агента репликации.   |       |

![horizontal-bar.png](media/horizontal-bar.png)

## <a name="bkmk_2016sp1"></a>SQL Server 2016 с пакетом обновления 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) В SQL Server 2016 с пакетом обновления 1 (SP1) входят все накопительные пакеты обновления вплоть до накопительного пакета обновления 3 для SQL Server 2016 RTM, включая обновление для системы безопасности MS16-136. Этот выпуск содержит все исправления из накопительных пакетов обновления для SQL Server 2016 до накопительного пакета обновления 3 включительно, а также обновление для системы безопасности MS16-136, выпущенное 8 ноября 2016 г.

В выпусках Standard, Web, Express и Local DB продукта SQL Server с пакетом обновления 1 (SP1) доступны следующие функции (если не указано иное):
- Always Encrypted
- Отслеживание измененных данных (недоступно в выпуске Express)
- columnstore
- Сжатие
- Динамическое маскирование данных
- Аудит мелких фрагментов данных
- Выполняющаяся в памяти OLTP (недоступна в выпуске Local DB)
- Несколько контейнеров файлового потока (недоступно в выпуске Local DB)
- Секционирование
- PolyBase
- Безопасность на уровне строк

В приведенной ниже таблице представлена сводка основных улучшений в SQL Server 2016 с пакетом обновления 1 (SP1).

|Компонент|Описание|Дополнительные сведения|
|---|---|---|
|Массовая вставка в кучи с автоматическим использованием указания TABLOCK, если установлен флаг трассировки 715| Флаг трассировки 715 включает блокировку таблицы для операций массовой загрузки в кучу без некластеризованных индексов.|[Перенос рабочих нагрузок SAP в SQL Server производится в 2,5 раза быстрее](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE или ALTER|Развертывание объектов, таких как хранимые процедуры, триггеры, определяемые пользователем функции и представления.|[Блог по ядру СУБД SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|Поддержка DROP TABLE для репликации|Поддержка DROP TABLE DDL для репликации позволяет удалять статьи репликации.|[Статья базы знаний 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Подписывание драйвера RsFx файлового потока|Драйвер RsFx файлового потока подписывается и сертифицируется с помощью портала "Информационная панель Центра разработки оборудования для Windows" (портал разработчика), что позволяет без проблем устанавливать драйвер RsFx файлового потока для SQL Server 2016 с пакетом обновления 1 (SP1) в ОС Windows Server 2016 и Windows 10.|[Перенос рабочих нагрузок SAP в SQL Server производится в 2,5 раза быстрее](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|Разрешение LPIM в учетной записи службы SQL — программное определение|Администраторы баз данных могут программно определять, действует ли разрешение "Блокировка страниц в памяти" (LPIM) во время запуска службы.|[Developers Choice: программное определение наличия разрешений LPIM и IFI в SQL Server](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|Очистка отслеживания изменений вручную|Новая хранимая процедура очищает внутреннюю таблицу отслеживания изменений по требованию.| [Статья базы знаний 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|Параллельные изменения INSERT..SELECT в локальных временных таблицах|Новые параллельные операции INSERT в INSERT..SELECT.|[Группа консультантов по SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|Расширенная диагностика, включающая предупреждение о временно предоставляемом буфере памяти, сведения о максимальном объеме памяти, предоставляемом для запроса, установленных флагах трассировки, а также другие диагностические данные. | [Статья базы знаний 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|Память класса хранилища|Ускорьте обработку транзакций с помощью памяти класса хранилища в Windows Server 2016, которая позволяет на порядок сократить время фиксации транзакций.|[Блог по ядру СУБД SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|Используйте параметр запроса `OPTION(USE HINT('<option>'))` для изменения поведения оптимизатора запросов с помощью поддерживаемых указаний уровня запроса. В отличие от QUERYTRACEON, параметр USE HINT не требует привилегий администратора.|[Developers Choice: указания запросов USE HINT](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|Дополнения XEvent|Возможности диагностики, предоставляемые новыми расширенными событиями и счетчиками производительности, позволяют более эффективно устранять задержки.|[Расширенные события](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

Кроме того, обратите внимание на указанные ниже исправления.
- На основе отзывов администраторов баз данных и участников сообщества SQL начиная с SQL Server 2016 с пакетом обновления 1 (SP1) сообщения журнала, связанные с Hekaton, сведены к минимуму.
- Ознакомьтесь с новыми [флагами трассировки](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).
- Полные версии образцов баз данных WideWorldImporters работают с выпусками Standard и Express начиная с SQL Server 2016 с пакетом обновления 1 (SP1) и доступны в [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0). Вносить изменения в образцы не требуется. Резервные копии баз данных, созданные в версии RTM выпуска Enterprise, работают с выпусками Standard и Express в SQL Server 2016 с пакетом обновления 1 (SP1).

После установки SQL Server 2016 с пакетом обновления 1 (SP1) может потребоваться перезагрузка. Мы рекомендуем запланировать и выполнить перезагрузку после установки SQL Server 2016 с пакетом обновления 1 (SP1).

### <a name="download-pages-and-more-information"></a>Страницы загрузки и дополнительные сведения

- [Скачать пакет обновления 1 (SP1) для Microsoft SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=54276)
- [Выпущен SQL Server 2016 с пакетом обновления 1 (SP1)](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [Сведения о выпуске SQL Server 2016 с пакетом обновления 1 (SP1)](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) В [Центре обновления SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) можно найти ссылки и сведения для всех поддерживаемых версий, включая пакеты обновления для [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]

![horizontal-bar.png](media/horizontal-bar.png)

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Ядро СУБД (общедоступная версия)](#bkmk_ga_instalpatch)
-   [Stretch Database (общедоступная версия)](#bkmk_ga_stretch)
-   [Хранилище запросов (общедоступная версия)](#bkmk_ga_query_store)
-   [Документация по продукту (общедоступная версия)](#bkmk_ga_docs)

### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA)
**Проблема и последствия для клиентов**: корпорация Майкрософт выявила проблему с двоичными файлами среды выполнения Microsoft VC++ 2013, которые SQL Server 2016 устанавливает в качестве необходимого компонента. Для исправления этой проблемы выпущено обновление. Если это обновление двоичных файлов среды выполнения VC не установлено, в SQL Server 2016 могут возникать проблемы с надежностью в определенных сценариях. Перед установкой SQL Server 2016 проверьте, требуется ли на вашем компьютере исправление, описываемое в статье [KB 3164398](https://support.microsoft.com/kb/3164398). Обновление также включено в [накопительный пакет обновления 1 (CU1) для SQL Server 2016 RTM](https://www.microsoft.com/download/details.aspx?id=53338).

**Решение.** Используйте одно из следующих решений:

- Установите [обновление для Visual C++ 2013 и распространяемого пакета Visual C++ из статьи KB 3138367](https://support.microsoft.com/kb/3138367). Использование статьи KB является предпочтительным решением. Обновление можно установить до или после установки SQL Server 2016.

    Если SQL Server 2016 уже установлен, выполните по порядку указанные ниже действия.

    1.  Скачайте соответствующий файл *vcredist_\*exe*.
    1.  Остановите службу SQL Server для всех экземпляров ядра СУБД.
    1.  Установите обновление **KB 3138367**.
    1.  Перезагрузите компьютер.


 - Установите  [критическое обновление для необходимых компонентов MSVCRT в SQL Server 2016, KB 3164398](https://support.microsoft.com/kb/3164398).

    Обновление **KB 3164398**можно установить во время установки SQL Server, из Центра обновления Майкрософт или из Центра загрузки Майкрософт.

    - **Во время установки SQL Server 2016**: если у компьютера, на котором запущена программа установки SQL Server, есть доступ к Интернету, программа установки SQL Server проверяет наличие обновления в процессе своего выполнения. Если вы подтвердите обновление, программа установки скачивает и обновляет двоичные файлы во время установки.

    - **Центр обновления Майкрософт**: обновление доступно в Центре обновления Майкрософт как критически важное обновление SQL Server 2016, не связанное с системой безопасности. После установки обновления через Центр обновления Майкрософт SQL Server 2016 потребует перезапустить сервер.

    - **Центр загрузки**: наконец-то обновление доступно в Центре загрузки Майкрософт. Вы можете скачать программный пакет обновления и установить его на серверах после установки SQL Server 2016.


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>Проблема с определенным символом в имени базы данных или таблицы

**Проблема и последствия для клиентов**: попытка включить Stretch Database в базе данных или таблице завершается ошибкой. Эта проблема возникает, если имя объекта содержит символ, который при преобразовании из нижнего в верхний регистр считается другим символом. Примером символа, вызывающего эту проблему, может служить символ "ƒ" (который вводится с помощью кода ALT+159).

**Решение:** если вы хотите включить Stretch Database для базы данных или таблицы, единственным выходом является переименование объекта с целью удалить проблемный символ.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>Проблема с индексом, в котором используется ключевое слово INCLUDE

**Проблема и последствия для клиентов**: при попытке включить Stretch Database для таблицы с индексом, в котором используется ключевое слово INCLUDE для включения в индекс дополнительных столбцов, происходит ошибка.

**Решение:** удалите индекс, в котором используется ключевое слово INCLUDE, включите Stretch Database для таблицы, а затем снова создайте индекс. При этом следует соблюдать принятые в организации правила и политики обслуживания, чтобы влияние на работу пользователей таблицы было минимальным или нулевым.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Проблема с автоматической очисткой данных в выпусках, отличных от Enterprise и Developer

 **Проблема и последствия для клиентов**: автоматическая очистка данных завершается сбоем в выпусках, отличных от Enterprise и Developer.
Поэтому, если не очищать данные вручную, пространство, используемое хранилищем запросов, с течением времени будет расти, пока не будет достигнуто настроенное предельное значение. Если эту проблему не решить, она также приведет к заполнению дискового пространства, выделенного для журналов ошибок, так как при каждой попытке очистки создается файл дампа. Период активации очистки зависит от частоты рабочей нагрузки, но не превышает 15 минут.

 **Решение:** если вы планируете использовать хранилище запросов в выпусках, отличных от Enterprise и Developer, необходимо явно отключить политики очистки. Это можно сделать либо в среде SQL Server Management Studio (на странице "Свойства базы данных"), либо с помощью скрипта Transact-SQL:

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

Кроме того, рассмотрите варианты ручной очистки, чтобы избежать перехода хранилища запросов в режим "только для чтения". Например, выполняйте следующий запрос для периодической очистки всего дискового пространства:

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

Кроме того, периодически выполняйте следующие процедуры хранилища запросов для очистки статистики времени выполнения, определенных запросов или планов:

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> Документация по продукту (общедоступная версия)
 **Проблема и последствия для клиентов**: скачиваемая версия документации по SQL Server 2016 пока не доступна. При использовании диспетчера библиотек справки для **установки содержимого из Интернета** вы увидите документацию по SQL Server 2012 и SQL Sever 2014, но не увидите документацию по SQL Server 2016.

 **Решение:** используйте один из описанных ниже способов.

 ![Управление параметрами справки для SQL Server](../sql-server/media/docs-sql2016-managehelpsettings.png "Управление параметрами справки для SQL Server")

-   Используйте вариант **Выбрать справку в сети или локальную справку** и настройте справку для "Я хочу использовать справку в сети".

-   Используйте вариант **Установить содержимое из сети** и загрузите содержимое SQL Server 2014.

 **Справка F1**: при нажатии клавиши F1 в [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] в браузере открывается веб-версия статьи справки F1. Проблема связана со справкой на основе браузера даже в том случае, если настроена или установлена локальная справка.

**Обновление содержимого**: В SQL Server Management Studio и Visual Studio окно справки может перестать отвечать на запросы во время добавления документации. Чтобы устранить эту проблему, выполните указанные ниже действия. Сведения об этой проблеме см. в разделе [Окно справки Visual Studio зависает](https://msdn.microsoft.com/library/mt654096.aspx).

* Откройте файл %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings в Блокноте и измените дату в приведенном ниже коде на какую-либо дату в будущем.

```
     Cache LastRefreshed="12/31/2017 00:00:00"
```

## <a name="additional-information"></a>Дополнительные сведения
+ [Установка SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [Ссылки и сведения для всех поддерживаемых версий в Центре обновления SQL Server](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")
