---
title: Использование политик AlwaysOn для определения работоспособности группы доступности | Документы Майкрософт
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 0c01218cf7303653464814a554771d2ea386f1fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803447"
---
# <a name="use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server"></a>Использование политик AlwaysOn для определения работоспособности группы доступности (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  В этом разделе описано, как определить состояние работоспособности группы доступности AlwaysOn с помощью политики AlwaysOn в среде [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или с помощью PowerShell в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Сведения об управлении на основе политики AlwaysOn см. в разделе [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!IMPORTANT]  
>  При работе с политиками AlwaysOn имена категорий используются в качестве идентификаторов. При изменении имени категории AlwaysOn ее функция оценки работоспособности будет нарушена. Поэтому имена категорий AlwaysOn изменять не следует никогда.  
  
  
  
##  <a name="Permissions"></a> Permissions  
 Требуются разрешения CONNECT, VIEW SERVER STATE и VIEW ANY DEFINITION.  
  
##  <a name="SSMSProcedure"></a> Использование панели мониторинга AlwaysOn  
 **Открытие панели мониторинга AlwaysOn**  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена одна из реплик доступности. Чтобы просмотреть сведения обо всех репликах доступности в группе доступности, используйте экземпляр сервера, на котором размещена первичная реплика.  
  
2.  Щелкните имя сервера, чтобы развернуть дерево сервера.  
  
3.  Разверните узел **Высокий уровень доступности AlwaysOn** .  
  
     Щелкните правой кнопкой мыши узел **Группы доступности** или разверните этот узел и щелкните правой кнопкой мыши определенную группу доступности.  
  
4.  Выберите команду **Показать панель мониторинга** .  
  
 Дополнительные сведения об использовании панели мониторинга AlwaysOn см. в разделе [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md).  
  
##  <a name="PowerShellProcedure"></a> Использование PowerShell  
 **Use Always On policies to view the health of an availability group**  
  
1.  Перейдите в каталог (**cd**) экземпляра сервера, в котором размещена одна из реплик доступности. Чтобы просмотреть сведения обо всех репликах доступности в группе доступности, используйте экземпляр сервера, на котором размещена первичная реплика.  
  
2.  Используйте следующие командлеты.  
  
     **Test-SqlAvailabilityGroup**  
     Оценивает работоспособность группы доступности при помощи оценки состояния политик управления SQL Server. Для выполнения этого командлета необходимо иметь разрешения CONNECT, VIEW SERVER STATE и VIEW ANY DEFINITION.  
  
     Например, следующая команда показывает все группы доступности с состоянием работоспособности «Ошибка» в экземпляре сервера `Computer\Instance`.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     **Test-SqlAvailabilityReplica**  
     Оценивает работоспособность реплик доступности при помощи оценки состояния политик управления SQL Server. Для выполнения этого командлета необходимо иметь разрешения CONNECT, VIEW SERVER STATE и VIEW ANY DEFINITION.  
  
     Например, следующая команда оценивает работоспособность реплики доступности с именем `MyReplica` в группе доступности `MyAg` и выводит краткую сводку.  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     **Test-SqlDatabaseReplicaState**  
     Оценивает работоспособность базы данных доступности на всех присоединенных репликах доступности при помощи оценки состояния политик управления SQL Server.  
  
     Например, следующая команда оценивает работоспособность всех баз данных доступности в группе доступности `MyAg` и выводит краткую сводку по каждой базе данных.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     Эти командлеты принимают следующие параметры.  
  
    |Параметр|Описание|  
    |------------|-----------------|  
    |**AllowUserPolicies**|Выполняет пользовательские политики из категорий политик AlwaysOn.|  
    |**InputObject**|Коллекция объектов, представляющих состояния групп доступности, реплик доступности или базы данных доступности (в зависимости от того, какой используется командлет). Этот командлет вычисляет исправность указанных объектов.|  
    |**NoRefresh**|Если задан этот параметр, командлет не обновляет объекты, указанные в параметре **-Path** или **-InputObject** , вручную.|  
    |**Путь**|Путь к группе доступности, одной или нескольким репликам доступности или состоянию кластера реплики базы данных доступности (в зависимости от того, какой используется командлет). Этот параметр является необязательным. Если этот параметр не указан, его значение по умолчанию соответствует текущему рабочему расположению.|  
    |**ShowPolicyDetails**|Показывает результат оценки каждой политики, выполненной этим командлетом. В результате работы командлета формируется по одному объекту для оценки каждой политики. Каждый такой объект имеет поле с описанием результатов оценки (было установлено соответствие политике или нет, имя и категория политики и так далее).|  
  
     Например, в приведенной ниже команде **Test-SqlAvailabilityGroup** задается параметр **-ShowPolicyDetails** , чтобы показать результат вычисления, выполненного этим командлетом для каждой политики управления на основе политик в группе доступности с именем `MyAg`.  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  Чтобы просмотреть синтаксис командлета, воспользуйтесь командлетом **Get-Help** в среде PowerShell [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [Поставщик SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Получение справок по SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> См. также  
 **Блоги группы разработчиков SQL Server AlwaysOn. Наблюдение за работоспособностью AlwaysOn с помощью PowerShell.**  
  
-   [Часть 1. Общие сведения о командлетах](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
-   [Часть 2. Расширенное использование командлетов](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
-   [Часть 3. Простое приложение для мониторинга](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
-   [Часть 4. Интеграция с агентом SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Администрирование группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Отслеживание групп доступности (SQL Server)](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  


