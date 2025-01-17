---
title: Создание проверочного ограничения | Документация Майкрософт
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98ddc4f21807b9ac5185ad5e510cd83e35bbc93b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62652608"
---
# <a name="create-check-constraints"></a>Создание ограничений CHECK
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  В [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] можно создать в таблице проверочное ограничение, чтобы указать значения данных, допустимые в одном или нескольких столбцах, с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или в [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [безопасность](#Security)  
  
-   **Создание нового проверочного ограничения с помощью следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Требуется разрешение ALTER на таблицу.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-create-a-new-check-constraint"></a>Создание нового проверочного ограничения  
  
1.  В **обозревателе объектов**разверните таблицу, в которую необходимо добавить проверочное ограничение, щелкните правой кнопкой пункт **Ограничения** и выберите команду **Создать ограничение**.  
  
2.  В диалоговом окне **Проверочные ограничения** установите курсор в поле **Выражение** и затем нажмите кнопку с многоточием **(…)** .  
  
3.  В диалоговом окне **Выражение проверочного ограничения** введите выражения SQL, соответствующие проверочному ограничению. Например, чтобы ограничить записи в столбце `SellEndDate` таблицы `Product` значениями, которые больше или равны дате в столбце `SellStartDate` или равны NULL, введите следующее:  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     Чтобы ограничить записи в столбце `zip` записями, состоящими из 5 цифр, введите:  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  Убедитесь, что все нечисловые ограничения по значению заключены в одиночные кавычки (').  
  
4.  Нажмите кнопку **ОК**.  
  
5.  В категории **Идентификация** можно изменить имя проверочного ограничения и добавить описание (расширенное свойство) ограничения.  
  
6.  В категории **Конструктор таблиц** можно задать время принудительного выполнения проверочного ограничения.  
  
    |**Чтобы:**|**Выберите «Да» в следующих полях:**|  
    |-------------|---------------------------------------------|  
    |Проверить ограничение для данных, которые существовали до создания ограничения|**Проверить существующие данные при создании или включении**|  
    |Принудительно применять ограничение при каждой операции репликации данной таблицы|**Принудительное применение для репликации**|  
    |Принудительно применять это ограничение при каждой вставке или обновлении строки таблицы|**Применять для INSERT и UPDATE**|  
  
7.  Щелкните **Закрыть**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-create-a-new-check-constraint"></a>Создание нового проверочного ограничения  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 Дополнительные сведения см. в разделе [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
