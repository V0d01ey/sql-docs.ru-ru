---
title: MSSQLSERVER_10509 | Документация Майкрософт
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 419b45c688f755d6e5f7cf86154ce6cc527fc6ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048248"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|10509|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|PG_INVALID_STMT|  
|Текст сообщения|Не удалось создать структуру плана '%.\*ls', поскольку инструкция, указанная параметром **@stmt** или **@statement_start_offset** , содержит синтаксическую ошибку или недопустима для использования в структуре плана. Задайте одну допустимую инструкцию [!INCLUDE[tsql](../../includes/tsql-md.md)] или допустимую начальную позицию инструкции внутри пакета. Допустимую начальную позицию можно запросить из столбца statement_start_offset функции динамического управления sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Объяснение  
Инструкция, указанная параметром **@stmt** или **@statement_start_offset** , содержит синтаксическую ошибку или недопустима для использования в структуре плана.  
  
## <a name="user-action"></a>Действие пользователя  
Задайте одну допустимую инструкцию [!INCLUDE[tsql](../../includes/tsql-md.md)] или допустимую начальную позицию инструкции внутри пакета. Допустимую начальную позицию можно запросить из столбца statement_start_offset функции динамического управления sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>См. также:  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Руководства планов](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats (Transact-SQL)](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
