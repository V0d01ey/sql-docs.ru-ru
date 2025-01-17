---
title: Просмотр модели в средстве просмотра временных рядов | Документация Майкрософт
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd57ae140adee0909c0f00647a334bd62f26c170
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62671365"
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Просмотр модели с помощью средства просмотра временных рядов (Майкрософт)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  В средстве просмотра временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] в службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] отображаются модели интеллектуального анализа данных, построенные с помощью алгоритма временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Алгоритм временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] представляет собой алгоритм регрессии, который создает модели интеллектуального анализа данных для прогнозирования столбцов с непрерывными данными, таких, как данные о продажах продукта, в сценарии прогнозирования. Эти модели временных рядов могут включать информацию, основанную на других алгоритмах:  
  
-   Алгоритм ARTxp, оптимизированный для краткосрочного прогнозирования.  
  
-   Алгоритм ARIMA, оптимизированный для долгосрочного прогнозирования.  
  
-   Сочетание алгоритмов ARTxp и ARIMA.  
  
 Дополнительные сведения об этих алгоритмах см. в разделах [Microsoft Time Series Algorithm](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) и [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
> [!NOTE]  
>  Чтобы просмотреть подробные сведения об использованных в модели уравнениях и обнаруженных закономерностях, используйте средство просмотра деревьев содержимого общего вида [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Дополнительные сведения см. в разделах [Просмотр модели в средстве просмотра деревьев содержимого общего вида (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) и [Средство просмотра деревьев содержимого общего вида (Майкрософт) (интеллектуальный анализ данных)](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Вкладки средства просмотра  
 При просмотре модели интеллектуального анализа данных в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]модель отображается на вкладке **Средство просмотра моделей интеллектуального анализа данных** конструктора интеллектуального анализа данных с использованием соответствующего средства просмотра для данной модели. Средство просмотра временных рядов ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) содержит следующие вкладки:  
  
-   [Модель](#BKMK_Tree)  
  
-   [Диаграммы](#BKMK_Charts)  
  
 **Примечание** Информация, отображаемая для содержимого модели и к условным обозначениям интеллектуального анализа данных, зависит от используемого в модели алгоритма. Тем не менее, вкладки **Модель** и **Диаграммы** остаются одинаковыми, независимо от применяемого сочетания алгоритмов.  
  
###  <a name="BKMK_Tree"></a> Модель  
 При построении модели временных рядов службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] представляют завершенную модель в виде дерева. Если рассматриваемые данные содержат несколько рядов вариантов, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] формируют отдельное дерево для каждого ряда. Например, необходимо создать прогноз продаж для тихоокеанского, североамериканского и европейского регионов. Прогнозы для каждой из этих областей — это ряды вариантов. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] создают отдельное дерево для каждого из этих рядов. Чтобы рассмотреть конкретный ряд, выберите этот ряд из списка **Дерево** .  
  
 Для каждого дерева модель временных рядов содержит узел **Все** , затем делится на ряд узлов, которые представляют периодические структуры, обнаруженные алгоритмом. Можно щелкнуть каждый узел, чтобы отобразить статистические данные, например количество вариантов и уравнение.  
  
 Если модель создана только с помощью алгоритма ARTxp, то **Условные обозначения интеллектуального анализа данных** для корневого узла содержат лишь общее количество вариантов. Для каждого некорневого узла **Условные обозначения интеллектуального анализа данных** содержат более подробную информацию о разбиении дерева. В частности, они могут содержать уравнение для узла и количество вариантов. *Правило* в условных обозначениях содержит информацию, определяющую ряд и временной срез, к которому применяется правило. Например, текст в условных обозначениях `M200 Europe Amount -2` указывает, что этот узел представляет модель для ряда M200 Europe в период, расположенный два временных среза тому назад.  
  
 Если модель создана только с помощью алгоритма ARIMA, то на вкладке **Модель** находится единственный узел с заголовком **Все**. **Условные обозначения интеллектуального анализа данных** для корневого узла содержат уравнение ARIMA.  
  
 Если создана смешанная модель, корневой узел содержит лишь количество вариантов и уравнение ARIMA. За корневым узлом дерево разбивается на отдельные узлы, относящиеся к каждой периодической структуре. Для каждого некорневого узла в условных обозначениях интеллектуального анализа данных содержатся алгоритмы ARTxp и ARIMA, уравнение для узла и количество вариантов в узле. На первом месте находится уравнение ARTxp, которое отмечено как уравнение узла дерева. За ним следует уравнение ARIMA. Дополнительные сведения об интерпретации этой информации см. в разделе [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Как правило, в диаграмме дерева решений показано только наиболее важное разбиение, узел **Все** , слева от средства просмотра. В деревьях решений наиболее важным является разбиение, которое следует за узлом **Все** , поскольку оно содержит условие, наиболее строго разделяющее варианты в наборе обучающих данных. В модели временных рядов с помощью основного ветвления обозначается наиболее вероятный сезонный цикл. Разбиения, которые следуют за узлом **Все** , отображаются справа от ветви.  
  
 Индивидуальные узлы в дереве можно развернуть или свернуть, чтобы отобразить или скрыть разбиения, происходящие после каждого узла. Кроме этого, можно воспользоваться параметром на вкладке **Дерево решений** для изменения способа отображения дерева. Используйте ползунок **Показать уровень** для установки количества уровней, отображаемых в дереве. Используйте ползунок **Расширение по умолчанию** для установки количества уровней по умолчанию, которые отображаются для всех деревьев в модели.  
  
 Заливка фонового цвета каждого узла обозначает количество вариантов в узле. Чтобы найти точное значение вариантов в узле, наведите указатель на узел, чтобы просмотреть всплывающую подсказку.  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> Диаграммы  
 На вкладке **Диаграммы** отображается диаграмма, показывающая поведение прогнозируемого атрибута во времени, вместе с пятью прогнозируемыми будущими значениями. Вертикальная ось диаграммы представляет значение ряда, а горизонтальная — время.  
  
> [!NOTE]  
>  Временные срезы, используемые на временной оси, зависят от единиц, используемых в конкретных данных: они могут представлять дни, месяцы или даже секунды.  
  
 Используйте кнопку **Абс** для переключения между абсолютными и относительными кривыми. Если диаграмма содержит несколько моделей, масштаб данных для каждой модели может значительно различаться. При использовании абсолютной кривой одна модель может выглядеть как плоская линия, тогда как в других моделях будут отображаться значительные изменения. Это происходит из-за того, что масштаб одной модели больше масштаба другой модели. Переключение к относительным кривым приводит к изменению масштаба, в результате чего отображаются изменения в процентах, а не абсолютные значения. Благодаря этому становится проще сравнивать модели, основанные на различных масштабах.  
  
 Если модель интеллектуального анализа данных включает несколько временных рядов, для отображения на диаграмме можно выбрать один или несколько рядов. Достаточно щелкнуть список справа от средства просмотра и выбрать необходимые ряды из списка. Если диаграмма становится слишком сложной, можно отфильтровать отображаемые ряды, устанавливая или снимая флажки рядов в условных обозначениях.  
  
 Диаграмма отображает как данные с предысторией, так и будущие данные. Будущие данные затенены, что позволяет отличить их от данных с предысторией. Значения данных отображаются в виде сплошных линий (для данных с предысторией) и пунктирных линий (для прогнозируемых данных). Можно изменить цвет линий, используемых для каждой последовательности, установив свойства в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Дополнительные сведения см. в разделе [Изменение цветов, используемых в средствах просмотра интеллектуального анализа данных](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 Можно настроить отображаемый диапазон времени, используя параметры увеличения. Также можно просмотреть конкретный временной диапазон, щелкнув диаграмму, перетащив выбранное время по диаграмме и щелкнув вновь для увеличения выбранного диапазона.  
  
 С помощью списка **Этапы прогнозирования** можно выбрать количество отображаемых в модели будущих временных **шагов**. Если установлен флажок **Отображать отклонения** , средство просмотра добавляет диаграммы погрешностей, чтобы можно было видеть, насколько точным является прогнозируемое значение.  
  
 [В начало](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>См. также  
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft Time Series Algorithm](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Примеры запросов моделей временных рядов](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
