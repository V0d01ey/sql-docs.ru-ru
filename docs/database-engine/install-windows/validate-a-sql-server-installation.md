---
title: Проверка установки SQL Server | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 7597997f55e6b070013b32a1d36f0a16f8fe5111
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794674"
---
# <a name="validate-a-sql-server-installation"></a>Проверка установки SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  С помощью отчета об обнаружении [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно проверить, какая версия [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и какие компоненты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установлены на компьютере. На странице **Отчет об обнаруженных установленных компонентах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** показан отчет обо всех продуктах и компонентах [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] и [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)], установленных на локальном сервере. Отчет об обнаружении компонентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] доступен на странице **Средства** в центре установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ## <a name="run-includessnoversionincludesssnoversion-mdmd-features-discovery-report"></a>Запуск отчета об обнаруженных компонентах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Запустите центр установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], для этого в меню **Пуск** выберите **Все программы**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<имя версии>** , **Средства настройки** и **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Центр установки**. Чтобы запустить отчет об обнаружении компонентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], щелкните **Средства** в левой области навигации **центра установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** и выберите **Установленный отчет об обнаружении компонентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** .  
  
 Отчет об обнаруженных компонентах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сохраняется в папке %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<последний_сеанс_программы_установки\>.  
  
 Его создание можно запустить из командной строки. Выполните команду Setup.exe/Action=RunDiscovery из командной строки. Если добавить к ней параметр /q, то пользовательский интерфейс не отобразится, но отчет все равно будет создан в каталоге %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<последний_сеанс_программы_установки\>.  
  
## <a name="see-also"></a>См. также раздел  
 [Просмотр и чтение файлов журналов программы установки SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
