---
title: SET CONCAT_NULL_YIELDS_NULL (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fa91003f0afd18372119864175806b4a8b9b6655
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639325"
---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Управляет представлением результатов объединения в виде значений NULL или пустых строковых значений.  
  
> [!IMPORTANT]  
>  В будущей версии параметр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CONCAT_NULL_YIELDS_NULL всегда будет иметь значение ON, а приложения, явно присваивающие ему значение OFF, будут вызывать ошибку. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>Remarks  
 Когда параметр SET CONCAT_NULL_YIELDS_NULL установлен в ON, объединение значения NULL со строкой дает в результате NULL. Например, `SELECT 'abc' + NULL` дает в результате `NULL`. Когда параметр SET CONCAT_NULL_YIELDS_NULL установлен в значение OFF, объединение значения NULL со строкой дает в результате исходную строку (значение NULL рассматривается как пустая строка). Например, `SELECT 'abc' + NULL` дает в результате `abc`.  
  
 Если параметр SET CONCAT_NULL_YIELDS_NULL не задан, применяется параметр **CONCAT_NULL_YIELDS_NULL** базы данных.  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL — это такая же установка, что и установка CONCAT_NULL_YIELDS_NULL для ALTER DATABASE.  
  
 Настройка SET CONCAT_NULL_YIELDS_NULL устанавливается во время выполнения или запуска, но не во время синтаксического анализа.  

Параметр SET CONCAT_NULL_YIELDS_NULL должен быть в состоянии **ON** при создании или изменении представления индексов, индексов в вычисляемых столбцах, отфильтрованных индексов или пространственных индексов. Если параметру SET CONCAT_NULL_YIELDS_NULL задано состояние **OFF**, любое применение инструкций CREATE, UPDATE, INSERT и DELETE к таблицам с индексами на вычисляемых столбцах, отфильтрованным индексам, пространственным индексам или к индексированным представлениям завершится ошибкой. Дополнительные сведения о настройке параметров SET с индексированными представлениями и индексами на вычисляемых столбцах см. в подразделе "Рекомендации по использованию инструкций SET" раздела [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md).
  
 Когда параметр CONCAT_NULL_YIELDS_NULL установлен в OFF, объединение строк через границы сервера становится невозможным.  
  
 Чтобы просмотреть текущее значение для этого параметра, выполните следующий запрос.  
  
```  
DECLARE @CONCAT_NULL_YIELDS_NULL VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_NULL_YIELDS_NULL = 'ON';  
SELECT @CONCAT_NULL_YIELDS_NULL AS CONCAT_NULL_YIELDS_NULL;  
  
```  
  
## <a name="examples"></a>Примеры  
 Следующий пример демонстрирует использование обеих настроек `SET CONCAT_NULL_YIELDS_NULL`.  
  
```  
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY (Transact-SQL)](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
