---
title: Детерминированные и недетерминированные функции | Документация Майкрософт
ms.custom: ''
ms.date: 08/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d782f8f612d8d4e9eb86a25ddf96e3d147a2f024
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63034874"
---
# <a name="deterministic-and-nondeterministic-functions"></a>Детерминированные и недетерминированные функции
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Детерминированные функции каждый раз возвращают один и тот же результат, если предоставлять им один и тот же набор входных значений и использовать одно и то же состояние базы данных. Недетерминированные функции могут возвращать каждый раз разные результаты, даже если предоставлять им один и тот же набор входных значений и использовать одно и то же состояние базы данных. Например, функция AVG всегда возвращает один результат при указанных выше условиях, а функция GETDATE, возвращающая текущие дату и время, всегда возвращает разный результат.  
  
 Определяемые пользователями функции имеют несколько свойств, определяющих способность ядра [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] индексировать результаты функции как с помощью индексов вычисляемых столбцов, вызывающих функцию, так и с помощью индексированных представлений, которые на нее ссылаются. Детерминизм функции — одно из таких свойств. Например, в представлении нельзя создать кластеризованный индекс, если оно ссылается на какие-либо недетерминированные функции. Дополнительные сведения о свойствах функций, включая детерминизм, см. в разделе [Определяемые пользователем функции](../../relational-databases/user-defined-functions/user-defined-functions.md).  
  
 В этом разделе описан детерминизм встроенных системных функций и их влияние на свойство детерминированности определяемых пользователем функций, если оно содержит вызов расширенных хранимых процедур.  
  
## <a name="built-in-function-determinism"></a>Детерминизм встроенных функций  
 На детерминизм встроенных функций повлиять нельзя. Каждая из них детерминирована или недетерминирована в зависимости от реализации в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Например, если вы укажете в запросе предложение ORDER BY, детерминизм функции, используемой в этом запросе, не изменится.  
  
 Все встроенные строковые функции являются детерминированными. Список этих функций см. в разделе [Строковые функции (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md).  
  
 Следующие встроенные функции, отличные от строковых функций, всегда детерминированы.  
  
||||  
|-|-|-|  
|ABS|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|LOG|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 Следующие функции не всегда детерминированы, их можно использовать в индексированных представлениях или индексах вычисляемых столбцов, если они заданы детерминированным образом.  
  
|Компонент|Комментарии|  
|--------------|--------------|  
|все агрегатные функции|Все агрегатные функции являются детерминированными, если они не указаны с помощью предложения OVER или ORDER BY. Список этих функций см. в разделе [Агрегатные функции (Transact-SQL)](../../t-sql/functions/aggregate-functions-transact-sql.md).|  
|CAST|Детерминированные, за исключением использования их с данными типа **datetime**, **smalldatetime**и **sql_variant**.|  
|CONVERT|Детерминирована, кроме следующих случаев.<br /><br /> <br /><br /> Тип источника — **sql_variant**.<br /><br /> Конечный тип — **sql_variant** , и его исходный тип недетерминирован.<br /><br /> Исходный или конечный тип — **datetime** или **smalldatetime**, другой исходный или конечный тип — строка символов, и задан недетерминированный стиль. Чтобы быть детерминированным, параметр стиля должен быть константой. Кроме того, стили, которые меньше или равны 100, являются недетерминированными, за исключением стилей 20 и 21. Стили более 100 являются детерминированными, за исключением стилей 106, 107, 109 и 113.|  
|CHECKSUM|Детерминирована, за исключением CHECKSUM(*).|  
|ISDATE|Детерминирована, только если используется с функцией CONVERT, при этом параметр стиля CONVERT задан, но не равен 0, 100, 9 или 109.|  
|RAND|Функция RAND детерминирована, только если параметр *seed* определен.|  
  
 Все функции конфигурации, курсора, метаданных, безопасности и системные статистические — недетерминированные. Список этих функций см. в разделе [Функции конфигурации (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md), [Функции работы с курсорами (Transact-SQL)](../../t-sql/functions/cursor-functions-transact-sql.md), [Функции метаданных (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md), [Функции безопасности (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md) и [Системные статистические функции (Transact-SQL)](../../t-sql/functions/system-statistical-functions-transact-sql.md).  
  
 Следующие встроенные функции других классов всегда недетерминированы.  
  
|||  
|-|-|  
|@@CONNECTIONS|GETDATE|  
|@@CPU_BUSY|GETUTCDATE|  
|@@DBTS|GET_TRANSMISSION_STATUS|  
|@@IDLE|LAG|  
|@@IO_BUSY|LAST_VALUE|  
|@@MAX_CONNECTIONS|LEAD|  
|@@PACK_RECEIVED|MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT|NEWID|  
|@@PACKET_ERRORS|NEWSEQUENTIALID|  
|@@TIMETICKS|NEXT VALUE FOR|  
|@@TOTAL_ERRORS|NTILE|  
|@@TOTAL_READ|PARSENAME|  
|@@TOTAL_WRITE|PERCENTILE_CONT|  
|AT TIME ZONE|PERCENTILE_DISC|
|CUME_DIST|PERCENT_RANK|  
|CURRENT_TIMESTAMP|RAND|  
|DENSE_RANK|RANK|  
|FIRST_VALUE|ROW_NUMBER|   
|FORMAT|TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>Вызов расширенной хранимой процедуры из функций  
 Функции, вызывающие расширенные хранимые процедуры, недетерминированы, так как расширенные хранимые процедуры могут оказать на базу данных побочное действие. Побочные действия — это такое изменение глобального состояния базы данных, как обновление таблицы, внешнего сетевого ресурса или файла. Например, к таким действиям можно отнести изменение файла или отправку сообщения по электронной почте. При выполнении расширенной хранимой процедуры из пользовательской функции не следует полагаться на то, что будет возвращен непротиворечивый результирующий набор. Не рекомендуется применять пользовательские функции, которые оказывают побочное действие на базу данных.  
  
 При вызове из функции расширенные хранимые процедуры не могут вернуть клиенту результирующий набор. API-интерфейс любых открытых служб данных, который возвращает результирующие наборы клиенту, имеет код возврата FAIL.  
  
 Расширенная хранимая процедура может подключиться обратно к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Однако процедура не может соединиться с той же транзакцией, что и первоначальная функция, которая вызвала расширенную хранимую процедуру.  
  
 Как и при вызове из пакета или хранимой процедуры, расширенная хранимая процедура выполняется в контексте той учетной записи [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, под которой запущен [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Владелец расширенной хранимой процедуры должен учитывать разрешения в контексте безопасности при предоставлении разрешения на выполнение этой процедуры другим пользователям.  
  
  
