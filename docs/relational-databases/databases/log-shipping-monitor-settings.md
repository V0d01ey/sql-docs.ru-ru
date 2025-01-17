---
title: Настройки монитора доставки журналов | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98c2a62a558785f2ea2c483eb1e109a6ee873b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62652735"
---
# <a name="log-shipping-monitor-settings"></a>Настройки монитора доставки журналов
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Используйте эту страницу для настройки и изменения параметров монитора доставки журналов на сервере мониторинга.  
  
 Основные сведения о доставке журналов изложены в статье [Сведения о доставке журналов (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Параметры  
 **Экземпляр сервера мониторинга**  
 Отображает имя экземпляра сервера, настроенного в качестве сервера мониторинга для конфигурации доставки журнала.  
  
 **Подключить**  
 Выберите экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , который используется в качестве сервера мониторинга, и соединитесь с ним. Учетная запись, использованная для подключения, должна быть экземпляром предопределенной роли сервера sysadmin на экземпляре сервера-получателя.  
  
 **С помощью олицетворения учетной записи-посредника этого задания**  
 Необходимо при доставке журналов олицетворять учетную запись-посредник агента SQL Server при соединении с экземпляром сервера мониторинга. Процессы резервного копирования, копирования и восстановления должны иметь возможность подключения к серверу мониторинга для обновления состояния операций доставки журналов.  
  
 **С использованием следующего имени входа SQL Server**  
 Позволяет использовать определенное имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при соединении с экземпляром сервера мониторинга для доставки журналов. Процессы резервного копирования, копирования и восстановления должны иметь возможность подключения к серверу мониторинга для обновления состояния операций доставки журналов. Выберите этот параметр, если для доставки журналов желательно использовать определенное имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , а затем укажите имя входа и пароль.  
  
 **Удалить журнал после**  
 Укажите интервал времени, в течение которого на сервере мониторинга сохраняются данные о доставке журналов.  
  
 **Имя задания**  
 Указывает имя задания предупреждения агента SQL Server, используемое при доставке журналов, для предупреждения о превышении пороговых значений во время резервного копирования и восстановления. При первом создании этого задания можно изменить имя, введя в текстовом поле новое.  
  
 **Расписание**  
 Текущее расписание задания предупреждения агента SQL Server.  
  
 **Изменить**  
 Измените параметры задания предупреждения агента SQL Server.  
  
 **Отключить это задание**  
 Приостановите задание предупреждения агента SQL Server.  
  
  
