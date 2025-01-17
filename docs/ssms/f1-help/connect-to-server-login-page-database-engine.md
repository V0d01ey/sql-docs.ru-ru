---
title: Подключение к серверу (страница входа) для ядра СУБД | Документация Майкрософт
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a5dc7ee943e4cd6bd25b903bb8eb7e59dfcb2ab6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65104444"
---
# <a name="connect-to-server-login-page-database-engine"></a>Соединение с сервером (страница "Вход") ядра СУБД
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Используйте эту вкладку для просмотра или задания параметров при соединении с [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]. В большинстве случаев при подключении в поле **Имя сервера** нужно ввести имя компьютера, на котором расположена база данных, а затем нажать кнопку **Соединить**. При подключении к именованному экземпляру укажите имя компьютера, введите обратную косую черту, а затем — имя экземпляра. Например, `mycomputer\myinstance`. Если выполняется соединение с [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], введите имя компьютера, а после него — **\sqlexpress**.  
  
На возможность подключиться к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]влияют многие факторы. Справочные сведения см. в следующих документах.  
- [Урок 1. Подключение к ядру СУБД](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Устранение неполадок при соединении с SQL Server Database Engine](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Устранение ошибок подключения к SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
> [!NOTE]  
> Для подключения с проверкой подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен быть сконфигурирован в режиме проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и Windows. Дополнительные сведения о том, как можно определить режим проверки подлинности и изменить его, см. в разделе [Практическое руководство. Изменение режима проверки подлинности сервера](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="options"></a>Параметры  
**Тип сервера**  
При регистрации сервера из обозревателя объектов выберите тип сервера для подключения: [!INCLUDE[ssDE](../../includes/ssde_md.md)], службы Analysis Services, службы Reporting Services или службы Integration Services. В остальной части диалогового окна показаны параметры, которые применяются только к выбранному типу сервера. При регистрации сервера c панели "Зарегистрированные серверы" поле **Тип сервера** не может быть изменено и совпадает с типом сервера, показанного в компоненте "Зарегистрированные серверы". Чтобы зарегистрировать другой тип сервера, выберите компонент [!INCLUDE[ssDE](../../includes/ssde_md.md)], службы Analysis Services, службы Reporting Services или службы Integration Services на панели инструментов «Зарегистрированные серверы», прежде чем начать регистрацию нового сервера.  
  
При соединении с экземпляром ядра СУБД [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] через [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]необходимо использовать проверку подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и указать базу данных в диалоговом окне **Соединение с сервером** на вкладке **Свойства соединения** . Обязательно установите флажок **Шифрование соединения** .  
  
По умолчанию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] соединяется с базой данных **master**. Если указать пользовательскую базу данных, в обозревателе объектов вы увидите только эту базу данных и ее объекты. Если же подключиться к **master**, можно будет увидеть все базы данных. Дополнительные сведения см. в статье [Общие сведения о Базе данных SQL Microsoft Azure](/azure/sql-database/sql-database-technical-overview/).
  
**Имя сервера**  
Выберите экземпляр сервера для подключения. По умолчанию выводится экземпляр сервера, к которому подключение выполнялось в последний раз.  
  
**Проверка подлинности**  
Текущая версия SSMS предлагает пять режимов проверки подлинности при подключении к экземпляру [!INCLUDE[ssDE](../../includes/ssde_md.md)]. Если диалоговое окно проверки подлинности не соответствует перечисленным ниже, скачайте последнюю версию SSMS на странице [Скачивание SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md).     
  
При соединении с экземпляром ядра СУБД [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] через [!INCLUDE[ssSDS](../../includes/sssds-md.md)]необходимо использовать проверку подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и указать базу данных в диалоговом окне **Соединение с сервером** на вкладке **Свойства соединения** . Обязательно установите флажок **Шифрование соединения** .  
  
По умолчанию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] соединяется с базой данных **master**. Если указать пользовательскую базу данных при подключении к [!INCLUDE[ssSDS](../../includes/sssds-md.md)], в обозревателе объектов будет видна только эта база данных и ее объекты. Если же подключиться к **master**, можно будет увидеть все базы данных. Дополнительные сведения см. в статье [Общие сведения о Базе данных SQL Microsoft Azure](/azure/sql-database/sql-database-technical-overview/).  
  
> **Проверка подлинности Windows.**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] Режим проверки подлинности Windows позволяет подключаться с учетной записью Windows.  
> 
> **Проверка подлинности SQL Server**  
> При подключении пользователя с указанным именем входа и паролем не через доверенное соединение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет проверку подлинности самостоятельно по наличию учетной записи входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и совпадения указанного пароля с ранее сохраненным. Если в службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не задана учетная запись входа, проверка подлинности завершается ошибкой, о которой пользователь получит сообщение. По возможности используйте аутентификацию Windows.  
> 
> **Active Directory — универсальная с поддержкой MFA**  
> Проверка подлинности "Active Directory — универсальная с поддержкой MFA" представляет собой интерактивный рабочий процесс, поддерживающий Многофакторную идентификацию Azure (MFA). Azure MFA помогает защитить доступ к данным и приложениям, а также удовлетворить потребность пользователей в простом процессе входа. Она обеспечивает надежную проверку подлинности с помощью целого спектра простых способов — телефонного звонка, текстового сообщения, смарт-карт с ПИН-кодом или уведомления мобильного приложения, чтобы пользователи могли выбрать наиболее удобный для них метод. Когда учетная запись пользователя настроена для MFA, рабочий процесс интерактивной проверки подлинности требует от пользователя дополнительного взаимодействия посредством всплывающих диалоговых окон, использования смарт-карт и т. д. Если учетная запись пользователя настроена для MFA, для подключения пользователь должен выбрать универсальную проверку подлинности Azure. Если учетная запись пользователя не требует применения MFA, пользователь может использовать два других варианта проверки подлинности Azure Active Directory. Дополнительные сведения см. в разделе [Поддержка SSMS для Azure AD MFA с использованием Базы данных SQL и хранилища данных SQL](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). При необходимости вы можете изменить домен, который проверяет подлинность имени входа, щелкнув **Параметры**, выбрав вкладку **Свойства соединения** и заполнив поле **Доменное имя AD или идентификатор клиента**.  
> 
> **Active Directory — пароль**  
> Проверка подлинности Azure Active Directory — это механизм подключения к [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] с помощью удостоверений в Azure Active Directory (Azure AD).  Используйте этот метод для подключения к [!INCLUDE[ssSDS](../../includes/sssds-md.md)], если вы вошли в Windows с учетными данными из домена, не включенного в федерацию с Azure, или если применяется проверка подлинности Azure AD на базе первоначального домена или домена клиента. Дополнительные сведения см. в статье [Подключение к базе данных SQL с использованием проверки подлинности Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
> 
> **Active Directory — встроенная**  
> Проверка подлинности Azure Active Directory — это механизм подключения к [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] с помощью удостоверений в Azure Active Directory (Azure AD). Используйте этот метод для подключения к [!INCLUDE[ssSDS](../../includes/sssds-md.md)], если вы вошли в Windows с учетными данными Azure Active Directory из федеративного домена. Дополнительные сведения см. в статье [Подключение к базе данных SQL с использованием проверки подлинности Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**User name**  
Имя пользователя Windows для соединения. Этот параметр доступен только в том случае, если выбрано соединение с использованием проверки подлинности **Проверка пароля Active Directory**. Он доступен только для чтения при выборе типа проверки подлинности **Проверка подлинности Windows** или **Active Directory — встроенная**.  
  
**Имя входа**  
Введите имя входа для подключения. Этот параметр доступен только в том случае, если выбрано подключение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или проверки подлинности "Active Directory — пароль".  
  
**Пароль**  
Введите пароль для этого имени входа. Этот параметр можно изменить только в том случае, если выбрано подключение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или проверки подлинности "Active Directory — пароль".  
  
**Запомнить пароль**  
Выберите, чтобы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сохранил введенный пароль. Этот параметр отображается только в том случае, если выбрано подключение с проверкой подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Подключить**  
Щелкните, чтобы подключиться к серверу.  
  
**Параметры**  
Щелкните, чтобы открыть вкладки **Свойства соединения** и **Дополнительные параметры соединения**.  
   
  
