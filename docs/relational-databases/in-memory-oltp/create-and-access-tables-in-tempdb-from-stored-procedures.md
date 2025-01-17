---
title: Создание таблиц в TempDB и доступ к ним из хранимых процедур | Документация Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fbb29e8e8f694c76ac7fab7340a3f90d7e5c7ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047818"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Создание таблиц в TempDB и доступ к ним из хранимых процедур
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Создание и обращение к таблицам в базе данных TempDB из скомпилированных в собственном коде хранимых процедур не поддерживается. Вместо этого используйте оптимизированные для памяти таблицы с параметром DURABILITY=SCHEMA_ONLY или табличные типы и переменные. 

Дополнительные сведения об оптимизации временных таблиц для памяти и табличных переменных см. в разделе: [Улучшение производительности временной таблицы и табличной переменной с помощью оптимизации памяти](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
  В следующем примере показано, как временную таблицу с тремя столбцами (id, ProductID, Quantity) можно заменить табличной переменной **@OrderQuantityByProduct** типа **dbo.OrderQuantityByProduct**:  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>См. также:  
 [Проблемы миграции, связанные с хранимыми процедурами, скомпилированными в собственном коде](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Конструкции языка Transact-SQL, неподдерживаемые в In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
