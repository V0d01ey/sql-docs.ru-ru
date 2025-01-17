---
title: Выбор места расположения резервной копии | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a3642d349fd9d6df39651e38b8b1789dd935c49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761218"
---
# <a name="select-backup-destination"></a>Выбор места расположения резервной копии
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Используйте диалоговое окно **Выбор места расположения резервной копии** для выбора устройства, где будет находиться резервная копия. Расположением резервной копии может быть диск или логическое устройство резервного копирования.  
  
 **Резервное копирование базы данных с помощью среды SQL Server Management Studio**  
  
-   [Создание полной резервной копии базы данных (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Создание разностной резервной копии базы данных (SQL Server)](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Резервное копирование файлов и файловых групп (SQL Server)](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Создание резервной копии журнала транзакций (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Параметры  
 Параметры диалогового окна зависят от выбранного места назначения: диск или магнитная лента.  
  
 **Место назначения на диске**  
 Для указания места назначения резервной копии выберите один из следующих параметров.  
  
|||  
|-|-|  
|**Имя файла**|Выберите этот параметр и введите в текстовое поле локальный или удаленный файл как место расположения резервной копии.<br /><br /> Для указания локального файла нажмите кнопку "Обзор" справа от текстового поля и укажите файл на фиксированных дисках компьютера, на котором находится сервер, или введите полный путь и имя файла. Например, `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Укажите удаленный файл в качестве места расположения резервной копии. Для этого введите полное имя файла в формате UNC. Дополнительные сведения см. в разделе [Устройства резервного копирования (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md).<br /><br /> <br /><br /> **\*\* Важная информация. \*\*** В случае резервного копирования данных по сети могут произойти сетевые ошибки. Поэтому по его завершении рекомендуется сделать проверку. Дополнительные сведения см. в разделе [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).|  
|**устройство резервного копирования;**|Выберите этот параметр для выбора логического устройства резервного копирования.<br /><br /> Примечание. Дополнительные сведения о создании дискового устройства резервного копирования см. в разделе [Определение логического устройства резервного копирования для дискового файла (SQL Server)](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Место назначения на ленте**  
 В качестве места расположения резервной копии выберите ленточный накопитель, физически подключенный к компьютеру, на котором находится сервер (экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Выберите один из следующих параметров.  
  
|||  
|-|-|  
|**Ленточный накопитель**|Выберите этот параметр, чтобы в качестве места расположения резервной копии выбрать накопитель на магнитной ленте из списка ленточных накопителей, физически подключенных к компьютеру, на котором находится экземпляр сервера.<br /><br /> Примечание. Устройства резервного копирования на магнитных лентах на удаленных компьютерах не могут указываться в качестве места назначения резервной копии.|  
|**устройство резервного копирования;**|Выберите этот параметр для выбора существующего логического устройства резервного копирования. Эти логические устройства соответствуют ленточным накопителям, физически подключенным к компьютеру, на котором находится экземпляр сервера.<br /><br /> Примечание. Дополнительные сведения о создании ленточного устройства резервного копирования см. в разделе [Определение логического устройства резервного копирования для ленточного накопителя (SQL Server)](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>См. также:  
 [Устройства резервного копирования (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Наборы носителей, семейства носителей и резервные наборы данных (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
