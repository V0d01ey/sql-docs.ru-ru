---
title: Базы данных master - Parallel Data Warehouse | Документация Майкрософт
description: Дополнительные сведения о базе данных master в Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213295"
---
# <a name="master-database---parallel-data-warehouse"></a>Базы данных master - Parallel Data Warehouse
Базы данных master SQL Server PDW хранит данные для входа на уровне устройства и каталоге базы данных. Это база данных master SQL Server, находится на узле управления. Таким образом он предоставляет аналогичную функциональность для SQL Server PDW как главный обеспечивает для SQL Server.  
  
Дополнительные сведения о системных баз данных, см. в разделе [системных баз данных](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Ограничения  
Ниже перечислены операции, которые невозможно выполнить в базе данных master SQL Server PDW.  
  
Вы *нельзя:*  
  
-   Выполните разностной резервной копии базы данных master.  
  
-   Создайте пользовательские объекты в базе данных master.  
  
-   Изменение параметров сортировки базы данных master.  
  
-   Измените владельца базы данных master.  
  
-   Удалите или переименуйте master.  
  
-   Измените разрешения в главную ветвь.  
  
-   Выполнение **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Задача|Описание|  
|--------|---------------|  
|Создание полной резервной копии базы данных master.|Пример<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Дополнительные сведения см. в разделе [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Восстановление базы данных master|Чтобы восстановить базу данных master, используйте [восстановление базы данных Master](restore-the-master-database.md) страницу в средство Configuration Manager.|  
|Просмотр сведений о каталоге базы данных.|`SELECT * FROM master.sys.databases;`|  
|Просмотр системных сведений для входа и разрешения.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
