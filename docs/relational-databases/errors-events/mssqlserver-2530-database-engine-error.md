---
title: MSSQLSERVER_2530 | Документация Майкрософт
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51ed043ddd34d902a989d966ee8f04405a2fbc72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045226"
---
# <a name="mssqlserver2530"></a>MSSQLSERVER_2530
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|2530|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|DBCC_INDEX_IS_OFFLINE|  
|Текст сообщения|Индекс "%.*ls" для таблицы "%.\*ls" помечен как отключенный.|  
  
## <a name="explanation"></a>Объяснение  
Инструкция DBCC не может быть выполнена, так как отключен указанный индекс. После отключения индекс остается в отключенном состоянии до тех пор, пока он не будет перестроен или удален и создан повторно.  
  
## <a name="user-action"></a>Действие пользователя  
  
1.  Включить отключенный индекс одним из следующих способов.  
  
    -   Инструкцией ALTER INDEX с предложением REBUILD.  
  
    -   Инструкцией CREATE INDEX с предложением DROP_EXISTING.  
  
    -   DBCC DBREINDEX  
  
2.  Перезапустить инструкцию DBCC.  
  
## <a name="see-also"></a>См. также:  
[Включение индексов и ограничений](~/relational-databases/indexes/enable-indexes-and-constraints.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[DBCC DBREINDEX (Transact-SQL)](~/t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)  
  
