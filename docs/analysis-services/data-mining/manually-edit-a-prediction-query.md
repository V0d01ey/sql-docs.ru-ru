---
title: Изменение прогнозирующего запроса вручную | Документация Майкрософт
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aba181ab73ab730869eaa7930591cf21a947d20c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62679422"
---
# <a name="manually-edit-a-prediction-query"></a>Изменение прогнозирующего запроса вручную
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  После проектирования запроса с использованием построителя прогнозирующих запросов можно изменить этот запрос, переключившись в представление «Текст запроса» на вкладке **Прогноз модели интеллектуального анализа данных** конструктора интеллектуального анализа данных. В нижней части экрана появится текстовый редактор, отображающий запрос, созданный построителем запросов.  
  
 Переключение на представление «Текст запроса» полезно при внесении дополнений в запрос. Например, можно добавить предложение WHERE или ORDER BY.  
  
 С помощью сетки в построителе прогнозирующих запросов можно вставить имена объектов и столбцов и настроить синтаксис отдельных прогнозирующих функций, а затем переключиться в режим ручного редактирования для изменения значений параметров.  
  
> [!NOTE]  
>  При переключении из представления **Текст запроса** обратно в представление **Проектирование** все изменения, внесенные в представлении **Текст запроса** , будут потеряны.  
  
### <a name="modify-a-query"></a>Изменение запроса  
  
1.  На вкладке **Прогноз модели интеллектуального анализа данных** конструктора интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]нажмите кнопку **SQL**.  
  
     Сетка в нижней части экрана заменится текстовым редактором, содержащим запрос. В этом редакторе можно ввести в запрос изменения.  
  
2.  Чтобы запустить запрос, выберите в меню **Модель интеллектуального анализа данных** команду **Результат**или нажмите соответствующую кнопку для переключения на результаты запроса.  
  
    > [!NOTE]  
    >  Если созданный запрос содержит ошибку, в окне результатов не будут показаны результаты и не будет выведено сообщение об ошибке. Чтобы исправить ошибку, нажмите кнопку **Конструктор** или выберите один из пунктов — **Конструктор** или **Запрос** — в меню **Модель интеллектуального анализа данных** .  
  
## <a name="see-also"></a>См. также  
 [Запросы интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-queries.md)   
 [Построитель прогнозирующих запросов (интеллектуальный анализ данных)](http://msdn.microsoft.com/library/12900d49-db88-48bb-a5f4-0a9a172bc126)   
 [Занятие 6. Создание прогнозов и работа с &#40;учебник интеллектуального анализа данных&#41;](http://msdn.microsoft.com/library/b213cb58-2c40-4c89-b08b-d3c36a4afad3)  
  
  
