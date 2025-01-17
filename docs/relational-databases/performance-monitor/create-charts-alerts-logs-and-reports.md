---
title: Создание диаграмм, предупреждений, журналов и отчетов | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 5c30dbb3d6924187e5bc38ba06c4b291e264e526
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62706435"
---
# <a name="create-charts-alerts-logs-and-reports"></a>Создание диаграмм, предупреждений, журналов и отчетов
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Для контроля экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]системный монитор позволяет создавать диаграммы, предупреждения, журналы и отчеты.  
  
## <a name="charts"></a>Диаграммы  
 Диаграммы позволяют контролировать производительность выбранных объектов и состояние счетчиков, например загрузку ЦП или дисковый ввод-вывод. К диаграмме можно добавить различные сочетания объектов и счетчиков системного монитора. К диаграмме также можно добавить объекты и счетчики [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Каждая диаграмма представляет подмножество контролируемых данных. Например, одна диаграмма может отслеживать статистику использования памяти, а вторая — статистику операций дискового ввода-вывода.  
  
 Диаграммы полезно использовать при выполнении следующих задач.  
  
-   Исследование причин медленной или неэффективной работы компьютера или приложения.  
  
-   Постоянный контроль различных систем для обнаружения периодических проблем с производительностью.  
  
-   Определение момента, когда требуется увеличить емкость.  
  
-   Отображение тренда в виде линии диаграммы.  
  
-   Отображение сравнительных данных в виде гистограммы.  
  
 Диаграммы полезно использовать для кратковременного контроля показателей локального или удаленного компьютера в реальном времени (например, контроля возникновения определенных событий).  
  
## <a name="alerts"></a>видны узлы  
 При помощи предупреждений системный монитор отслеживает определенные события и уведомляет выбранным способом. В журнал предупреждений можно записывать текущее состояние выбранных счетчиков производительности и экземпляров объектов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Когда счетчик превышает заданное значение, в журнал записываются соответствующие дата и время. Предупреждения о событиях можно передавать по сети. Кроме того, можно указать программу, которую необходимо запускать при первом или каждом возникновении события. Например, можно передать по сети сообщение всем системным администраторам о том, что экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не хватает пространства на диске.  
  
## <a name="logs"></a>Журналы  
 Журналы позволяют записывать сведения о текущей активности выбранных объектов и компьютеров для последующего просмотра и анализа. В один файл журнала можно записывать данные нескольких систем. Например, можно создать различные журналы для сбора сведений о производительности выбранных объектов на разных компьютерах для последующего анализа. Журнал с выбранными настройками можно сохранить в отдельном файле и использовать его для создания других журналов, которые должны содержать аналогичные сведения.  
  
 Файлы журнала предоставляют сведения для устранения неполадок и планирования. В отличие от диаграмм, предупреждений и отчетов, которые предоставляют сведения о текущей активности, файлы журнала позволяют отслеживать состояние счетчиков за длительное время. Таким образом, они позволяют более тщательно контролировать и изучать сведения о производительности системы.  
  
## <a name="reports"></a>Отчеты  
 Отчеты позволяют посмотреть состояние постоянно меняющегося счетчика и значения экземпляров выбранных объектов. Значения отображаются для каждого экземпляра. Можно настроить период отчета, напечатать моментальные снимки и экспортировать данные. Используйте отчеты, если требуются необработанные данные.  
  
 Дополнительные сведения о создании диаграмм, предупреждений, журналов и отчетов и об объектах и счетчиках Windows см. в документации по Windows.  
  
## <a name="see-also"></a>См. также:  
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
