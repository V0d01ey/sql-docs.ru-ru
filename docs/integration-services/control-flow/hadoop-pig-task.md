---
title: Задача Pig для Hadoop | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4991fd3ad95a633881099b9677c9db55935f6a13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727599"
---
# <a name="hadoop-pig-task"></a>Задача Pig для Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача Pig для Hadoop используется для запуска сценария Pig в кластере Hadoop.  
  
 Чтобы добавить задачу Pig для Hadoop, перетащите ее в конструктор. Затем дважды щелкните задачу или щелкните ее правой кнопкой мыши и выберите команду **Изменить**, чтобы открыть диалоговое окно **Hadoop Pig Task Editor** (Редактор задач Pig для Hadoop).  
  
 ![Hadoop Pig Task Editor](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig Task Editor")  
  
## <a name="options"></a>Параметры  
 В диалоговом окне **Hadoop Pig Task Editor** (Редактор задач Pig для Hadoop) настройте следующие параметры.  
  
|Поле|Описание|  
|-----------|-----------------|  
|**Hadoop Connection (Подключение Hadoop)**|Укажите существующий диспетчер подключений Hadoop или создайте новый. Этот диспетчер указывает, где размещена служба WebHCat.|  
|**Тип источника**|Укажите тип источника запроса. Доступные значения: **ScriptFile** (Файл сценария) и **DirectInput**(Прямой ввод).|  
|**InlineScript (Встроенный сценарий)**|Если значение параметра **SourceType** (Тип источника) — **DirectInput**(Прямой ввод), укажите сценарий Pig.|  
|**HadoopScriptFilePath (Путь к файлу сценария Hadoop)**|Если значение **SourceType** (Тип источника) — **ScriptFile**(Файл сценария), укажите путь к файлу скрипта в Hadoop.|  
|**TimeoutInMinutes (Время ожидания в минутах)**|Укажите время ожидания в минутах. Задание Hadoop останавливается, если оно не завершилось до истечения времени ожидания. Укажите 0, чтобы запланировать асинхронное выполнение задания Hadoop.|  
  
## <a name="see-also"></a>См. также:  
 [Диспетчер подключений Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
