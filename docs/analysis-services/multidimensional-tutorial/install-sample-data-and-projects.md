---
title: Установка образцов данных служб Analysis Services и проектов | Документация Майкрософт
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 999e1c1434bd727fe0ac889c2041145a5c1ec750
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404096"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Установка образцов данных и многомерные проекты 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

Используйте указания и ссылки, приведенные в этой статье для установки файлов данных и проектов, используемых в учебники по службам Analysis Services. 
  
## <a name="step-1-install-prerequisites"></a>Шаг 1. Установка необходимых компонентов 
В занятиях этого учебника предполагается, что установлено следующее программное обеспечение. Все функции можно установить на одном компьютере. Для установки этих компонентов запустите программу установки SQL Server и выберите их на странице «Выбор компонентов».  
  
-   Компонент SQL Server Database Engine  
  
-   SQL Server Analysis Services (SSAS) 
  
    Службы Analysis Services доступна только в следующих выпусках: Evaluation, Enterprise, Business Intelligence, Standard. Многомерных моделях не поддерживаются в Azure Analysis Services.
  
    По умолчанию служб Analysis Services 2016 и более поздние версии устанавливается как табличный экземпляр, который можно переопределить, выбрав многомерном режиме сервера на сервере конфигурации страницы мастера установки.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>Шаг 2. Скачайте и установите средства разработки и управления
SQL Server Data Tools (SSDT) для Visual Studio загружается и устанавливается отдельно от других компонентов SQL Server. Конструкторы и шаблоны проектов, используемый для создания моделей бизнес-Аналитики и отчетов, включенных в SSDT для Visual Studio 2015 или как [пакеты Nuget](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) для Visual Studio 2017.  
  
[Скачайте SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542).   

SQL Server Management Studio (SSMS) загружается и устанавливается отдельно от других компонентов SQL Server.  

[Скачать SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

При необходимости по ходу работы с учебником можно установить Excel для просмотра многомерных данных. Установка Excel позволит применять функцию **Анализ в Excel** , которая запускает Excel, используя список полей сводной таблицы, связанный с разрабатываемым кубом. Рекомендуется использовать для просмотра данных Excel, так как в этом случае можно быстро строить сводные отчеты, позволяющие взаимодействовать с данными.  
  
Кроме того, данные можно просматривать с помощью конструктора запросов многомерных выражений, который встроен в [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Конструктор запросов возвращает те же данные, только представленные в виде плоского набора строк.  
  
## <a name="step-3-install-databases"></a>Шаг 3. Установка баз данных  
В многомерной модели служб Analysis Services используются транзакционные данные, импортируемые из системы управления реляционными базами данных. Для целей данного учебника используется следующая реляционная база данных как источника данных.  
  
-   **AdventureWorksDW2012 или более поздней версии** — это реляционное хранилище данных, выполняемое в экземпляре ядра СУБД. Он предоставляет исходные данные, используемые баз данных служб Analysis Services и проекты, которые создают и развернете в этом учебнике. В учебнике предполагается, вы используете AdventureWorksDW2012, тем не менее, работают ли более поздних версий.
  
    Можно использовать этот образец базы данных с помощью [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] и более поздних версий. В целом, следует использовать версию образец базы данных, которая соответствует версии базы данных.
  
Чтобы установить базу данных, сделайте следующее:  
  
1.  Скачайте [AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) резервной копии базы данных с сайта GitHub.  
  
2.  Скопируйте файл резервной копии в каталог данных локального экземпляра SQL Server Database Engine.
  
3.  Запустите среду Microsoft SQL Server Management Studio и подключитесь к экземпляру компонента Database Engine.  
  
4.  восстановить базу данных.  
  
## <a name="step-4-grant-database-permissions"></a>Шаг 4. GRANT, предоставление разрешений базы данных  
В образцах проектов используются параметры олицетворения источников данных, указывающие контекст безопасности, в котором импортируются и обрабатываются данные. По умолчанию в параметрах олицетворения для доступа к данных указана учетная запись службы Analysis Services. Чтобы использовать этот параметр по умолчанию, необходимо убедиться, что учетная запись службы, под которой выполняются службы Analysis Services имеются данных разрешения на чтение **AdventureWorksDW** базы данных.  
  
> [!NOTE]  
> В целях обучения рекомендуется использовать стандартный вариант олицетворения учетной записи службы и предоставить разрешения на чтение данных учетной записи службы в SQL Server. Хотя возможны и другие варианты олицетворения, не все из них подходят для операций обработки. В частности, вариант использования учетных данных текущего пользователя не поддерживается при обработке.  
  
1.  Определите учетную запись службы. Для просмотра сведений об учетной записи можно использовать диспетчер конфигурации SQL Server или консольное приложение командной строки «Службы». Если службы Analysis Services установлены в качестве экземпляра по умолчанию с использованием учетной записи по умолчанию, служба выполняется как **NT Service\MSSQLServerOLAPService**.  
  
2.  В среде Management Studio подключитесь к экземпляру компонента Database Engine.  
  
3.  Разверните папку "Безопасность" и выберите команду **Создать имя входа**.  
  
4.  На странице "Общие" в поле "Имя входа" введите **NT Service\MSSQLServerOLAPService** (или другую учетную запись, от имени которой выполняется служба).  
  
5.  Щелкните **Сопоставление пользователей**.  
  
6.  Установите флажок рядом с полем **AdventureWorksDW** базы данных. Членство в ролях должно автоматически включать роли **db_datareader** и **public**. Нажмите кнопку **ОК** , чтобы принять параметры по умолчанию.  
  
## <a name="step-5-install-projects"></a>Шаг 5. Установка проектов  

Учебник включает образцы проектов, что позволяет сравнить полученные вами результаты с готовым проектом или сразу перейти к одному из следующих занятий.  
  
1.  Скачайте [adventure-works многомерных учебник projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) в компании Adventure Works для служб Analysis Services странице образцов на GitHub.  
  
    Образцы проектов работать для [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] и более поздних версий.  
  
2.  Переместите этот ZIP-файл в папку, расположенную в корне диска (например, C:\Tutorial). Это позволяет избежать ошибки «Слишком длинный путь», которая иногда возникает при попытке распаковать файлы в папке «загрузки».  
  
3.  Извлеките образцы проектов. Щелкните файл правой кнопкой мыши и выберите команду **Извлечь все**. После извлечения файлов, вы получите папки занятия 1, 2, 3, 5, 6, 7, 8, 9, 10 завершить и Lesson 4 Start. 
  
4.  Удалите для этих файлов разрешения только на чтение. Щелкните правой кнопкой мыши родительскую папку, выберите **свойства**и снимите флажок для **только для чтения**. Нажмите кнопку **ОК**. Примените изменения к этой папке, вложенным папкам и файлам.  

5.  Откройте файл решения (SLN), соответствующий к занятию, используемая в. Например, в папке с именем «Занятие 1 выполнено» нужно будет открыть файл «Analysis Services Tutorial.sln».  
  
6.  Разверните решение, чтобы убедиться, что разрешения базы данных и сведения о расположении сервера настроены правильно.  
  
    Если службы Analysis Services и компонент ядра СУБД установлены в качестве экземпляра по умолчанию (MSSQLServer) и все программное обеспечение выполняется на одном компьютере, можно выбрать команду **Развернуть решение** в меню "Сборка", чтобы выполнить сборку и развернуть образец проекта в локальном экземпляре служб Analysis Services. Во время развертывания данные обрабатываются (или импортировать) из **AdventureWorksDW** базы данных на локальном экземпляре ядра СУБД. Новую базу данных служб Analysis Services создается на экземпляре служб Analysis Services, который содержит данные, полученные от ядра СУБД.  
  
    В случае возникновения ошибок повторно просмотрите предыдущие шаги по настройке разрешений для базы данных. Кроме того, может потребоваться изменить имена серверов. Имя сервера по умолчанию — localhost. Если ваши серверы установлены на удаленных компьютерах или как именованные экземпляры, необходимо переопределить значение по умолчанию для имени сервера на такое, что будет допустимым для установки. Кроме того, если серверы размещены на удаленных компьютерах, может понадобиться настроить брандмауэр Windows на разрешение доступа к этим серверам.  
  
    Имя сервера для соединения с компонентом Database Engine указано в объекте Data Source многомерного решения (учебник Adventure Works), видимом в обозревателе решений.  
  
    Имя сервера для подключения к службам Analysis Services указывается на вкладке «Развертывание» страниц «Свойства» проекта, также отображаемых в обозревателе решений.  
  
7.  В среде SQL Server Management Studio подключитесь к службам Analysis Services. Убедитесь в том, что на сервере работает база данных с именем **Analysis Services Tutorial** .  
  
## <a name="next-step"></a>Следующий шаг  
Теперь вы готовы к работе с учебником. Дополнительные сведения о том, как приступить к работе, см. в разделе [Многомерное моделирование (учебник по Adventure Works)](multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>См. также  
[Настройка брандмауэра Windows на разрешение доступа к службам Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configure the Windows Firewall to Allow SQL Server Access](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  