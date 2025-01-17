---
title: Сведения о публикации, предупреждения (публикация транзакций) | Документация Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95074e741823747ba861efcfa6c025b5fb2c9e53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704389"
---
# <a name="publication-information-warnings-transactional-publication"></a>Сведения о публикации, предупреждения (публикация транзакций)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Вкладка **Предупреждения** доступна для распространителей, работающих с [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздними версиями. Вкладка **Предупреждения** позволяет выполнять следующие задачи для выбранных публикаций:  
  
-   включать предупреждения, которые будут отображаться в мониторе репликации;  
  
-   указать пороговые значения для предупреждений;  
  
-   указать оповещения, связанные с предупреждениями;  
  
## <a name="warnings-thresholds-and-alerts"></a>Предупреждения, пороговые значения и оповещения  
 По умолчанию монитор репликации отображает предупреждения для неинициализированных подписок: состояние **Неинициализированная подписка** отображается в виде предупреждения в столбце **Состояние** страниц, содержащих сведения о подписке. Для публикаций транзакций можно задать, должны ли такие дополнительные условия приводить к выдаче следующего предупреждения:  
  
-   Приближение даты истечения срока подписки.  
  
     Это соответствует параметру **Предупреждать, если действие подписки истекает до порогового значения**. Если указанное пороговое значение достигнуто или превышено, состояние подписки отображается как **Срок действия скоро истекает или истек** (в том случае если не требуется отобразить более важную информацию).  
  
-   Превышение заданной задержки. Время, прошедшее между фиксацией транзакции на издателе и фиксацией соответствующей транзакции на подписчике.  
  
     Это соответствует параметру **Предупредить, если задержка превышает пороговое значение**. Если указанное пороговое значение достигнуто или превышено, состояние подписки отображается как **Критическое для производительности** (в случае если не требуется отобразить более приоритетные сведения). Порог также используется для определения оценки производительности, которая отображается в столбце **Производительность** на страницах с данными о подписке. Рейтинг производительности может иметь одно из следующих значений.  
  
    -   Высокая  
  
    -   Хорошая.  
  
    -   удовлетворительная  
  
    -   Низкая  
  
    -   Критическая  
  
 При включении предупреждения задается пороговое значение. Например, если включено предупреждение **Предупредить, если задержка превышает пороговое значение**, выберите допустимый интервал времени между фиксацией транзакции на издателе и фиксацией транзакции на подписчике.  
  
 Достижение порогового значения помимо отображения предупреждения в мониторе репликации может также вызывать системное предупреждение. Предупреждения определяются нажатием кнопки **Настройка предупреждений** и указанием сведений в диалоговом окне **Настройка предупреждений репликации** .  
  
## <a name="options"></a>Параметры  
 **Включено**  
 Выберите, чтобы включить предупреждение и указать пороговое значение.  
  
 **Предупреждение**  
 Описание предупреждения, связанного с пороговым значением.  
  
 **Порог**  
 Укажите пороговое значение.  
  
 **Настройка предупреждений**  
 Выберите строку в сетке **Предупреждения** и нажмите кнопку **Настройка предупреждений** для запуска диалогового окна **Настройка предупреждений репликации** . Это диалоговое окно позволяет определить оповещение, связанное с выбранным пороговым значением и предупреждением.  
  
 **Отменить изменения**  
 Нажмите эту кнопку для отмены всех произведенных изменений предупреждениях и пороговых значениях.  
  
> [!NOTE]  
>  Нажатие кнопки **Отменить изменения** не затрагивает предупреждения, определенные в диалоговом окне **Настройка предупреждений репликации** .  
  
 **Сохранить изменения**  
 Нажмите эту кнопку для сохранения всех произведенных изменений предупреждений и пороговых значений.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач с помощью монитора репликации](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Наблюдение за производительностью с помощью монитора репликации](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
