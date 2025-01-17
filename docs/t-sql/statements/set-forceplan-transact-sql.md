---
title: SET FORCEPLAN (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 424f595b2a1fa5d1c55afd003d10fa42ba5b130e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62939904"
---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Если параметр FORCEPLAN установлен в значение ON, оптимизатор запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обрабатывает соединение в порядке появления таблиц в предложении FROM запроса. Кроме того, при установке параметра FORCEPLAN в значение ON принудительно используется вложенный цикл соединения, если для построения плана запроса не требуются другие типы соединений или же они запрашиваются с указаниями соединений или запросов.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 Инструкция SET FORCEPLAN, в сущности, переопределяет логику, используемую в оптимизаторе запросов для обработки инструкции SELECT языка [!INCLUDE[tsql](../../includes/tsql-md.md)]. Данные, возвращаемые инструкцией SELECT, не зависят от этого параметра. Единственное различие — способ обработки таблиц в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], применяемый для выполнения запроса.  
  
 Подсказки оптимизатора запросов могут быть использованы в запросах для изменения способа обработки инструкции SELECT в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Инструкция SET FORCEPLAN применяется на этапе выполнения или запуска, но не на этапе синтаксического анализа.  
  
## <a name="permissions"></a>Разрешения  
 Разрешения SET FORCEPLAN по умолчанию имеют все пользователи.  
  
## <a name="examples"></a>Примеры  
 В следующем примере выполняется соединение четырех таблиц. Параметр `SHOWPLAN_TEXT` включен, поэтому [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] иначе возвращает данные о способе обработки запроса, нежели после включения параметра `SET FORCE_PLAN`.  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL (Transact-SQL)](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT (Transact-SQL)](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
