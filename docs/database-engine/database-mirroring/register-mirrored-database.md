---
title: Регистрация зеркальной базы данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.registermirroreddb.f1
ms.assetid: 6acd02b9-2311-49b0-a5f8-3852beecb4b0
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: be6b135e4e21f7bdcec47c231be6fe872a20ab76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795307"
---
# <a name="register-mirrored-database"></a>Регистрация зеркальной базы данных
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Используйте это диалоговое окно для регистрации одной или нескольких баз данных на данном экземпляре сервера посредством добавления базы или баз данных к монитору зеркального отображения баз данных. Когда база данных добавлена, монитор зеркального отображения баз данных локально кэширует сведения о базе данных, ее участниках и о возможностях соединения с участниками.  
  
> [!IMPORTANT]  
>  Пользователь, являющийся членом предопределенной роли сервера **sysadmin** на экземпляре основного сервера, но не являющийся им на экземпляре зеркального сервера, может просмотреть только состояние экземпляра основного сервера.  
  
 **Наблюдение за зеркальным отображением базы данных с помощью среды SQL Server Management Studio**  
  
-   [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Параметры  
 **Экземпляр сервера**  
 Выберите экземпляр сервера из списка, в котором содержатся экземпляры сервера, сведения о соединении с которыми хранятся монитором зеркального отображения баз данных, или нажмите кнопку **Соединить**. Для определения новых учетных данных для выбранного из списка экземпляра сервера нажмите кнопку **Соединить** и подключитесь с помощью новых учетных данных.  
  
> [!NOTE]  
>  Для регистрации баз данных на нескольких экземплярах сервера после завершения проверки необходимых баз данных для одного экземпляра нажмите кнопку **Применить**и выберите другой экземпляр сервера.  
  
 **Подключить**  
 Для определения новых учетных данных для выбранного из списка экземпляра сервера нажмите кнопку **Соединить** и подключитесь с помощью новых учетных данных. Во время подключения к экземпляру сервера монитор зеркального отображения баз данных отображает сообщение **Ожидание данных**.  
  
 **Зеркальные базы данных**  
 В сетке **Зеркальные базы данных** перечислены зеркальные базы данных на экземпляре сервера.  
  
 Сетка содержит следующие столбцы:  
  
|Имя столбца|Описание|  
|-----------------|-----------------|  
|**Зарегистрировать**|Проверка каждой базы данных, которую требуется зарегистрировать. Если база данных в настоящий момент настраивается, соответствующий ей флажок установлен и отключен.<br /><br /> Примечание. Для отмены регистрации базы данных необходимо закрыть диалоговое окно **Зарегистрированная зеркальная база данных**, выбрать базу данных в дереве навигации и в меню **Действие** выбрать команду **Отменить регистрацию**.|  
|**База данных**|Имя зеркальной базы данных на выбранном экземпляре сервера.|  
|**Текущая роль**|Текущая роль зеркального отображения базы данных, основной или зеркальный сервер, на выбранном экземпляре сервера.|  
|**Участник (Подключить как)**|Имя партнера по обеспечению отработки отказа для базы данных. В круглых скобках отображается **Проверка подлинности Windows пользователя консоли** или **Проверка подлинности имени для входа SQL Server "***\<имя для входа>***"** . Это используемые в настоящий момент сведения для проверки подлинности, если экземпляр был добавлен ранее, или те, которые будут использованы, если данный экземпляр не был добавлен в монитор.|  
  
 **Показать диалоговое окно «Управление соединениями сервера» после нажатия кнопки «ОК»**  
 По умолчанию, монитор зеркального отображения баз данных использует учетные данные проверки подлинности Windows для экземпляров сервера-участника, учетные данные для которых ранее не были указаны. Включите этот параметр для изменения учетных данных для одного или нескольких экземпляров сервера после завершения регистрации баз данных.  
  
 Если данный параметр включен, то после нажатия кнопки **ОК**откроется диалоговое окно **Управление соединениями сервера** . Здесь можно выбрать экземпляр сервера, для которого необходимо указать учетные данные, используемые монитором при подключении к данному партнеру по обеспечению отработки отказа.  
  
 Для изменения учетных данных участника найдите его запись в сетке **Экземпляры сервера** и выберите **Изменить** в данной строке. Откроется диалоговое окно **Соединение с сервером** для этого имени экземпляра сервера с элементами управления для учетных данных, инициализированных текущим кэшированным значением. Измените необходимым образом учетные данные и нажмите кнопку **Соединить**. Если учетные данные имеют достаточные права доступа, столбец **Соединиться при помощи** обновляется новыми учетными данными.  
  
 **Применить**  
 Нажмите эту кнопку для регистрации выбранных баз данных (и для сохранения учетных данных для экземпляров сервера-участника), при этом диалоговое окно остается открытым.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Наблюдение за зеркальным отображением базы данных (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Запуск мастера настройки безопасности зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
