---
title: Очистка журналов ошибок агента SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 98433d08b6000fcba73e1d4e06a88b5c529defc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101843"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Очистка журналов ошибок агента SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Эта страница позволяет очистить журналы ошибок агента [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Очистка журнала закрывает текущий журнал ошибок агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и начинает новый журнал ошибок без перезапуска службы агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Учтите, что агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] содержит девять самых последних журналов ошибок. Если в наличии все девять журналов, при очистке журнала ошибок агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] удаляет самый старый журнал.  
  
## <a name="see-also"></a>См. также:  
[Журнал ошибок агента SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
