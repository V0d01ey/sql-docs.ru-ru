---
title: Настройка брандмауэра для доступа к серверу отчетов | Документы Майкрософт
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dfb2676b2cc06b2a3ab774b467759c7e26c58e3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175565"
---
# <a name="configure-a-firewall-for-report-server-access"></a>Configure a Firewall for Report Server Access
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] и опубликованным отчетам производится по URL-адресам, которые состоят из IP-адреса, номера порта и имени виртуального каталога. Если включен брандмауэр Windows, то порт, на который настроен сервер отчетов, скорее всего, закрыт. Обычно это выражается в том, что при обращении с удаленного клиентского компьютера к веб-порталу отображается пустая страница либо при запросе отчета открывается пустая веб-страница.  
  
 Открыть порт можно при помощи брандмауэра Windows на компьютере сервера отчетов. Службы Reporting Services не открывают порты автоматически, этот шаг необходимо выполнить вручную.  
  
 По умолчанию сервер отчетов слушает HTTP-запросы для порта 80. Следующие пошаговые инструкции позволяют настроить порт. Если URL-адреса сервера отчетов настроены на другой порт, при выполнении описанных ниже инструкций необходимо указывать его номер.  
  
 При обращении к реляционным базам данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на внешних компьютерах или в случае, если база данных сервера отчетов находится на внешнем экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо открыть порт 1433 и 1434 на внешнем компьютере. Дополнительные сведения о брандмауэре Windows см. в статье [Настройка брандмауэра Windows для доступа к компоненту Database Engine](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) в электронной документации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения о настройках брандмауэра Windows по умолчанию и описание портов TCP, влияющих на компоненты [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]и [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], см. в разделе [Настройка брандмауэра Windows для разрешения доступа к SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="prerequisites"></a>предварительные требования  
 Выполнение следующих инструкций предполагает, что создана база данных сервера отчетов, настроена учетная запись службы и URL-адреса веб-портала и веб-службы сервера отчетов. Дополнительные сведения см. в разделе [Управление сервером отчетов служб Reporting Services в собственном режиме](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Кроме этого, необходимо проверить доступность экземпляра сервера отчетов из веб-браузера через локальное соединение. Этот шаг необходим для проверки работоспособности установки. Прежде чем приступать к открытию портов, необходимо проверить правильность настройки установки. Чтобы выполнить этот шаг в Windows Server, потребуется также добавить сервер отчетов к доверенным сайтам. Дополнительные сведения см. в разделе [Настройка сервера отчетов, работающего в основном режиме, для локального администрирования (службы SSRS)](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="opening-ports-in-windows-firewall"></a>Открытие портов в брандмауэре Windows  
  
#### <a name="to-open-port-80"></a>Открытие порта 80  
  
1.  В меню **Пуск** выберите **Панель управления**, **Система и безопасность**и **Брандмауэр Windows**. Если на панели управления не включено представление по категориям, сразу выберите **Брандмауэр Windows**.  
  
2.  Выберите **Дополнительные настройки**.  
  
3.  Выберите **Правила для входящих подключений.**  
  
4.  Выберите **Создать правило** в окне **Действия**.  
  
5.  Выберите **Тип правила** в разделе **Порт**.  
  
6.  Нажмите кнопку **Далее**.  
  
7.  На странице **Протокол и порты** выберите **TCP**.  
  
8.  Выберите **Указанные локальные порты** и введите значение **80**.  
  
9. Нажмите кнопку **Далее**.  
  
10. На странице **Действие** выберите **Разрешить соединение**.  
  
11. Нажмите кнопку **Далее**.  
  
12. На странице **Профиль** выберите необходимые параметры для среды.  
  
13. Нажмите кнопку **Далее**.  
  
14. На странице **Имя** введите имя**ReportServer (TCP через порт 80)** .  
  
15. Нажмите кнопку **Готово**.  
  
16. Перезагрузите компьютер.  
  
## <a name="next-steps"></a>Следующие шаги  
 После открытия порта, прежде чем удаленные пользователи смогут производить доступ к серверу отчетов, им необходимо предоставить доступ к корневой папке и на уровне сайта. Даже если порт правильно открыт, пользователи не смогут соединяться с сервером отчетов, если им не предоставлены необходимые разрешения. См. подробнее о [предоставлении пользователям доступа к серверу отчетов](../../reporting-services/security/grant-user-access-to-a-report-server.md) в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]электронной документации.  
  
 Правильность открытия порта можно также проверить, открыв веб-портал с другого компьютера. См. подробнее о [веб-портале сервера отчетов](../../reporting-services/web-portal-ssrs-native-mode.md).
  
## <a name="see-also"></a>См. также раздел  
 [Настройка учетной записи службы сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Создание базы данных сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Настройка учетной записи службы сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Управление сервером отчетов Reporting Services в собственном режиме](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
