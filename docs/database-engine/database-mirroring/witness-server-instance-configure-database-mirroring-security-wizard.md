---
title: Экземпляр следящего сервера (мастер настройки безопасности зеркального отображения баз данных) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.witnsrvr.f1
ms.assetid: b5763663-984a-473b-93a3-6cd3322ad41c
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: e8d038947ac511d9b271fc5b4e07ffabcc47cc96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795066"
---
# <a name="witness-server-instance-configure-database-mirroring-security-wizard"></a>Экземпляр следящего сервера (мастер настройки безопасности зеркального отображения баз данных)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Эта страница используется для задания сведений об экземпляре сервера, служащего в качестве средства слежения за сеансом.  
  
> [!NOTE]
>  Экземпляр следящего сервера доступен не во всех выпусках [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Сведения о функциях, поддерживаемых различными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в статье [Возможности, поддерживаемые выпусками SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 **Настройка зеркального отображения базы данных в среде SQL Server Management Studio**  
  
-   [Создание сеанса зеркального отображения базы данных с использованием проверки подлинности Windows (среда SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Запуск мастера настройки безопасности зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Параметры  
 **Экземпляр следящего сервера**  
 Если экземпляр следящего сервера уже задан (на странице **Зеркальное отображение** диалогового окна **Свойства базы данных** ), то он отображается. Дополнительные сведения см. в разделе [Свойства базы данных (страница "Зеркальное отображение")](../../relational-databases/databases/database-properties-mirroring-page.md).  
  
 В противном случае в этом списке отображается имя текущего сервера. Обратите внимание, что экземпляр следящего сервера не может одновременно быть экземпляром основного или зеркального сервера.  
  
 **Подключить**  
 Если экземпляр следящего сервера не задан, нажмите **Соединить**. При этом выводится диалоговое окно **Соединение с сервером** , в котором можно указать экземпляр сервера и установить с ним соединение.  
  
 Если экземпляр был указан, но мастер не смог установить соединение с разрешениями, достаточными для проверки существования конечной точки, нажмите **Соединить**. При этом выводится диалоговое окно **Соединение с сервером** с предварительно заданным и неизменяемым экземпляром сервера. Укажите учетную запись домена, имеющую достаточные разрешения, и установите соединение с экземпляром сервера.  
  
> [!NOTE]  
>  При подключении к экземпляру сервера мастер настройки безопасности зеркального отображения баз данных использует учетные данные, представленные в диалоговом окне **Соединение с сервером** . Эти учетные данные отличаются от учетных данных сеанса зеркального отображения, использующего учетные данные стартовой учетной записи, в которой экземпляр сервера выполняется как служба.  
  
 **Прослушивающий порт**  
 Поведение этого параметра зависит от того, существует ли конечная точка зеркального отображения для этого экземпляра сервера.  
  
-   Если в экземпляре сервера нет средства прослушивания, в текстовом поле **Порт** в качестве порта отображается порт с номером 5022. Можно ввести любой доступный номер порта, например 7022.  
  
-   Если конечная точка зеркального отображения уже существует, отображается номер порта конечной точки. Если необходимо изменить этот порт, используйте инструкцию ALTER ENDPOINT. Дополнительные сведения см. в статье [ALTER ENDPOINT (Transact-SQL)](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
    > [!NOTE]  
    >  Номер порта обязателен.  
  
 **Имя конечной точки**  
 Если для данного экземпляра сервера существует конечная точка зеркального отображения, то здесь отображается имя конечной точки. Если конечная точка отсутствует, можно задать имя конечной точки.  
  
 **Шифровать данные, проходящие через эту конечную точку**  
 По умолчанию шифрование включено. Если этот параметр включен, шифрование обязательно (а не просто поддерживается), а для всех параметров шифрования используются значения по умолчанию. Дополнительные сведения см. в разделе [CREATE ENDPOINT (Transact-SQL)](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Снимите этот флажок для выключения шифрования. Установите этот флажок, чтобы вновь включить шифрование.  
  
## <a name="see-also"></a>См. также:  
 [Конечная точка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Свойства базы данных (страница "Зеркальное отображение")](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Создание конечной точки зеркального отображения базы данных с проверкой подлинности Windows (Transact-SQL)](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Зеркальное отображение базы данных (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Следящий сервер зеркального отображения базы данных](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
