---
title: Резервное копирование и восстановление SQL Server с помощью службы хранилища Blob-объектов Microsoft Azure | Документация Майкрософт
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 625eccb976c500dcacaa5612ca41bac8b638fbed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62516245"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>Резервное копирование и восстановление SQL Server с помощью службы хранилища Blob-объектов Microsoft Azure
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![Изображение резервного копирования в большой двоичный объект Azure](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "Изображение резервного копирования в большой двоичный объект Azure")  
  
 В этом разделе описывается резервное копирование [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и восстановление из [службы хранилища BLOB-объектов Microsoft Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). В разделе также описаны основные преимущества использования службы BLOB-объектов Microsoft Azure для хранения резервных копий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 SQL Server позволяет хранить резервные копии в службе хранилища BLOB-объектов Microsoft Azure следующими способами:  
  
-   **Управление резервными копиями в Microsoft Azure**. Используя те же методы, которые применяются для резервного копирования на диски и магнитные ленты, можно создать резервную копию в хранилище Microsoft Azure, указав URL-адрес в качестве места назначения резервного копирования. Эту функцию можно использовать для создания резервной копии вручную или настройки собственной стратегии резервного копирования для локального хранилища или других вариантов удаленного хранения. Эта функция также называется **резервным копированием SQL Server по URL-адресу**. Дополнительные сведения см. в разделе [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md). Эта функция доступна в SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным обновлением 2 и более поздних версиях. В [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] эта функция получила улучшения. В результате была повышена производительность и улучшены функциональные возможности за счет блочной обработки больших двоичных объектов, подписей общего доступа и чередования.  
  
    > [!NOTE]  
    >  Для версий SQL Server до SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 2 (CU2) имеется надстройка для резервного копирования SQL Server в Microsoft Azure, которая позволяет быстро и легко создавать резервные копии в службе хранилища Microsoft Azure. Дополнительные сведения см. в [центре загрузки](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Резервные копии моментальных снимков файлов баз данных в хранилище больших двоичных объектов Azure** Если использовать моментальные снимки Azure, резервные копии моментальных снимков [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяют почти мгновенно выполнять резервное копирование и восстановление файлов базы данных, хранящихся в службе хранилища BLOB-объектов Azure. Эта функция позволяет упростить политики резервного копирования и восстановления, а также поддерживает восстановление до точки во времени. Дополнительные сведения см. в разделе [Резервные копии моментальных снимков файлов для файлов базы данных в Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md). Эта функция доступна в SQL Server 2016 и более поздних версиях.  
  
-   **Предоставьте SQL Server возможность управлять резервным копированием в Microsoft Azure**. Настройте SQL Server для управления стратегией резервного копирования и планирования резервного копирования для отдельной базы данных или нескольких баз данных, а также настройки параметров по умолчанию на уровне экземпляра. Это функция называется **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** . Дополнительные сведения см. в разделе [Управляемое резервное копирование SQL Server в Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md). Эта функция доступна в SQL Server 2014 и более поздних версиях.  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>Преимущества хранения резервных копий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в службе BLOB-объектов Microsoft Azure  
  
-   Гибкое, надежное и неограниченное по объему удаленное хранилище. Хранение резервных копий в службе BLOB-объектов Microsoft Azure является удобным и гибким, а также позволяет реализовать простой удаленный доступ к данным. Для создания удаленного хранилища для резервных копий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] достаточно внести изменения в существующие скрипты и задания. Удаленное хранилище обычно должно быть расположено достаточно далеко от рабочей базы данных, чтобы одна авария не могла повлиять одновременно и на удаленную копию, и на рабочую базу данных. Георепликация хранилища больших двоичных объектов обеспечивает дополнительный уровень защиты в случае аварии регионального масштаба. Кроме того, резервные копии доступны в любом месте и в любое время, а также к ним легко получить доступ для восстановления.  
  
    > [!IMPORTANT]  
    >  С помощью блочных BLOB-объектов в [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]можно создать чередующийся резервный набор данных, обеспечив поддержку файлов резервной копии размером до 12,8 ТБ.  
  
-   Архив резервных копий. Служба BLOB-объектов Microsoft Azure — это лучшая альтернатива популярному подходу к резервному копированию на магнитную ленту. Может потребоваться физически транспортировать накопители на магнитной ленте в удаленное помещение и принимать меры для защиты носителей. Хранение резервных копий в хранилище BLOB-объектов Microsoft Azure обеспечивает быстрое, доступное и надежное архивирование.  
  
-   Отсутствие расходов на управление оборудованием. Службы Microsoft Azure позволяют избежать расходов на управление оборудованием. Службы Microsoft Azure сами управляют оборудованием и обеспечивают георепликацию для избыточности и защиты от сбоев оборудования.  
  
-   В настоящее время для экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , запущенных в виртуальной машине Microsoft Azure, создание резервных копий с помощью службы хранилища BLOB-объектов Microsoft Azure можно выполнить, создав подключенные диски. Однако количество дисков, которые можно подключить к виртуальной машине Microsoft Azure, ограничено. Для сверхбольших экземпляров данное ограничение составляет 16 дисков, а для небольших экземпляров это количество меньше. Включив резервное копирование непосредственно в хранилище BLOB-объектов Microsoft Azure, вы можете обойти ограничение в 16 дисков.  
  
     Кроме того, файл резервной копии, который хранится в службе хранилища BLOB-объектов Microsoft Azure, напрямую доступен в локальной службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или другой службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в виртуальной машине Microsoft Azure. Присоединение и отсоединение базы данных, а также скачивание и подключение виртуального жесткого диска не требуется.  
  
-   Экономические преимущества: оплата только тех услуг, которые используются. Может применяться в качестве экономически эффективного решения по удаленному резервному копированию и архивированию. Для получения дополнительной информации и ссылок см. раздел [Вопросы оплаты использования Microsoft Azure](#Billing) .  
  
##  <a name="Billing"></a> Вопросы оплаты использования Microsoft Azure  
 Если вы знаете, сколько стоит использование службы хранилища Microsoft Azure, вы можете прогнозировать стоимость создания и хранения резервных копий в Microsoft Azure.  
  
 [Ценовой калькулятор Microsoft Azure](https://go.microsoft.com/fwlink/?LinkId=277060) может помочь оценить затраты.  
  
 **Хранение данных.** Стоимость основывается на используемом пространстве и высчитывается по градуированной шкале и уровню избыточности. Дополнительные сведения и обновленную информацию см. в разделе **Управление данными** статьи [Расчет цен](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Передача данных**. За входящий трафик в Microsoft Azure оплата не начисляется. Исходящие передачи оцениваются по пропускной способности, а их стоимость высчитывается по градуированной шкале, привязанной к региону. Дополнительные сведения см. в разделе [Передача данных](https://go.microsoft.com/fwlink/?LinkId=277061) в статье «Расчет цен».  
  
## <a name="see-also"></a>См. также:  

[Резервное копирование SQL Server на URL-адрес — рекомендации и устранение неполадок](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[Резервное копирование и восстановление системных баз данных (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[Учебник. Использование службы хранилища больших двоичных объектов Microsoft Azure с базами данных SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[Резервное копирование в SQL Server по URL-адресу](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
