---
title: Транзакции (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 56b0fb8ed9eeb0471f623462e34ec5c03fedde5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981390"
---
# <a name="transactions-transact-sql"></a>Транзакции (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Транзакция является единственной единицей работы. Если транзакция выполнена успешно, все модификации данных, сделанные в течение транзакции, принимаются и становятся постоянной частью базы данных. Если в результате выполнения транзакции происходят ошибки и должна быть произведена отмена или выполнен откат, все модификации данных будут отменены.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает в перечисленных ниже режимах транзакций.  
  
 Автоматическое принятие транзакций  
 Каждая отдельная инструкция является транзакцией.  
  
 Явные транзакции  
 Каждая транзакция явно начинается с инструкции BEGIN TRANSACTION и явно заканчивается инструкцией COMMIT или ROLLBACK.  
  
 Неявные транзакции  
 Новая транзакция неявно начинается, когда предыдущая транзакция завершена, но каждая транзакция явно завершается инструкцией COMMIT или ROLLBACK.  
  
 Транзакции контекста пакета  
 Будучи применимой только к множественным активным результирующим наборам (режим MARS), явная или неявная транзакция [!INCLUDE[tsql](../../includes/tsql-md.md)], которая запускается в сеансе режима MARS, становится транзакцией контекста пакета. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] автоматически выполняет откат транзакции контекста пакета, если эта транзакция не зафиксирована или выполнен ее откат при завершении пакета.  

> [!NOTE] 
> Особые замечания, касающиеся хранилища данных, см. в статье [Транзакции (хранилище данных SQL)](transactions-sql-data-warehouse.md).   

## <a name="in-this-section"></a>в этом разделе  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет перечисленные ниже инструкции транзакций.  
  
|||  
|-|-|  
|[BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[COMMIT TRANSACTION](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[SAVE TRANSACTION](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[COMMIT WORK](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>См. также:  
 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
