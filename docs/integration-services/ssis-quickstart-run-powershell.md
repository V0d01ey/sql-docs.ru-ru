---
title: Выполнение пакета служб SSIS с помощью PowerShell | Документы Майкрософт
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0703c95824224f8200a43a38ad5990971c6b7911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65717565"
---
# <a name="run-an-ssis-package-with-powershell"></a>Выполнение пакета служб SSIS с помощью PowerShell

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


В этом кратком руководстве описывается применение скрипта PowerShell для подключения к серверу базы данных и запуска пакета служб SSIS.

## <a name="prerequisites"></a>предварительные требования

Сервер базы данных SQL Azure прослушивает порт 1433. Если вы пытаетесь подключиться к серверу базы данных SQL Azure изнутри корпоративного брандмауэра, для успешного подключения в этом брандмауэре должен быть открыт данный порт.

## <a name="supported-platforms"></a>Поддерживаемые платформы

Сведения, приведенные в этом кратком руководстве, можно использовать для выполнения пакета SSIS на следующих платформах:

-   SQL Server в Windows.

-   База данных SQL Azure. Дополнительные сведения о развертывании и запуске пакетов в Azure см. в разделе [Перенос рабочих нагрузок SQL Server Integration Services в облако](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Сведения, приведенные в этом кратком руководстве, не могут быть использованы для выполнения пакета SSIS в Linux. Дополнительные сведения о запуске пакетов на Linux см. в разделе [Извлечение, преобразование и загрузка данных в Linux с помощью служб SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Получение сведений о подключении для базы данных SQL Azure

Для запуска пакета в базе данных SQL Azure вам нужны сведения, необходимые для подключения к базе данных каталога служб SSIS (SSISDB). В описанных ниже процедурах вам потребуется полное имя сервера и имя для входа.

1. Войдите на [портал Azure](https://portal.azure.com/).
2. Выберите **Базы данных SQL** в меню слева, а затем на странице **Базы данных SQL** — базу данных SSISDB. 
3. На странице **Обзор** для базы данных просмотрите полное имя сервера. Чтобы увидеть параметр **Щелкните, чтобы скопировать**, наведите указатель мыши на имя сервера. 
4. Если вы забыли учетные данные входа на сервер базы данных SQL Azure, перейдите на страницу этого сервера, чтобы узнать имя его администратора. При необходимости вы можете сбросить пароль.
5. Щелкните **Показать строки подключения к базам данных**.
6. Просмотрите полную строку подключения **ADO.NET**.

## <a name="ssis-powershell-provider"></a>Поставщик SSIS PowerShell
Поставщик PowerShell служб SSIS можно использовать для подключения к каталогу служб SSIS и выполнения пакетов в нем.

Ниже приведен простой пример того, как выполнить пакет служб SSIS в каталоге пакетов с помощью поставщика PowerShell для служб SSIS.

```powershell
(Get-ChildItem SQLSERVER:\SSIS\localhost\Default\Catalogs\SSISDB\Folders\Project1Folder\Projects\'Integration Services Project1'\Packages\ |
WHERE { $_.Name -eq 'Package.dtsx' }).Execute("false", $null)
```

## <a name="powershell-script"></a>Скрипт PowerShell
Предоставьте соответствующие значения для переменных в начале следующего скрипта, а затем выполните скрипт, чтобы запустить пакет служб SSIS.

> [!NOTE]
> В следующем примере используется проверка подлинности Windows. Чтобы использовать проверку подлинности SQL Server, замените аргумент `Integrated Security=SSPI;` на `User ID=<user name>;Password=<password>;`. Если вы подключаетесь к серверу базы данных SQL Azure, вы не можете использовать проверку подлинности Windows. 

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>Следующие шаги
- Рассмотрите другие варианты выполнения пакета.
    - [Выполнение пакета служб SSIS с помощью SSMS](./ssis-quickstart-run-ssms.md)
    - [Выполнение пакета служб SSIS с помощью Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Выполнение пакета служб SSIS с помощью Transact-SQL (Visual Studio Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Выполнение пакета служб SSIS из командной строки](./ssis-quickstart-run-cmdline.md)
    - [Выполнение пакета служб SSIS с помощью C#](./ssis-quickstart-run-dotnet.md) 
