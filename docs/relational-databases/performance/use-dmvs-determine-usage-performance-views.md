---
title: Использование динамических административных представлений для определения статистики использования и производительности представлений
description: Использование динамических административных представлений для определения статистики использования и производительности представлений
manager: craigg
author: julieMSFT
ms.author: jrasnick
ms.date: 09/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.openlocfilehash: 75563b5dcceead80b5b4d55c07413b37c9d0c278
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299492"
---
# <a name="use-dmvs-to-determine-usage-statistics-and-performance-of-views"></a>Использование динамических административных представлений для определения статистики использования и производительности представлений
В этой статье рассматриваются методы и скрипты, используемые для получения информации о **производительности запросов, которые используют представления**. Цель этих скриптов — предоставить показатели использования и производительности различных представлений, найденных в базе данных. 

## <a name="sysdmexecqueryoptimizerinfo"></a>sys.dm_exec_query_optimizer_info
Динамическое административное представление [sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md) предоставляет статистику об оптимизации, выполняемой оптимизатором запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Эти значения являются накопительными. Их запись начинается при запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения об оптимизации запросов: [Руководство по архитектуре обработки запросов](../../relational-databases/query-processing-architecture-guide.md).   

Приведенное ниже обобщенное табличное выражение (CTE) common_table_expression использует это динамическое административное представление, чтобы предоставить сведения о рабочей нагрузке, например долю запросов, которые ссылаются на представление. Результаты, возвращенные этим запросом, сами по себе не указывают на проблему производительности, но помогают выявлять исходные проблемы в сочетании с жалобами пользователей на запросы с низкой производительностью. 

```sql
WITH CTE_QO AS
(
  SELECT
    occurrence
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    ([counter] = 'optimizations')
),
QOInfo AS
(
  SELECT
    [counter]
    ,[%] = CAST((occurrence * 100.00)/(SELECT occurrence FROM CTE_QO) AS DECIMAL(5, 2))
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    [counter] IN ('optimizations'
                  ,'trivial plan'
                  ,'no plan'
                  ,'search 0'
                  ,'search 1'
                  ,'search 2'
                  ,'timeout'
                  ,'memory limit exceeded'
                  ,'insert stmt'
                  ,'delete stmt'
                  ,'update stmt'
                  ,'merge stmt'
                  ,'contains subquery'
                  ,'view reference'
                  ,'remote query'
                  ,'dynamic cursor request'
                  ,'fast forward cursor request'
             )
)
SELECT
  [optimizations] AS [optimizations %]
  ,[trivial plan] AS [trivial plan %]
  ,[no plan] AS [no plan %]
  ,[search 0] AS [search 0 %]
  ,[search 1] AS [search 1 %]
  ,[search 2] AS [search 2 %]
  ,[timeout] AS [timeout %]
  ,[memory limit exceeded] AS [memory limit exceeded %]
  ,[insert stmt] AS [insert stmt %]
  ,[delete stmt] AS [delete stmt]
  ,[update stmt] AS [update stmt]
  ,[merge stmt] AS [merge stmt]
  ,[contains subquery] AS [contains subquery %]
  ,[view reference] AS [view reference %]
  ,[remote query] AS [remote query %]
  ,[dynamic cursor request] AS [dynamic cursor request %]
  ,[fast forward cursor request] AS [fast forward cursor request %]
FROM
  QOInfo
PIVOT (MAX([%]) FOR [counter] 
  IN ([optimizations]
      ,[trivial plan]
      ,[no plan]
      ,[search 0]
      ,[search 1]
      ,[search 2]
      ,[timeout]
      ,[memory limit exceeded]
      ,[insert stmt]
      ,[delete stmt]
      ,[update stmt]
      ,[merge stmt]
      ,[contains subquery]
      ,[view reference]
      ,[remote query]
      ,[dynamic cursor request]
      ,[fast forward cursor request])) AS p;
GO
```

Объедините результаты этого запроса с результатами системного представления [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md), чтобы определить статистику запросов, текст запроса и кэшированный план выполнения. 

## <a name="sysviews"></a>sys.views
В приведенном ниже обобщенном табличном выражении предоставляются сведения о количестве выполнений, общем времени работы и количестве прочитанных страниц из памяти. На основе результатов можно определить запросы, требующие оптимизации. 
  
> [!NOTE]
> Результаты этого запроса могут различаться в зависимости от используемой версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  


```sql
WITH CTE_VW_STATS AS
(
  SELECT
    SCHEMA_NAME(vw.schema_id) AS schemaname
    ,vw.name AS viewname
    ,vw.object_id AS viewid
  FROM
    sys.views AS vw
  WHERE
    (vw.is_ms_shipped = 0)
  INTERSECT
  SELECT
    SCHEMA_NAME(o.schema_id) AS schemaname
    ,o.Name AS name
    ,st.objectid AS viewid
  FROM
    sys.dm_exec_cached_plans cp
  CROSS APPLY
    sys.dm_exec_sql_text(cp.plan_handle) st
  INNER JOIN
    sys.objects o ON st.[objectid] = o.[object_id]
  WHERE
    st.dbid = DB_ID()
)
SELECT
  vw.schemaname
  ,vw.viewname
  ,vw.viewid
  ,DB_NAME(t.databaseid) AS databasename
  ,t.databaseid
  ,t.*
FROM
  CTE_VW_STATS AS vw
CROSS APPLY
  (
    SELECT
      st.dbid AS databaseid
      ,st.text
      ,qp.query_plan
      ,qs.*
    FROM
      sys.dm_exec_query_stats AS qs
    CROSS APPLY
      sys.dm_exec_sql_text(qs.plan_handle) AS st
    CROSS APPLY
      sys.dm_exec_query_plan(qs.plan_handle) AS qp
    WHERE
      (CHARINDEX(vw.schemaname, st.text, 1) > 0)
      AND (st.dbid = DB_ID())
  ) AS t;
GO
```

## <a name="sysdmvexeccachedplans"></a>sys.dmv_exec_cached_plans
Окончательный запрос предоставляет сведения о неиспользуемых представлениях при помощи динамического административного представления [sys.dmv_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md). Однако кэшированный план выполнения динамический и результаты могут различаться. Таким образом, необходимо использовать этот запрос через какое-то время, чтобы определить, используется ли представление. 

```sql
SELECT
  SCHEMA_NAME(vw.schema_id) AS schemaname
  ,vw.name AS name
  ,vw.object_id AS viewid
FROM
  sys.views AS vw
WHERE
  (vw.is_ms_shipped = 0)
EXCEPT
SELECT
  SCHEMA_NAME(o.schema_id) AS schemaname
  ,o.name AS name
  ,st.objectid AS viewid
FROM
  sys.dm_exec_cached_plans cp
CROSS APPLY
  sys.dm_exec_sql_text(cp.plan_handle) st
INNER JOIN
  sys.objects o ON st.[objectid] = o.[object_id]
WHERE
  st.dbid = DB_ID();
GO
```

## <a name="see-also"></a>См. также раздел
[Динамические административные представления и функции](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 
