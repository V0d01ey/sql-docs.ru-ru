---
title: Скрытие экземпляра компонента SQL Server Database Engine | Документы Майкрософт
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 5401e5b731f09de89dedeef8308b7118299fbc9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785273"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>Скрытие экземпляра компонента SQL Server Database Engine
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В этом разделе описано, как скрыть экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью диспетчера конфигурации SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] служба браузера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] используется для перечисления экземпляров компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] , установленных на компьютере. Это позволяет клиентскому приложению просмотреть сервер, а клиентам поможет отличить друг от друга экземпляры компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] на одном и том же компьютере. Чтобы служба обозревателя SQL Server не открывала экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] для клиентских компьютеров, которые пытаются найти экземпляр с помощью кнопки **Обзор** , воспользуйтесь следующей процедурой.  
  
##  <a name="SSMSProcedure"></a> Использование диспетчера конфигурации SQL Server  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>Скрытие экземпляра компонента SQL Server Database Engine  
  
1.  В **диспетчере конфигурации SQL Server** разверните узел **Сетевая конфигурация SQL Server**, щелкните правой кнопкой мыши элемент **Протоколы для** *\<экземпляр сервера>* и выберите пункт **Свойства**.  
  
2.  На вкладке **Флаги** в диалоговом окне **Скрыть экземпляр** выберите **Да**и затем закройте диалоговое окно, нажав кнопку **ОК** . Изменения вступят в силу немедленно для новых соединений.  
  
## <a name="remarks"></a>Remarks  
 Если скрыть именованный экземпляр, необходимо будет указать номер порта в строке подключения, чтобы соединиться со скрытым экземпляром, даже если служба браузера запущена. Для именованного скрытого экземпляра рекомендуется использовать статический порт вместо динамического.  
  Дополнительные сведения см. в разделе [Настройка сервера для прослушивания указанного TCP-порта (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="clustering"></a>Кластеризация  
 Если скрыть кластеризованный именованный экземпляр, у службы кластеров могут возникнуть проблемы с подключением к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Это приведет к тому, что проверка **IsAlive** экземпляра кластера не будет выполнена и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] перейдет в автономный режим. Для отражения статического порта, настроенного для экземпляра, рекомендуется создать псевдоним во всех узлах кластеризованного экземпляра.  
 Дополнительные сведения см. в разделе [Создание или удаление псевдонима сервера для использования клиентом (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
 Если скрыть кластеризованный именованный экземпляр, у службы кластеров могут возникнуть проблемы с подключением к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], если порт раздела реестра **LastConnect** (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) отличается от порта, от которого [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ожидает передачи данных. Если служба кластера не может подключиться к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], появится сообщение, подобное следующему:  
**Код события: 1001: Имя события: Взаимоблокировка ресурсов отказоустойчивой кластеризации.**  
  
## <a name="see-also"></a>См. также:  
 [Сетевая конфигурация сервера](../../database-engine/configure-windows/server-network-configuration.md)   
 [Описание клиентских подключений виртуального сервера SQL](https://support.microsoft.com/kb/273673)   
 [Назначение статического порта именованному экземпляру SQL Server: как избежать распространенных ошибок](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
