---
title: Свойства таблицы (SSMS) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.tableproperties.storage.f1
- sql13.swb.tableproperties.changetracking.f1
- sql13.swb.tableproperties.general.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql13.swb.tableproperties.filetable.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5f4b3c22e81f28116fcdaaa83076ff4212b24bf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632030"
---
# <a name="table-properties---ssms"></a>Table Properties - SSMS
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Данный раздел описывает свойства таблицы, отображаемые в диалоговом окне «Свойства таблицы» в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Дополнительные сведения по отображению этих свойств см. в разделе [Просмотр определения таблицы](../../relational-databases/tables/view-the-table-definition.md).  
  
 **В этом разделе**  
  
1.  [Страница «Общие»](#GeneralPage)  
  
2.  [Страница отслеживания изменений](#ChangeTracking)  
  
3.  [Страница FileTable](#FileTable)  
  
4.  [Страница хранилища](#Storage)  
  
##  <a name="GeneralPage"></a> Страница «Общие»  
 **База данных**  
 Имя базы данных, содержащей эту таблицу.  
  
 **Server**  
 Имя текущего экземпляра сервера.  
  
 **Пользователь**  
 Имя пользователя этого соединения.  
  
 **Дата создания**  
 Дата и время создания таблицы.  
  
 **Название**  
 Имя таблицы.  
  
 **Схема**  
 Схема, к которой принадлежит таблица.  
  
 **Системный объект**  
 Указывает, что эта таблица является системной таблицей, используемой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для хранения внутренних данных. Пользователи не должны непосредственно изменять системные таблицы или ссылаться на них.  
  
 **Значения NULL по стандарту ANSI**  
 Показывает, был ли объект создан с параметром ANSI NULL в значении ON. Дополнительные сведения см. в разделе [SET ANSI_NULLS (Transact-SQL)](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 **Заключенный в кавычки идентификатор**  
 Показывает, был ли объект создан с параметром «заключенный в кавычки идентификатор» в значении ON. Дополнительные сведения см. в разделе [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 **Укрупнение блокировки**  
 Указывает укрупнение блокировки гранулярности таблицы. Дополнительные сведения о блокировке в компоненте Database Engine см. в разделе [Руководство по блокировке транзакций и управлению версиями строк SQL Server](https://msdn.microsoft.com/library/jj856598.aspx). Возможны следующие значения:  
  
 AUTO  
 Этот параметр позволяет [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] выбрать степень детализации укрупнения блокировки, подходящую для данной схемы таблицы.  
  
-   Если таблица является секционированной, то укрупнению блокировки будет разрешен доступ к куче или гранулярности сбалансированного дерева. После укрупнения блокировки до уровня HoBT блокировка не будет укрупнена позднее до гранулярности TABLE.  
  
-   Если таблица не секционирована, то блокировка будет укрупняться до гранулярности TABLE.  
  
 TABLE  
 Укрупнение блокировки будет выполняться на уровне гранулярности таблицы независимо от того, секционирована таблица или нет. Значение по умолчанию равно TABLE.  
  
 DISABLE  
 В большинстве случаев предотвращает укрупнение блокировки. Блокировки уровня таблицы запрещены не полностью. Например, при сканировании таблицы, которая не имеет кластеризованного индекса на уровне изоляции SERIALIZABLE, компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] должен установить блокировку таблицы для защиты целостности данных.  
  
 **Таблица реплицирована**  
 Указывает на то, что таблица реплицирована в другую базу данных при помощи репликации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Допустимые значения — **True** или **False**.  
  
##  <a name="ChangeTracking"></a> Страница отслеживания изменений  
 **Отслеживание изменений**  
 Указывает, разрешено ли отслеживание изменений для этой таблицы. Значение по умолчанию равно **False**.  
  
 Этот параметр доступен только в том случае, если отслеживание изменений разрешено для базы данных.  
  
 Чтобы разрешить отслеживание изменений, необходимы наличие в этой таблице первичного ключа и разрешения на ее изменение. Отслеживание изменений может быть настроено при помощи инструкции [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 **Отслеживание обновления столбцов**  
 Указывает, производит ли компонент [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] отслеживание обновлений столбцов.  
  
 Дополнительные сведения об отслеживании изменений см. в статье [Об отслеживании изменений (SQL Server)](../../relational-databases/track-changes/about-change-tracking-sql-server.md).  
  
##  <a name="FileTable"></a> Страница FileTable  
 Отображаются свойства таблицы, относящиеся к таблицам FileTable. Дополнительные сведения см в разделе [FileTables (SQL Server)](../../relational-databases/blob/filetables-sql-server.md).  
  
 **Параметры сортировки столбцов с именами в FileTable**  
 Параметры сортировки, применяемые к столбцу **Имя** в FileTable. Столбец **Name** содержит имена файлов и каталогов.  
  
 **Имя каталога FileTable**  
 Корневая папка для FileTable.  
  
 **Пространство имен FileTable включено**  
 Если это значение равно **True**, значит таблица — FileTable. Если изменить это значение на **False**, FileTable изменяется на обычную пользовательскую таблицу. Если впоследствии потребуется вновь преобразовать таблицу в FileTable, то перед преобразованием таблица должна пройти проверку согласованности FileTable.  
  
##  <a name="Storage"></a> Страница хранилища  
 Отображаются относящиеся к хранению свойства выбранной таблицы.  
  
### <a name="compression"></a>Сжатие  
 **Тип сжатия**  
 Тип сжатия таблицы. Это свойство доступно только для секционированных таблиц. Дополнительные сведения см. в разделе [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
 **Секционирование путем сжатия страниц**  
 Номера секций, в которых используется сжатие страниц. Это свойство доступно только для секционированных таблиц.  
  
 **Секции не сжаты**  
 Номера несжатых секций. Это свойство доступно только для секционированных таблиц.  
  
 **Секционирование, в которых используется сжатие строк**  
 Номера секций, в которых используется сжатие строк. Это свойство доступно только для секционированных таблиц.  
  
### <a name="filegroup"></a>Файловая группа  
 **Текстовая файловая группа**  
 Имя файловой группы, содержащей текстовые данные таблицы.  
  
 **Файловая группа**  
 Имя файловой группы, содержащей таблицу.  
  
 **Таблица секционирована**  
 Допустимые значения — **True** и **False**.  
  
 **Файловая группа файлового потока**  
 Укажите имя файловой группы данных FILESTREAM, если таблица содержит столбец **varbinary(max)** , в котором есть атрибут FILESTREAM. Значение по умолчанию — файловая группа данных FILESTREAM.  
  
 Если таблица не содержит данных FILESTREAM, то это поле пусто.  
  
### <a name="general"></a>Общие  
 **Включен формат хранения Vardecimal**  
 Если задано **True**, это доступное только для чтения значение указывает, что типы данных **decimal** и **numeric** хранятся в формате vardecimal. Изменить его можно параметром **vardecimal storage format** хранимой процедуры [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Формат хранения Vardecimal устарел. Вместо этого используйте сжатие ROW.  
  
 **Место, занимаемое индексом**  
 Объем свободного места в мегабайтах, занимаемого индексами в таблице. Это значение не включает занимаемое XML-индексом пространство для таблицы. Если XML-индексы относятся к таблице, используйте вместо этого процедуру [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .  
  
 **Число строк**  
 Число строк в таблице.  
  
 **Область данных**  
 Объем свободного места в мегабайтах, занимаемого данными в таблице.  
  
### <a name="partitioning"></a>Секционирование  
 Этот раздел доступен только если таблица является секционированной. Дополнительные сведения см. в разделе [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 **Столбец секционирования**  
 Имя столбца, по которому таблица была секционирована.  
  
 **Схема секционирования**  
 Имя схемы секционирования, если таблица является секционированной. Если таблица не секционирована, это поле пусто.  
  
 **Количество секций**  
 Количество секций в таблице.  
  
 **Схема секционирования FILESTREAM**  
 Имя схемы секционирования FILESTREAM, если таблица является секционированной. Если таблица не секционирована, это поле пусто.  
  
 Схема секционирования FILESTREAM должна быть симметрична схеме, указанной в параметре **Схема секционирования** .  
  
## <a name="see-also"></a>См. также:  
 [Просмотр определения таблицы](../../relational-databases/tables/view-the-table-definition.md)   
 [Изменение столбцов (компонент Database Engine)](../../relational-databases/tables/modify-columns-database-engine.md)  
  
  
