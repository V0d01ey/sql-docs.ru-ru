---
title: SET NOEXEC (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOEXEC_TSQL
- SET_NOEXEC_TSQL
- SET NOEXEC
- NOEXEC
dev_langs:
- TSQL
helpviewer_keywords:
- queries [SQL Server], compiling
- SET NOEXEC statement
- compiling queries [SQL Server]
- NOEXEC option
ms.assetid: ba56fba1-af9b-4459-b6e4-5d7e71a7630b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4c131cfa111b31f857d3403ed23f2836da237fd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62939909"
---
# <a name="set-noexec-transact-sql"></a>SET NOEXEC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Компилирует каждый запрос, но не выполняет его.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SET NOEXEC { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 Если выполняется инструкция SET NOEXEC ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] компилирует каждый пакет инструкций языка [!INCLUDE[tsql](../../includes/tsql-md.md)], но не выполняет их. Если выполняется инструкция SET NOEXEC OFF, то все пакеты выполняются после компиляции.  
  
 Выполнение инструкций в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] происходит в два этапа: компиляция и собственно выполнение. Этот параметр полезен для проверки синтаксиса и имен объектов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в исходном коде языка [!INCLUDE[tsql](../../includes/tsql-md.md)] при выполнении. Он также полезен для инструкций отладки, которые, как правило, являются частью более крупного пакета инструкций.  
  
 Параметр SET NOEXEC устанавливается на этапе выполнения или запуска, но не на этапе синтаксического анализа.  
  
## <a name="permissions"></a>Разрешения  
 Требуется членство в роли public.  
  
## <a name="examples"></a>Примеры  
 В следующем примере используется инструкция `NOEXEC` с правильным запросом, запрос с некорректным именем объекта и запрос с неверным синтаксисом.  
  
```  
USE AdventureWorks2012;  
GO  
PRINT 'Valid query';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Inner join.  
SELECT e.BusinessEntityID, e.JobTitle, v.Name  
FROM HumanResources.Employee AS e   
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid object name';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Function name uses is a reserved keyword.  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.Values(@BusinessEntityID int)  
RETURNS TABLE  
AS  
RETURN (SELECT PurchaseOrderID, TotalDue  
   FROM dbo.PurchaseOrderHeader  
   WHERE VendorID = @BusinessEntityID);  
  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid syntax';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Built-in function incorrectly invoked.  
SELECT *  
FROM fn_helpcollations;  
-- Reset SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL (Transact-SQL)](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT (Transact-SQL)](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
