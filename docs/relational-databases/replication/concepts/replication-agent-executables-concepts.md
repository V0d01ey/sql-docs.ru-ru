---
title: Основные понятия исполняемых файлов агента репликации | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f02932eff39003f318d2324cce85e51e54a4a77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724552"
---
# <a name="replication-agent-executables-concepts"></a>Основные понятия исполняемых файлов агента репликации
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Управление агентами репликации может осуществляться программным путем следующими способами:  
  
-   использованием управляемых программных интерфейсов агента в пространстве имен <xref:Microsoft.SqlServer.Replication>;  
  
-   вызовом исполняемых файлов агента из командной строки с предоставленным набором параметров.  
  
 Непосредственный вызов агентов репликации из командной строки позволяет использовать агенты для доступа к ним программным путем из пакетных файлов сценариев командной строки. Если агент вызван из командной строки, то выполняется в учетной записи системы безопасности [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows того пользователя, который вызвал агента или запустил пакетный файл.  
  
 С применением исполняемых файлов можно запускать экземпляры следующих агентов репликации.  
  
-   [Агент распространения репликации](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Агент чтения журнала репликации](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 При вызове агентов репликации можно использовать профили производительности для автоматической передачи определенного набора параметров для исполняемого файла агента. Дополнительные сведения см. в статье [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="examples"></a>Примеры  
 В следующих примерах показано, как вызывать агенты репликации из командной строки. Агенты репликации могут быть также вызваны с использованием объектов RMO. Дополнительные сведения см. в статье [Синхронизация подписок (репликация)](../../../relational-databases/replication/synchronize-data.md).  
  
> [!NOTE]  
>  Символы обозначения конца строки в этих примерах были добавлены для повышения удобства чтения. В пакетном файле команды необходимо вводить в одной строке.  
  
### <a name="running-the-snapshot-agent"></a>Управление агентом моментальных снимков  
 Этот пример пакетного файла вызывает агент моментальных снимков из командной строки для создания моментального снимка публикации **AdvWorksSalesOrdersMerge**. (Приведенный ниже скрипт использует путь к файлам [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] (версия 130). Измените его так, чтобы путь к файлам соответствовал вашей версии [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]).  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>Управление агентом распространителя  
 Этот пример пакетного файла вызывает агент распространителя из командной строки для непрерывной репликации изменений из публикации **AdvWorksProductTran** подписчику с принудительной подпиской.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>Управление агентом слияния  
 Этот пример пакетного файла вызывает агент слияния из командной строки для синхронизации подписки по запросу для публикации **AdvWorksSalesOrdersMerge**.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
