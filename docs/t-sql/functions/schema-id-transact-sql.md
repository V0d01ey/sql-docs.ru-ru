---
title: SCHEMA_ID (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eefc84ea48372824ecec0617513262998bcc5ad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945348"
---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает идентификатор схемы, связанный с именем схемы.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|----------|----------------|  
|*schema_name*|Имя схемы. Аргумент *schema_name* имеет тип **sysname**. Если аргумент *schema_name* не задан, SCHEMA_ID возвращает идентификатор схемы по умолчанию вызывающего элемента.|  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **int**  
  
 Возвращает NULL, если *schema_name* не является допустимой схемой.  
  
## <a name="remarks"></a>Remarks  
 SCHEMA_ID возвращает идентификаторы системных и пользовательских схем. Функцию SCHEMA_ID можно вызывать в списке выбора, в предложении WHERE и в любом месте, где разрешается выражение.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. Возвращение идентификатора схемы по умолчанию вызывающего объекта  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>Б. Возвращение идентификатора именованной схемы  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>См. также:  
 [Функции метаданных (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME (Transact-SQL)](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas (Transact-SQL)](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

