---
title: Разрешения в Parallel Data Warehouse | Документация Майкрософт
description: В этой статье описываются требования и параметры для управления разрешениями базы данных для Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639514"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Управление разрешениями в Parallel Data Warehouse
В этой статье описываются требования и параметры для управления разрешениями базы данных для SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Основы разрешение ядра базы данных  
Разрешения для ядра СУБД в SQL Server PDW управляются на уровне сервера с помощью имен входа, а также на уровне базы данных с помощью пользователей базы данных и определяемые пользователем роли базы данных.  
  
**Имена входа**  
Имена входа являются учетными записями отдельных пользователей для входа в систему SQL Server PDW. SQL Server PDW поддерживает имена входа с использованием проверки подлинности SQL Server и проверка подлинности Windows.  Имена входа проверки подлинности Windows может быть пользователей Windows или группы Windows из любого домена, который является доверенным для SQL Server PDW. Имена входа SQL Server определяются и проверку подлинности SQL Server PDW и должна быть создана посредством задания пароля.  
  
Членами **sysadmin** предопределенной роли сервера (такие как **sa** входа) можно соединиться с базой данных без необходимости, сопоставляемая с пользователем базы данных. Они сопоставляются **dbo** пользователя. Владелец базы данных также отображаются как **dbo** пользователя.  
  
**Роли сервера**  
Существуют четыре особые роли сервера с помощью набора предварительно настроенных ролей, который представляет собой удобную группу разрешений уровня сервера. **Sysadmin**, **MediumRC**, **LargeRC**, и **XLargeRCfixed** роли сервера являются только роли реализована в SQL Server PDW. **Sa** имя входа является единственным членом **sysadmin** предопределенной роли сервера и дополнительные учетные данные не могут быть добавлены **sysadmin** роли. Имена входа могут быть предоставлены **CONTROL SERVER** разрешение, которое выполняется аналогично, хотя не полностью идентичны, для **sysadmin** предопределенной роли сервера. Используйте [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) для добавления членов в остальных ролей сервера. SQL Server PDW не поддерживает определяемые пользователем роли сервера.  
  
**Пользователей базы данных**  
Имена входа имеют доступ к базе данных путем создания пользователя базы данных в базе данных и сопоставление имени входа этого пользователя базы данных. Как правило, имя пользователя базы данных совпадает с именем входа, хотя это и необязательно. Один пользователь базы данных сопоставляется с одним именем входа. Имя входа может быть сопоставлено только с одним пользователем в базе данных, однако может сопоставляться как пользователь базы данных в нескольких базах данных.  
  
**Предопределенные роли базы данных**  
Предопределенные роли базы данных — это набор предварительно настроенных ролей, который представляет собой удобную группу разрешений уровня базы данных. Пользователи базы данных и определяемые пользователем роли базы данных можно добавить к предопределенной роли базы данных с помощью [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) процедуры. Дополнительные сведения о предопределенных ролей базы данных, см. в разделе [предопределенные роли базы данных](#fixed-database-roles).  
  
**Определяемые пользователем роли базы данных**  
Пользователи с **CREATE ROLE** разрешение можно создать новые роли пользовательскую базу данных для представления групп пользователей с общими разрешениями. Обычно разрешения предоставляются или отклоняются для всей роли, что упрощает управление разрешениями и мониторинг.  
  
Разрешения предоставляются субъектам безопасности (имена входа, пользователей и роли) с помощью **GRANT** инструкции. Разрешения явно отклоняются с помощью **DENY** команды. Ранее предоставленного или Отказано в разрешении удаляется с помощью **ОТОЗВАТЬ** инструкции. Разрешения накапливаются, то есть пользователь получает все разрешения, предоставленные пользователю, имени входа и любой группе, членом которой он является. При этом отклонение разрешения отменяет все предоставленные ранее разрешения. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
В следующем примере представлен типичный и рекомендуемый способ настройки разрешений.  
  
1.  При использовании проверки подлинности Windows, создайте имя входа для каждого пользователя Windows или группы Windows, которые будут подключаться к SQL Server PDW. Если используется проверка подлинности SQL Server, необходимо Создайте имя входа для каждого пользователя, который будет подключаться к SQL Server PDW.  
  
2.  Создание пользователя базы данных для каждого имени входа в все необходимые базы данных.  
  
3.  Создайте одну или несколько ролей пользовательскую базу данных, каждый из которых представляет ту же функцию. Например, финансовый аналитик и аналитик продаж.  
  
4.  Добавьте пользователей базы данных одну или несколько ролей пользовательскую базу данных.  
  
5.  Предоставьте разрешения для определяемых пользователем ролей базы данных.  
  
Имена входа являются объектами уровня сервера и может быть перечислено, просмотрев [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Только разрешения уровня сервера могут предоставляться для участников на уровне сервера.  
  
Пользователи и роли базы данных — это объекты уровня базы данных и может быть перечислено, просмотрев [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Разрешения уровня базы данных могут предоставляться, только для участников базы данных.  
  
## <a name="BackupTypes"></a>Разрешения по умолчанию  
Разрешения по умолчанию приведены в следующем списке:  
  
-   При создании имени входа с помощью директивы using **CREATE LOGIN** инструкция, имя входа получает **CONNECT SQL** разрешение имени входа разрешение на подключение к SQL Server PDW.  
  
-   При создании пользователя базы данных с помощью **CREATE USER** инструкцию, пользователь получает **CONNECT ON DATABASE::** _< имя_базы_данных >_ разрешение, позволяя Имя входа для подключения к базе данных, от имени пользователя.  
  
-   Все субъекты, включая роль PUBLIC, не имеют явных или неявных разрешений по умолчанию неявные разрешения наследуются от явных разрешений. Таким образом при наличии нет явных разрешений, может также существовать отсутствуют неявные разрешения.  
  
-   Если имени входа становится владельцем объекта или базы данных, имя входа всегда имеет все разрешения для объекта или базы данных. Разрешения владельца не отображаются как явные разрешения. **GRANT**, **ОТОЗВАТЬ**, и **DENY** инструкций не оказывают влияния на разрешения владельца. Владельца можно изменить с помощью [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) инструкции.  
  
-   Имя входа sa имеет все разрешения на устройстве. Как и разрешения владельца, полномочий системного администратора не может быть изменено и не отображаются как явные разрешения. **GRANT**, **ОТОЗВАТЬ**, и **DENY** инструкций не оказывают влияния на полномочий системного администратора.  
  
-   Роли сервера PUBLIC получает разрешения не по умолчанию и не наследует разрешения от других ролей сервера. Роли сервера PUBLIC можно предоставить явные разрешения с **GRANT**, **ОТОЗВАТЬ**, и **DENY** инструкций.  
  
-   Транзакции не требуются разрешения. Любой субъект может выполнить **BEGIN TRANSACTION**, **ЗАФИКСИРОВАТЬ**, и **ОТКАТА** команды транзакций. Тем не менее участник должен иметь соответствующие разрешения для выполнения каждой инструкции в транзакции.  
  
-   Для использования инструкции **USE** не требуются разрешения. Любой субъект может выполнить **используйте** инструкции в любой базе данных, однако для доступа к базе данных они должны иметь участника-пользователя в базе данных или гостевой пользователь должен быть активирован.  
  
### <a name="the-public-role"></a>Роли PUBLIC  
Всех новых имен входа устройства автоматически принадлежит роли PUBLIC. Роли сервера PUBLIC имеет следующие характеристики:  
  
-   Роли сервера PUBLIC не имеет разрешений по умолчанию.  
  
-   Все субъекты являются членами роли сервера PUBLIC и роль сервера PUBLIC не является членом другой роли сервера.  
  
-   Роли сервера PUBLIC не может наследовать неявные разрешения. Все разрешения, предоставленные роли PUBLIC должны быть явно предоставлены.  
  
## <a name="BackupProc"></a>Определение разрешений  
Ли имя входа имеет разрешение на выполнение определенного действия зависит от разрешения, предоставленные или отклоненные для имени входа, пользователей и роли, которые пользователь является членом. Разрешения уровня сервера (такие как **CREATE LOGIN** и **VIEW SERVER STATE**) доступны для участников уровня сервера (имена входа). Разрешения на уровне базы данных (таких как **ВЫБЕРИТЕ** из таблицы или **EXECUTE** на процедуру) доступны для участников уровня базы данных (пользователи и роли базы данных).  
  
### <a name="implicit-and-explicit-permissions"></a>Явные и неявные разрешения  
*Явное разрешение* — это разрешение **GRANT** или **DENY**, предоставляемое субъекту с помощью инструкции **GRANT** или **DENY**. Разрешения уровня базы данных, перечислены в [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) представления. Разрешения уровня сервера перечислены в [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) представления.  
  
*Неявное разрешение* — **GRANT** или **DENY** разрешение с наследуемыми субъект (имя входа или роль сервера). Разрешение может быть унаследовано из следующих способов.  
  
-   Субъект может наследовать разрешения от роли, если участник является членом роли, даже если участник не имеет явно **GRANT** или **DENY** разрешение.  
  
-   Субъект может наследовать разрешение на подчиненный объект (например, таблицы), если участник имеет разрешение на одном из объектов родительских областей (например, схема таблицы или разрешение для всей базы данных).  
  
-   Субъект может наследовать разрешение, если разрешение, которое включает подчиненных разрешение. Например **ALTER ANY USER** разрешение включает в себя **CREATE USER** и **ALTER ON USER::** _<name>_ разрешения.  
  
### <a name="determining-permissions-when-performing-actions"></a>При выполнении действий, определение разрешений  
Процесс определения разрешений для назначения субъект является сложным. Сложность возникает при определении неявные разрешения, так как субъекты могут быть членами нескольких ролей и разрешений могут передаваться через несколько уровней в иерархии роли.  
  
Ниже перечислены общие правила для определения разрешений.  
  
-   Владение предполагает разрешение.  
  
    Владелец объекта имеет все разрешения на объект. Аналогичным образом владелец базы данных имеет все разрешения на базы данных, а также все разрешения на объекты в базе данных. Невозможно изменить эти разрешения.  
  
-   Разрешения могут быть унаследованы по нескольким уровням в иерархии членство в роли сервера.  
  
    Например предположим, что у вас есть следующая ситуация:  
  
    -   Дэвид имя входа является членом роли базы данных PerfAnalysts.  
  
    -   PerfAnalysts является членом роли базы данных рабочей среде.  
  
    -   Дэвид и PerfAnalysts не имеют **ВЫБЕРИТЕ** разрешение для таблицы Customer. Разрешение была отозван или предоставлено явно.  
  
    -   Производство имеет **ВЫБЕРИТЕ** разрешение для таблицы Customer.  
  
    В этом случае будет наследовать PerfAnalysts **GRANT** будет наследовать разрешения для таблицы Customer из производства и Дэвид **GRANT** разрешение для таблицы Customer из рабочей среды.  
  
-   **Запретить** переопределяет **GRANT** при разрешения конфликтов.  
  
    Предположим, например, Дэвид имя входа не имеет разрешений на таблицу Customer и является членом двух ролей базы данных-dbgroup1, имеющая **DENY** разрешение для таблицы Customer и dbgroup2, имеющая **GRANT** разрешение для таблицы Customer. В этом случае будет наследовать Дэвид **DENY** разрешение для таблицы Customer. Это происходит ли роли запрошенные их разрешения, явно или неявно.  
  
### <a name="auditing-permissions"></a>Аудит разрешений  
Чтобы выяснить разрешения пользователя, проверьте следующее.  
  
-   Выполните следующий запрос, чтобы определить, какие имена входа являются системными администраторами.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Выполните следующий запрос, чтобы определить, какие имена входа предоставлены явные разрешения.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Выполните следующий запрос в пользовательской базе данных, чтобы определить, какие пользователи базы данных являются членами роли базы данных.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Выполните следующий запрос в пользовательской базе данных, чтобы определить, какие базы данных пользователей и ролей были предоставлены или запрещены конкретные разрешения. Требуется запрос дополнительные представления, такие как sys.objects и sys.schemas, чтобы определить элементы, описанные с major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Рекомендации по обеспечению разрешения базы данных  
  
-   Предоставьте разрешения на самом детальном уровне, практичным. Предоставление разрешений на таблицу или разрешения на уровне представления может стать неуправляемым. Но предоставление разрешений на уровне базы данных может быть слишком широкие права. Если база данных предназначена со схемами для определения границ работы, возможно предоставление разрешения на схему является соответствующие баланс уровне таблицы и уровне базы данных.  
  
-   Предоставление разрешений ролям, а не для пользователей или имена для входа. Управление правами с помощью ролей, а не пользователям позволяет быстро предоставить или отменить набор разрешений для пользователя или имени входа, перемещая их в или из нее роль. По истечении функция от одного лица к другому разрешения могут оставаться без изменений на уровне роли во время изменения членства в роли.  
  
-   Предоставление разрешений ролям, на основе функции задания и в более высокого уровня роли групп, в которых сочетаются функции роли заданий, на основе группы компании, выполнив действия.  
  
-   Каждый пользователь должен иметь уникальное имя входа. Не разрешайте пользователям для совместного использования имен входа. Предоставление имени входа для каждого пользователя гарантирует след аудита и упрощает управление разрешениями.  
  
## <a name="fixed-database-roles"></a>Предопределенные роли базы данных
SQL Server предоставляет предварительно настроенных (фиксированного) роли уровня базы данных помогает управлять разрешениями на сервере. Предварительно настроенных ролей фиксированы, в том, что нельзя изменить разрешения, назначенные им. Можно также создать определяемые пользователем роли базы данных. Можно изменить разрешения, назначенные определяемые пользователем роли базы данных.  
  
Роли являются субъектами безопасности, группирующими других участников. Роли базы данных распространяются от базы данных в своей области разрешений. Пользователи базы данных и других ролей базы данных можно добавить как члены ролей базы данных. Предопределенные роли базы данных невозможно добавить друг с другом. (*Роли* похожи на *группы* в операционной системе Windows.)  
  
Существуют 9 предопределенных ролей базы данных.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>Разрешения предопределенных ролей базы данных  
Система предопределенных ролей сервера и предопределенных ролей базы данных является устаревшей системой, которая была создана в 1980's. Предопределенные роли по-прежнему поддерживаются и полезны в средах, где есть несколько пользователей и требования к безопасности являются простыми. Начиная с SQL Server 2005, была создана более подробные систему предоставление разрешения. Это новая система становится более детализированным, предоставляя больше возможностей для как предоставление и запрет разрешений. Дополнительные осложнения более детализированные системы затрудняет дополнительные, но большинство систем предприятия должны предоставлять разрешений вместо предопределенных ролей. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->На следующем рисунке показана разрешения, которые связаны с каждой предопределенной роли базы данных. Все разрешения на этом графике SQL Server не доступна (или необходимости) в точках доступа.  
  
![Фиксированные роли базы данных безопасности](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>См. также  
  
-   Чтобы создать пользовательские роли, см. в разделе [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Предопределенные роли сервера
Предопределенные роли сервера, автоматически создаваемые SQL Server. SQL Server PDW имеет ограниченная реализация предопределенных ролей сервера SQL Server. Только **sysadmin** и **открытый** иметь имена входа пользователей в качестве членов. **Setupadmin** и **dbcreator** ролей используются внутри SQL Server PDW. Дополнительные члены нельзя добавить или удалить ни из какой роли.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin предопределенной роли сервера  
Члены предопределенной роли сервера **sysadmin** могут выполнять любые действия на сервере. **Sa** имя входа является единственным членом **sysadmin** предопределенной роли сервера. Невозможно добавить дополнительные учетные данные **sysadmin** предопределенной роли сервера. Для предоставления разрешения **CONTROL SERVER** требуется членство в предопределенной роли сервера **sysadmin**. В следующем примере предоставляется **CONTROL SERVER** разрешения для пользователя с именем Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER** разрешение предоставляет практически полный контроль над SQL Server PDW. По возможности предоставьте более детализированных разрешений с именами входа. Например, рассмотрите возможность предоставления **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, или **CREATE ANY DATABASE** разрешения.  
  
### <a name="public-server-role"></a>Роли сервера Public  
Каждое имя входа, который может подключиться к SQL Server PDW является членом **открытый** роли сервера. Все имена входа наследуют разрешения, предоставленные **открытый** для любого объекта. Не назначайте **открытый** разрешений на объект, если объект должен быть доступен для всех пользователей. Нельзя изменить членство в роли **открытый** роли.  
  
> [!NOTE]  
> **открытый** реализуется по-другому, чем другие роли. Так как все участники сервера являются членами public, членство **открытый** роль не указана в **sys.server_role_members** динамического административного Представления.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Vs предопределенной роли сервера. Предоставление разрешений  
Система предопределенных ролей сервера и предопределенных ролей базы данных является устаревшей системой, которая была создана в 1980's. Предопределенные роли по-прежнему поддерживаются и полезны в средах, где есть несколько пользователей и требования к безопасности являются простыми. Начиная с SQL Server 2005, была создана более подробные систему предоставление разрешения. Это новая система становится более детализированным, предоставляя больше возможностей для как предоставление и запрет разрешений. Дополнительные осложнения более детализированные системы затрудняет дополнительные, но большинство систем предприятия должны предоставлять разрешений вместо предопределенных ролей. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>См. также  
  
- [Предоставление разрешений](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

