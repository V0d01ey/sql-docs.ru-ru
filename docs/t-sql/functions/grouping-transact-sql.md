---
title: GROUPING (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 01272dedee424cb50c3c0e8e40c9ac92c95ec070
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65942995"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Указывает, является ли указанное выражение столбца в списке GROUP BY статистическим или нет. В результирующем наборе функция GROUPING возвращает 1 (статистическое выражение) или ноль (нестатистическое выражение). Функция GROUPING может использоваться только в предложениях SELECT \<select>, HAVING и ORDER BY, если указано предложение GROUP BY.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Аргументы  
 \<column_expression>  
 Столбец или выражение, которое содержит столбец в предложении [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md).  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING используется, чтобы различать значения NULL, возвращаемые операторами ROLLUP, CUBE или GROUPING SETS, и стандартные значения NULL. Возвращение NULL в качестве результата операции ROLLUP, CUBE или GROUPING SETS является особым случаем использования NULL. Значение служит заполнителем столбца в результирующем наборе и означает «все».  
  
## <a name="examples"></a>Примеры  
 В следующем примере производится группирование `SalesQuota` и статистическая обработка сумм `SaleYTD` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Функция `GROUPING` применяется к столбцу `SalesQuota`.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 В результирующем наборе показаны два значения NULL в `SalesQuota`. Первый `NULL` представляет группу значений NULL из этого столбца в таблице. Второй `NULL` находится в строке итогов, добавленной операцией ROLLUP. Строка итогов содержит суммы `TotalSalesYTD` для всех групп `SalesQuota` и обозначается с помощью `1` в столбце `Grouping`.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>См. также:  
 [GROUPING_ID (Transact-SQL)](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY (Transact-SQL)](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
