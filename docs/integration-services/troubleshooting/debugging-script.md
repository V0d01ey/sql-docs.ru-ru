---
title: Скрипт отладки | Документы Майкрософт
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Script task [Integration Services], debugging
- debugging [Integration Services], scripts
- scripts [Integration Services], debugging
ms.assetid: fddf57d8-8607-4f88-85a0-1b683087b491
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0b038e81c70e3368e9f66c6dfefc925e282b27d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65713738"
---
# <a name="debugging-script"></a>Скрипт отладки

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Скрипты, использующие задачу и компонент "Скрипт", создаются в средствах для приложений [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] (VSTA).  
  
 Можно задавать и использовать в скриптах точки останова в VSTA. VSTA дает возможность управлять точками останова, но для этого вы можете также пользоваться и диалоговым окном **Задание точек останова** конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Дополнительные сведения см. в статье [Отладка потока управления](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 Диалоговое окно **Задание точек останова** включает точки останова скрипта. Они содержатся внизу списка точек останова и отображают номер строки и имя функции, в которой появляется точка останова. Точки останова скрипта вы можете удалять с помощью диалогового окна **Задание точек останова** .  
  
 Во время выполнения точки останова, заданные для строк кода скрипта, объединяются с точками останова, заданными для пакета или задач и контейнеров в пакете. Отладчик может выполняться от точки останова в скрипте до точки останова, заданной для пакета задачи или контейнера, и наоборот. Например, для пакета могут существовать точки останова, заданные условиями останова, возникающими при получении пакетом событий **OnPreExecute** и **OnPostExecute** , а также задача «Скрипт» с точками останова для строк скрипта. В этом случае пакет может приостановить выполнение по условию останова, связанного с событием **OnPreExecute** , выполниться до точки останова в скрипте и в заключение до условия останова, связанного с событием **OnPostExecute** .  
  
 Дополнительные сведения об отладке задачи и компонента «Скрипт» см. в разделах [Coding and Debugging the Script Task](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) и [Coding and Debugging the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-visual-studio-for-applications"></a>Задание точки останова в Visual Studio для приложений  
  
-   [Отладка скрипта с помощью точек останова в задаче и компоненте «Скрипт»](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)  
  
## <a name="see-also"></a>См. также:  
 [Инструменты устранения неполадок при разработке пакета](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
