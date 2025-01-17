---
title: Назначение SAP BW | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6ae27f40a1da682ee0254d3605f3f05d47ceba44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726416"
---
# <a name="sap-bw-destination"></a>Назначение SAP BW

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Назначение SAP BW — компонент назначения [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 для SAP BW. Таким образом, назначение SAP BW загружает данные из потока данных в пакете служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] в систему SAP Netweaver BW версии 7.  
  
 Это назначение имеет один вход и один выход ошибок.  
  
> [!IMPORTANT]  
>  Документация по Microsoft Connector 1.1 для SAP BW предполагает, что читатель знаком со средой SAP Netweaver BW. Дополнительные сведения о SAP Netweaver BW или сведения о настройке объектов и процессов SAP Netweaver BW см. в документации SAP.  
  
 Для использования источника SAP BW необходимо выполнить следующие задачи:  
  
-   [подготовка объектов SAP Netweaver BW;](#bkmk_Prepare_Objects)  
  
-   [подключение к системе SAP Netweaver BW;](#bkmk_Connect_Database)  
  
-   [настройка цели SAP BW.](#bkmk_Configure_Destination)  
  
##  <a name="bkmk_Prepare_Objects"></a> Подготовка объектов SAP Netweaver BW, необходимых для цели  
 Цели SAP BW для функционирования необходимы определенные объекты в системе SAP Netweaver BW. Если эти объекты не существуют, выполните следующие действия для создания и настройки этих объектов в системе SAP Netweaver BW.  
  
> [!NOTE]  
>  Дополнительные сведения об этих объектах и следующих шагах настройки см. в документации SAP Netweaver BW.  
  
1.  Создайте новую исходную систему.  
  
    1.  Выберите тип **"Сторонние/промежуточные BAPI"** .  
  
    2.  Для параметра **Тип связи с целевой системой**выберите **Не Юникод (неактивные настройки MDMP)** .  
  
    3.  Назначьте соответствующий идентификатор программы.  
  
2.  Назначьте исходную систему для InfoSource.  
  
3.  Создайте InfoPackage.  
  
     InfoPackage — это самый важный объект, который требуется для цели SAP BW.  
  
 Также можно создать дополнительные объекты InfoObject, Infocube, InfoSource и InfoPackage, которые необходимы для поддержки загрузки данных в систему SAP Netweaver BW.  
  
##  <a name="bkmk_Connect_Database"></a> Подключение к системе SAP Netweaver BW  
 Для подключения к системе SAP Netweaver BW версии 7 цель SAP BW использует диспетчер соединений SAP BW, который является частью пакета [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 для SAP BW. Диспетчер соединений SAP BW является единственным диспетчером соединений [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , который может использоваться целью SAP BW.  
  
 Дополнительные сведения о диспетчере соединений SAP BW см. в разделе [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="bkmk_Configure_Destination"></a> Настройка целевого объекта SAP BW  
 Целевой объект SAP BW может быть настроен следующими способами.  
  
-   Найдите и выберите InfoPackage, который будет использоваться для загрузки данных.  
  
-   Сопоставьте каждый столбец потока данных соответствующему объекту InfoObject в пакете InfoPackage.  
  
-   Укажите, сколько строк данных будут переданы одновременно путем настройки свойства **PackageSize** .  
  
-   Выберите ожидание, пока не будет выполнена загрузка данных системой SAP Netweaver BW.  
  
-   Выберите отказ от использования триггера пакета InfoPackage и ожидание уведомления о том, что система SAP Netweaver BW начала загрузку данных.  
  
-   Можно также вызывать другую последовательность процесса после завершения загрузки данных.  
  
-   Дополнительно можно создать объекты SAP Netweaver BW, которые требуются для целевого объекта. Сюда входит создание объектов InfoObject, Infocube, InfoSource и InfoPackage.  
  
-   Проверьте загрузку данных с выбранными параметрами.  
  
 Можно также включить ведение журнала вызовов функций RFC целевым объектом. (Это ведение журнала отделено от дополнительного ведения журналов, которое можно включить для пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].) Ведение журнала вызовов функций RFC включается при настройке диспетчера соединений SAP BW, используемого целевым объектом. Дополнительные сведения о настройке диспетчера соединений см. в разделе [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Если вы не знаете все значения, необходимые для настройки назначения, может потребоваться связаться с администратором SAP.  
  
 Пошаговое руководство, в котором показано, как настроить и использовать диспетчер соединений, источник и назначение SAP BW, см. в техническом документе [Использование служб SQL Server 2008 Integration Services с SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). В этом техническом документе также показано, как настроить необходимые объекты в SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>Использование конструктора служб SSIS для настройки целевого объекта  
 Дополнительные сведения о свойствах целевого объекта SAP BW, который можно задать в конструкторе [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в одном из следующих разделов.  
  
-   [Редактор назначений SAP BW (страница "Диспетчер подключений")](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)  
  
-   [Редактор назначений SAP BW (страница "Сопоставления")](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)  
  
-   [Редактор назначений SAP BW (страница "Вывод ошибок")](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)  
  
-   [Редактор назначений SAP BW (страница "Дополнительно")](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)  
  
 При настройке целевого объекта SAP BW можно также использовать другие диалоговые окна для уточняющих запросов или создать объекты SAP Netweaver BW. Дополнительные сведения об этих диалоговых окнах см. в следующих разделах.  
  
-   [Поиск InfoPackage](../../integration-services/data-flow/look-up-infopackage.md)  
  
-   [Создание InfoObject](../../integration-services/data-flow/create-new-infoobject.md)  
  
-   [Создание InfoCube для данных транзакции](../../integration-services/data-flow/create-infocube-for-transaction-data.md)  
  
-   [Поиск InfoObject](../../integration-services/data-flow/look-up-infoobject.md)  
  
-   [Создание InfoSource](../../integration-services/data-flow/create-infosource.md)  
  
-   [Создание InfoSource для данных транзакции](../../integration-services/data-flow/create-infosource-for-transaction-data.md)  
  
-   [Создание InfoSource для основных данных](../../integration-services/data-flow/create-infosource-for-master-data.md)  
  
-   [Создать InfoPackage](../../integration-services/data-flow/create-infopackage.md)  
  
## <a name="see-also"></a>См. также:  
 [Компоненты Microsoft Connector для SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
