---
title: Сопоставление трассировки с журналом производительности Windows | Документы Майкрософт
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bdbd634a74c5e7cd48232a28ab4c7709e8febfad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033775"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Сопоставление трассировки с журналом производительности Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  С помощью приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]можно открыть журнал производительности Microsoft Windows, выбрать счетчики, которые нужно сопоставить с трассировкой, и отобразить выбранные счетчики производительности рядом с трассировкой в графическом пользовательском интерфейсе приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . При выборе события в окне трассировки вертикальная красная линия на панели окна системного монитора в приложении [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] показывает данные журнала производительности, которые сопоставлены выбранному событию трассировки.  
  
 Чтобы сопоставить трассировку со счетчиками производительности, откройте файл трассировки или таблицу, содержащую столбцы данных **Начальное время** и **Конечное время** data columns, и then click **Импортировать данные производительности** в меню приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Файл** . Потом можно открыть журнал производительности и выбрать объекты системного монитора и счетчики, которые сопоставляются с трассировкой.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Согласование трассировки с данными журнала производительности  
  
1.  В [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]откройте сохраненный файл трассировки или таблицу трассировки. Нельзя согласовывать запущенную трассировку, которая производит сбор данных события. Чтобы гарантировать точность связывания с данными системного монитора, трассировка должна содержать столбцы данных **StartTime** и **EndTime** .  
  
2.  В меню [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **приложения** выберите **Импорт данных производительности**.  
  
3.  В диалоговом окне **Открыть** выберите файл с журналом производительности. Чтобы данные журнала производительности можно было связать с трассировкой, они должны быть собраны в то же время, что и данные трассировки.  
  
4.  В диалоговом окне **Ограничение счетчиков производительности** установите флажки, относящиеся к объектам и счетчикам системного монитора, которые необходимо отобразить наряду с трассировкой. Нажмите кнопку **ОК.**  
  
5.  Выберите событие в окне событий трассировки или используйте клавиши со стрелками, чтобы перемещаться по строкам в окне событий трассировки. Красная вертикальная черта в окне **Данные системного монитора** указывает на данные журнала производительности, связанные с выбранным событием трассировки.  
  
6.  Выберите интересующую точку на графике системного монитора. Выбирается соответствующая трассировка строки, ближайшая по времени к выбранной точке. Чтобы увеличить временной диапазон, удерживая клавишу мыши, перетащите ее указатель по графику системного монитора.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Создание журналов производительности, общих для различных версий Windows  
  
1.  На панели управления выберите пункт **Администрирование**, а затем дважды щелкните элемент **Производительность**.  
  
2.  В диалоговом окне **Производительность** разверните **Оповещения и журналы производительности**, щелкните правой кнопкой мыши **Журналы счетчиков**и выберите **Новые параметры журнала**.  
  
3.  Введите имя журнала счетчиков и нажмите кнопку **ОК**.  
  
4.  На вкладке **Общие** щелкните **Добавить счетчики**.  
  
5.  В списке **Объект производительности** выберите объект, который требуется контролировать. Названия объектов производительности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для экземпляров по умолчанию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] начинаются с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , а именованные экземпляры начинаются с MSSQL$*instanceName*.  
  
6.  Добавьте к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] необходимое количество счетчиков и прочие важные значения, такие как процессорное время и время диска.  
  
7.  После завершения добавления счетчиков нажмите кнопку **Закрыть**.  
  
8.  Установите значения для интервала **Снимать показания каждые** . Начинайте с интервала в 5 минут, и затем корректируйте его по необходимости.  
  
9. На вкладке **Файлы журналов** выберите **Текстовый файл (разделители-запятые)** в списке **Тип файла журнала** . Текстовые файлы журнала с разделителями-запятыми подходят для различных версий Windows; кроме того, их можно просматривать при помощи таких средств, как Microsoft Excel.  
  
10. На вкладке **Расписание** укажите расписание контроля.  
  
11. Нажмите кнопку **ОК** для создания журнала производительности.  
