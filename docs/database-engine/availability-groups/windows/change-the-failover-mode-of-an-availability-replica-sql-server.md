---
title: Изменение режима отработки отказа для реплики в группе доступности
description: Описывается, как изменить режим отработки отказа для реплики в группе доступности Always On с помощью Transact-SQL (T-SQL), PowerShell или SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover modes [SQL Server]
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover modes
- Availability Groups [SQL Server], configuring
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: f466fc76d2b960cd5b27eef70dd8a553833c83af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796659"
---
# <a name="change-the-failover-mode-for-a-replica-within-an-always-on-availability-group"></a>Изменение режима отработки отказа для реплики в группе доступности Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В этом разделе описывается изменение режима отработки отказа для реплики доступности в группе доступности AlwaysOn в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]или PowerShell. Режим отработки отказа ― это свойство реплики, которое определяет режим отработки отказа для реплик, работающих в режиме доступности с синхронной фиксацией. Дополнительные сведения см. в разделах [Отработка отказа и режимы отработки отказа (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) и [Режимы доступности (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
## <a name="Prerequisites"></a> Требования и ограничения  
  
-   Эта задача поддерживается только на первичных репликах. Необходимо подключиться к экземпляру сервера, на котором размещена первичная реплика.  
  
-   Экземпляры отказоустойчивого кластера SQL Server не поддерживают автоматический переход на другой ресурс с учетом групп доступности, поэтому любая реплика доступности, размещенная в них, должна быть настроена для перехода на другой ресурс вручную.  
  

##  <a name="Permissions"></a> Permissions  
 Необходимо разрешение ALTER AVAILABILITY GROUP для группы доступности, разрешение CONTROL AVAILABILITY GROUP, разрешение ALTER ANY AVAILABILITY GROUP или разрешение CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 **Изменение режима отработки отказа для реплики доступности**  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена первичная реплика, и разверните дерево сервера.  
  
2.  Разверните узел **Высокий уровень доступности AlwaysOn** и узел **Группы доступности** .  
  
3.  Щелкните группу доступности, реплику которой нужно изменить.  
  
4.  Щелкните правой кнопкой мыши реплику и выберите пункт **Свойства**.  
  
5.  В диалоговом окне **Свойства реплики доступности** используйте раскрывающийся список **Режим отработки отказа** , чтобы изменить режим отработки отказа для этой реплики.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Изменение режима отработки отказа для реплики доступности**  
  
1.  Подключитесь к экземпляру сервера, на котором находится первичная реплика.  
  
2.  Инструкция [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) используется следующим образом:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
      WITH ( {  
           AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }
              | FAILOVER_MODE = { AUTOMATIC | MANUAL }
            }  )
   ```

   В приведенном выше сценарии:

      - *имя_группы* — это имя группы доступности.  
  
      - *имя_сервера* — это имя компьютера или сетевое имя отказоустойчивого кластера. Для именованных экземпляров добавьте "\имя_экземпляра". Используйте имя, на котором размещена реплика, которую требуется изменить.
  
   Дополнительные сведения об этих параметрах см. в разделе [ALTER AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
   В следующем примере для первичной реплики группы доступности *MyAG* режим отработки отказа меняется на автоматический переход на другой ресурс для реплики доступности, находящейся на экземпляре сервера по умолчанию на компьютере *COMPUTER01*.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Использование PowerShell  
 **Изменение режима отработки отказа для реплики доступности**  
  
1.  Перейдите в каталог (**cd**) экземпляра сервера, в котором находится первичная реплика.  
  
2.  Используйте командлет **Set-SqlAvailabilityReplica** с параметром **FailoverMode** . При настройке автоматического перехода на другой ресурс для реплики может потребоваться указать параметр **AvailabilityMode** , чтобы перевести реплику в режим доступности с синхронной фиксацией.  
  
     Например, следующая команда изменяет реплику `MyReplica` в группе доступности `MyAg` , устанавливая использование режима доступности с синхронной фиксацией и поддержку автоматического перехода на другой ресурс.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Чтобы просмотреть синтаксис командлета, воспользуйтесь командлетом **Get-Help** в среде PowerShell [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [Поставщик SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Режимы доступности (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Отработка отказа и режимы отработки отказа (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
