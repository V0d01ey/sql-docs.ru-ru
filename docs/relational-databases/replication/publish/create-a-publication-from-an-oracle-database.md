---
title: Создание публикации из базы данных Oracle | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62d24228267d0f5fd104a26d46d4aae721ac2663
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509956"
---
# <a name="create-a-publication-from-an-oracle-database"></a>Создание публикации из базы данных Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В данном разделе описывается процесс создания публикации из базы данных Oracle в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Предварительные требования](#Prerequisites)  
  
-   **Для создания публикации из базы данных Oracle используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Перед созданием публикации необходимо установить программное обеспечение Oracle на распространитель [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и настроить базу данных Oracle. Дополнительные сведения см. в статье [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 Создать публикацию моментальных снимков или публикацию транзакций из базы данных Oracle можно с помощью мастера создания публикаций.  
  
 При первоначальном создании публикации из базы данных Oracle необходимо идентифицировать издатель Oracle на распространителе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (этого не нужно делать для последующих публикаций из этой же самой базы данных). Идентификацию издателя Oracle можно выполнить в мастере создания публикаций или в диалоговом окне **Свойства распространителя — \<распространитель>** . В этой статье описывается диалоговое окно **Свойства распространителя — \<распространитель>** .  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>Идентификация издателя Oracle на распространителе SQL Server  
  
1.  В [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]подключитесь к экземпляру [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , который будет использоваться как распространитель издателем Oracle, затем раскройте серверный узел.  
  
2.  Щелкните правой кнопкой папку **Репликация** , затем щелкните **Свойства распространителя**.  
  
3.  На странице **Издатели** диалогового окна **Свойства распространителя — \<распространитель>** щелкните **Добавить**, а затем выберите **Добавить издатель Oracle**.  
  
4.  В диалоговом окне **Соединение с сервером** нажмите кнопку **Параметры** .  
  
5.  На вкладке **Имя входа** выполните следующие действия:  
  
    1.  Введите имя экземпляра базы данных Oracle или выберите **Продолжить обзор** в поле со списком **Экземпляр сервера** .  
  
    2.  Для выбора доступны **Стандартная проверка подлинности Oracle** (рекомендуется) или **Проверка подлинности Windows**.  
  
         Если выбрана **Проверка подлинности Windows**, на сервере Oracle должны быть разрешены соединения с помощью учетных данных Windows (дополнительные сведения см. в документации Oracle). Кроме того, необходимо войти в систему с той же учетной записью [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, которая была указана для схемы администратора репликации.  
  
    3.  Если установлен флажок **Стандартная проверка подлинности Oracle**, введите имя входа и пароль схемы администратора репликации, созданной на издателе Oracle во время настройки.  
  
6.  На вкладке **Свойства соединения** выберите тип издателя **Шлюз** или **Полный**.  
  
     Параметр **Полный** обеспечивает публикации моментальных снимков и транзакций с полным набором поддерживаемых функций для публикаций Oracle. Параметр **Шлюз** оптимизирует работу системы для случаев, когда шлюзом между системами выступает репликация. Параметр **Шлюз** нельзя использовать, если одна и та же таблица будет публиковаться в нескольких публикациях транзакций. Если выбран параметр **Шлюз**, то таблица может использоваться только в одной публикации транзакций и в любом количестве публикаций моментальных снимков.  
  
7.  По щелчку **Соединиться**устанавливается соединение с издателем Oracle и выполняется его настройка для репликации. Диалоговое окно **Соединение с сервером** закрывается, и вы возвращаетесь в диалоговое окно **Свойства распространителя — \<распространитель>** .  
  
    > [!NOTE]  
    >  Если имеются какие-либо проблемы с конфигурацией сети, в этом месте выводится сообщение об ошибке. Если при подключении к базе данных Oracle возникают проблемы, см. подраздел «Распространитель SQL Server не может подключиться к экземпляру базы данных Oracle» в разделе [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-create-a-publication-from-an-oracle-database"></a>Создание публикации из базы данных Oracle  
  
1.  Подключитесь к экземпляру [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , который издатель Oracle будет использовать в качестве распространителя, а затем раскройте узел сервера.  
  
2.  Раскройте папку **Репликация** .  
  
3.  Щелкните правой кнопкой папку **Локальные публикации** , затем щелкните **Создать публикацию Oracle**.  
  
4.  На странице **Издатель Oracle** мастера создания публикации выберите издателя Oracle. Если издатель Oracle не отображается, щелкните **Добавить издатель Oracle**, чтобы выполнить шаги из предыдущей процедуры.  
  
5.  На странице **Тип публикации** выберите **Публикация моментальных снимков** или **Публикация транзакций**.  
  
6.  На странице **Статьи** выберите объекты базы данных, которые нужно опубликовать.  
  
     При необходимости отфильтруйте столбцы таблицы, раскрыв таблицу и сняв флажки для одного или более столбцов. Щелкните **Свойства статьи** , чтобы просмотреть и изменить свойства статьи, а также указать при необходимости альтернативные соответствия типов данных. Дополнительные сведения о сопоставлении типов данных см. в статье [Указание сопоставления типов данных для издателя Oracle](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  На странице **Фильтрация строк таблицы** примените при необходимости фильтры для публикации подмножества данных из одной или более таблиц.  
  
8.  На странице **Агент моментальных снимков** снимите флажок **Создать моментальный снимок немедленно** только в том случае, если созданы все объекты и добавлены все требуемые данные в базу данных подписок.  
  
9. На странице **Безопасность агента** укажите учетные данные для агента моментальных снимков (для всех публикаций) и агента чтения журнала (для публикаций транзакций). Агенты запускаются и создают подключения к распространителю [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] с использованием контекста указанной учетной записи [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Агенты выполняют подключения к базе данных Oracle, используя контекст учетной записи, указанной в качестве схемы администратора репликации. Дополнительные сведения см. в статье [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
     Дополнительные сведения о разрешениях, необходимых для каждого агента, см. в разделе [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) и [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. На странице **Действия мастера** можно создать при необходимости скрипт публикации. Дополнительные сведения см. в разделе [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. На странице **Завершение работы мастера** укажите имя публикации.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 После того как база данных Oracle будет настроена как издатель, можно создать публикацию транзакций или публикацию моментальных снимков точно так же, как из издателя [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , с помощью системных хранимых процедур.  
  
#### <a name="to-create-an-oracle-publication"></a>Создание публикации Oracle  
  
1.  Настройте базу данных Oracle в качестве издателя. Дополнительные сведения см. в статье [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
2.  Если удаленный распространитель не существует, настройте удаленный распространитель. Дополнительные сведения см. в статье [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  На удаленном распространителе, который будет использовать издатель Oracle, выполните хранимую процедуру [sp_adddistpublisher (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Задайте имя TNS (Transparent Network Substrate) экземпляра базы данных Oracle для **@publisher** и значение **ORACLE** или **ORACLE GATEWAY** для **@publisher_type** . `Specify` режим безопасности, используемый при соединении с издателем Oracle к удаленному распределителю [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] одним из следующих способов:  
  
    -   Чтобы по умолчанию использовать стандартную проверку подлинности Oracle, укажите значение **0** для **@security_mode** , имя входа административной схемы пользователей репликации, созданной во время настройки издателя Oracle, в параметре **@login** и пароль в параметре **@password** .  
  
        > [!IMPORTANT]  
        >  По возможности предлагайте пользователям вводить учетные данные системы безопасности во время выполнения приложения. При хранении учетных данных в файле скрипта необходимо защитить этот файл во избежание несанкционированного доступа.  
  
    -   Чтобы использовать проверку подлинности Windows укажите в параметре **@security_mode** для **@security_mode** .  
  
        > [!NOTE]  
        >  Чтобы использовать проверку подлинности Windows, на сервере Oracle должны быть разрешены соединения с помощью учетных данных Windows (дополнительные сведения см. в документации Oracle). Кроме того, необходимо войти в систему с той же учетной записью Microsoft Windows, которая была указана для схемы администратора репликации.  
  
4.  Создайте задание агента чтения журнала для базы данных публикации.  
  
    -   Если неизвестно, существует ли задание агента чтения журнала для опубликованной базы данных, выполните хранимую процедуру [sp_helplogreader_agent (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) на распространителе, который используется издателем Oracle в базе данных распространителя. В параметре **@publisher** . Если результирующий набор пуст, необходимо создать задание агента чтения журнала.  
  
    -   Если агент чтения журнала для базы данных публикации уже существует, переходите к шагу 5.  
  
    -   На распространителе, который используется издателем Oracle в базе данных распространителя, выполните хранимую процедуру [sp_addlogreader_agent (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Укажите учетные данные Windows, с которыми будет запущен агент, в качестве значений параметров **@job_login** и **@job_password** .  
  
        > [!NOTE]  
        >  Параметр **@job_login** должен соответствовать имени входа, заданному на шаге 3. Не указывайте сведения о безопасности издателя. Агент чтения журнала соединяется с издателем с помощью сведений о безопасности издателя, указанных на шаге 3.  
  
5.  Чтобы создать публикацию, на распространителе в базе данных распространителя выполните хранимую процедуру [sp_addpublication (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Дополнительные сведения см. в статье [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  На распространителе в базе данных распространителя выполните процедуру [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Укажите имя публикации, используемое на шаге 4, в параметре **@publication** , а учетные данные Windows, с которыми работает агент моментальных снимков, — в параметрах **@job_name** и **@password** . Чтобы использовать стандартную проверку подлинности Oracle при подключении к издателю, требуется также указать значение **0** для **@publisher_security_mode** и сведения об имени входа Oracle для параметров **@publisher_login** и **@publisher_password** . Будет создано задание агента моментальных снимков для публикации.  
  
## <a name="see-also"></a>См. также:  
 [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Публикация данных и объектов базы данных](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Configure the Transaction Set Job for an Oracle Publisher](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  (Настройка задания для набора транзакции в издателе Oracle)  
 [Обзор публикации Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  
