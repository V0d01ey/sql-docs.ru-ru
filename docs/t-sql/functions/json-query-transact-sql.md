---
title: JSON_QUERY (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: ba0fdffbc354e87419da9d349841d63c38ab794b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65577427"
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

 Извлекает объект или массив из строки JSON.  
  
 Чтобы извлечь скалярное значение, а не объект или массив из строки JSON, см. раздел [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md). Сведения о различиях между **JSON_VALUE** и **JSON_QUERY** см. в разделе [Сравнение JSON_VALUE и JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Аргументы

 *expression*  
 Выражение. Обычно имя переменной или столбца, содержащего текст JSON.  
  
 Если функция **JSON_QUERY** находит код JSON, который не является допустимым в *выражении* перед тем, как она найдет значение, определяемое *путем*, функция возвращает ошибку. Если функция **JSON_QUERY** не находит значение, определяемое *путем*, она просматривает весь текст и возвращает ошибку, если он найдет недопустимый код JSON в любом месте *выражения*.  
  
 *путь*  
 Путь JSON, который указывает объект или массив для извлечения.

В [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] и [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] можно указать переменную в качестве значения *пути*.

В пути JSON можно указать режим синтаксического анализа: нестрогий или строгий режим. Если режим анализа не указан явно, по умолчанию используется нестрогий режим. Дополнительные сведения см. в статье [Выражения пути JSON (SQL Server)](../../relational-databases/json/json-path-expressions-sql-server.md).  

Значение *пути* по умолчанию — '$'. Поэтому если не указать значение для *пути*, **JSON_QUERY** возвращает входное *выражение*.

Если *путь* имеет недопустимый формат, **JSON_QUERY** возвращает ошибку.  
  
## <a name="return-value"></a>Возвращаемое значение

 Возвращает фрагмент JSON типа nvarchar(max). Параметры сортировки для возвращаемого значения совпадают с параметрами сортировки входного выражения.  
  
 Если значение не является объектом или массивом:  
  
- В нестрогом режиме **JSON_QUERY** возвращает значение NULL.  
  
- В строгом режиме **JSON_QUERY** возвращает сообщение об ошибке.  
  
## <a name="remarks"></a>Remarks  

### <a name="lax-mode-and-strict-mode"></a>Нестрогий и строгий режимы

 Рассмотрим следующий текст JSON:  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 В следующей таблице сравнивается поведение **JSON_QUERY** в нестрогом и в строгом режиме. Дополнительные сведения о необязательном режиме пути (строгий или нестрогий) см. в статье [Выражения пути JSON (SQL Server)](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Путь|Возвращаемое значение в нестрогом режиме|Возвращаемое значение в строгом режиме|Дополнительные сведения|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Возвращает весь текст JSON.|Возвращает весь текст JSON.|Недоступно|  
|$.info.type|NULL|Ошибка|Значение не является объектом или массивом.<br /><br /> Используйте **JSON_VALUE**.|  
|$.info.address.town|NULL|Ошибка|Значение не является объектом или массивом.<br /><br /> Используйте **JSON_VALUE**.|  
|$.info."address"|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|Недоступно|  
|$.info.tags|N'[ "Sport", "Water polo"]'|N'[ "Sport", "Water polo"]'|Недоступно|  
|$.info.type[0]|NULL|Ошибка|Не является массивом.|  
|$.info.none|NULL|Ошибка|Свойство не существует.|  

### <a name="using-jsonquery-with-for-json"></a>Использование JSON_QUERY с FOR JSON

**JSON_QUERY** возвращает допустимый фрагмент JSON. Поэтому **FOR JSON** не экранирует специальные символы в возвращаемом значении **JSON_QUERY**.

Если вы возвращаете результаты для FOR JSON и включаете данные, которые уже находятся в формате JSON (в столбце или в результате выражения), оберните данные JSON с помощью **JSON_QUERY** без параметра *путь*.

## <a name="examples"></a>Примеры  
  
### <a name="example-1"></a>Пример 1

 В следующем примере показано, как можно вернуть фрагмент JSON из столбца `CustomFields` в результатах запроса.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>Пример 2

В следующем примере показано, как включить фрагменты JSON в выходные данные предложения FOR JSON.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>См. также раздел

 [Выражения пути JSON (SQL Server)](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Данные JSON (SQL Server)](../../relational-databases/json/json-data-sql-server.md)  
