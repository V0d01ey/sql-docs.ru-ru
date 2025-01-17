---
title: ENABLE TRIGGER (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 86b23a92006e4a2f3e3896cd1fe20c8b566d14e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62681497"
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Включает триггер DML, DDL или logon.  
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Аргументы  
*schema_name*  
Имя схемы, к которой принадлежит триггер. Аргумент *schema_name* не может указываться для триггеров DDL или триггеров входа.  
  
*trigger_name*  
Имя триггера.  
  
ALL  
Указывает, что включаются все триггеры, определенные в области предложения ON.  
  
*object_name*  
Имя таблицы или представления, для выполнения которых создан триггер DML с именем *trigger_name*.  
  
DATABASE  
Показывает, что триггер DDL *trigger_name* был создан или изменен для выполнения в области базы данных.  
  
ALL SERVER  
**Применимо к**: с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Показывает, что триггер DDL *trigger_name* был создан или изменен для выполнения в области сервера. Параметр ALL SERVER также применяется к триггерам входа.  
  
> [!NOTE]  
>  Этот параметр недоступен в автономной базе данных.  
  
## <a name="remarks"></a>Remarks  
При включении триггера он не создается повторно. Отключенный триггер не может быть запущен, но продолжает существование в виде объекта в текущей базе данных. Включение триггера приводит к его запуску при выполнении любых инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)], на которые он изначально был запрограммирован. Триггеры отключаются с помощью инструкции [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md). Триггеры DML, определенные в таблицах, также можно отключать или включать с помощью [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Разрешения  
Чтобы включить триггер DML, пользователю необходимо, как минимум, обладать разрешением ALTER для таблицы или представления, на которые был создан триггер.  
  
Для включения триггера DDL в области сервера (ON ALL SERVER) или триггера входа пользователю необходимо обладать разрешением CONTROL SERVER на этот сервер. Чтобы включить триггер DDL в области базы данных (ON DATABASE), пользователю необходимо, как минимум, иметь разрешение ALTER ANY DATABASE DDL TRIGGER для текущей базы данных.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. Включение триггера DML для таблицы  
В данном примере отключается триггер `uAddress`, созданный для таблицы `Address` в базе данных AdventureWorks, а затем он включается.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>Б. Включение триггера DDL  
В следующем примере создается триггер DDL `safety` в области базы данных, а затем он отключается и включается.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>В. Включение всех триггеров, определенных в одной области  
В следующем примере включаются все триггеры DDL, созданные в области сервера.  
  
**Применимо к**: с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [DISABLE TRIGGER (Transact-SQL)](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
