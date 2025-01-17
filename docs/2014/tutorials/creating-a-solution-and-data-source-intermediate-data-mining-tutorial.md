---
title: Создание решения и источника данных (учебник по интеллектуальному анализу интеллектуальному анализу данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2f089f487586b6def3d2ddd4eecdbbde1532952b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62855344"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>Создание решения и источника данных (учебник по интеллектуальному анализу данных — средний уровень)
  Для работы с интеллектуальным анализом данных необходимо сначала создать проект в среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] на основе шаблона **Проект многомерных данных и интеллектуального анализа данных служб Analysis Services**. После открытия шаблона он загружает в конструктор все схемы, которые могут понадобиться для интеллектуального анализа данных: источники данных, структуры и модели интеллектуального анализа данных и даже кубы, если в структуре интеллектуального анализа данных используются многомерные данные.  
  
 При создании проекта решение сохраняется в виде локального файла до момента развертывания решения. При развертывании решения службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ищут сервер служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , указанный в свойствах проекта, и создают новую базу данных [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , имя которой совпадает с именем проекта. По умолчанию службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] используют для новых проектов экземпляр **localhost** . Если используется именованный экземпляр или экземпляру по умолчанию задано другое имя, нужно изменить свойство развертывания базы данных проекта, чтобы указать папку, в которой будут создаваться объекты интеллектуального анализа данных.  
  
 Дополнительные сведения о [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] проектов, см. в разделе [Создание проекта служб Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md).  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>Создание нового проекта служб Analysis Services для данного учебника  
  
1.  Откройте [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  В меню **Файл** укажите **Создать**, затем нажмите **Проект**.  
  
3.  Выберите **Проект многомерных данных и интеллектуального анализа данных служб Analysis Services** на панели **Установленные шаблоны** .  
  
4.  В поле **Имя** введите для нового проекта имя **DM Intermediate**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>Изменение экземпляра, в котором хранятся объекты интеллектуального анализа данных (необязательно)  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]в меню **Проект** выберите пункт **Свойства**.  
  
2.  В левой части панели **Страницы свойств** щелкните элемент **Развертывание**.  
  
3.  Убедитесь, что поле **Сервер** содержит значение **localhost**. Если используется другой экземпляр, введите имя этого экземпляра. Если используется именованный экземпляр служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], введите имя компьютера и имя экземпляра. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>Изменение свойств развертывания для проекта (необязательно)  
  
1.  В обозревателе решений щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.  
  
     или  
  
     В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], в меню **Проект** выберите **Свойства**.  
  
2.  В левой части панели **Страницы свойств** щелкните элемент **Развертывание**.  
  
     На панели **Параметры** выберите пункт **Режим развертывания**и установите значение **Развернуть все** для перезаписи либо значение **Только развертывание изменений** для обновления объектов или добавления новых.  
  
## <a name="creating-a-data-source"></a>Создание источника данных  
 В учебнике по интеллектуальному анализу данных (начальный уровень) был создан *источник данных* , в котором хранятся сведения о соединении для базы данных [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] . Выполните те же шаги, чтобы создать источник данных [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] в этом решении.  
  
#### <a name="to-create-a-data-source"></a>Создание источника данных  
  
-   [Создание источника данных &#40;учебник интеллектуального анализа данных&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 Один источник данных может поддерживать несколько представлений источника данных, а каждое представление источника данных может иметь несколько таблиц. Однако, поскольку источник данных и представление источника данных развертываются в базе данных служб [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] вместе с создаваемыми моделями интеллектуального анализа данных, рекомендуется включить в представление источника данных только те таблицы, которые необходимы для каждой модели интеллектуального анализа данных или группы таких моделей.  
  
 На следующих занятиях мы добавим представления источников данных для поддержки каждого из новых сценариев. Только в занятиях по анализу потребительской корзины и кластеризации последовательностей используется одно представление источника данных. Но во всех остальных отношениях эти занятия не связаны между собой и могут изучаться раздельно.  
  
|Сценарий|Данные, включенные в представление источника данных|  
|--------------|-------------------------------------------|  
|[Занятие 2. Построение сценария прогнозирования &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|Ежемесячные отчеты по продажам в разрезе моделей велосипедов в различных регионах, собранных в единое представление.|  
|[Занятие 3. Построение сценария потребительской корзины &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|Таблица, содержащая список клиентских заказов, а также вложенная таблица, показывающая конкретные покупки для каждого из клиентов.|  
|[Занятие 4. Построение сценария кластеризации последовательностей &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|Для анализа покупательского поведения используются те же данные за добавлением идентификатора, который показывает, в каком порядке производились покупки.|  
|[Занятие 5. Построение моделей логистической регрессии нейронной сети и &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|В одной таблице содержатся некоторые предварительные данные отслеживания производительности, получаемые из центра обработки вызовов.|  
  
## <a name="next-lesson"></a>Следующее занятие  
 [Занятие 2. Построение сценария прогнозирования &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>См. также  
 [Проекты интеллектуального анализа данных](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [Представления источников данных в многомерных моделях](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
