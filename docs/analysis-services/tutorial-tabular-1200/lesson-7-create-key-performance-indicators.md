---
title: 'Занятие 7: Создание ключевых показателей эффективности | Документация Майкрософт'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21767c239ed3498e0e593e221203b1cde3b7ae69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403876"
---
# <a name="lesson-7-create-key-performance-indicators"></a>Занятие 7: Создание ключевых показателей эффективности
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

На этом занятии мы создадим ключевые показатели эффективности (KPI). KPI используются для измерения производительности значения, определенного *базовой* мерой относительно *целевого* значения, определенного мерой, или абсолютного значения. В клиентских приложения создания отчетов показатели KPI предоставляют бизнесменам быстрый и легкий способ получения обзорных сведений о развитии бизнеса или определении тенденций. Дополнительные сведения см. в разделе [ключевые показатели эффективности](../tabular-models/kpis-ssas-tabular.md).  
  
Предполагаемое время для выполнения этого занятия: **15 минут**  
  
## <a name="prerequisites"></a>предварительные требования  
Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Перед выполнением задач на этом занятии, необходимо завершить предыдущее занятие: [Занятие 6. Создание мер](lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Создание ключевых показателей эффективности  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Для создания ключевого показателя Эффективности InternetCurrentQuarterSalesPerformance  
  
1.  В конструкторе моделей щелкните **FactInternetSales** таблицу (вкладку).  
  
2.  В сетке мер щелкните пустую ячейку.  
  
3.  В строке формул над таблицей введите следующую формулу: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IFERROR([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Эта мера будет служить базовой мерой для KPI.  
  
4.  Щелкните правой кнопкой мыши **InternetCurrentQuarterSalesPerformance** > **создать ключевой показатель Эффективности**.   
  
5.  В диалоговом окне ключевого индикатора производительности (KPI) в **целевой** выберите **абсолютное значение**, а затем введите **1.1**.  
  
7.  В левом (нижнем) поле ползунка введите **1**, а затем в правом (верхнем) поле ползунка введите **1,07**.  
  
8.  На вкладке **Выберите стиль значка**выберите тип значков: ромб (красный), треугольник (желтый), круг (зеленый).
  
    ![как табличных lesson7-ключевого показателя эффективности](media/as-tabular-lesson7-kpi.png)
    
    > [!TIP]  
    > Обратите внимание на развертываемую **описания** подпись под доступными стилями значков. Позволяет вводить описания для различных элементов KPI, чтобы сделать их более понятными в клиентских приложениях.  
  
9. Чтобы завершить создание ключевого показателя эффективности, нажмите кнопку **ОК** .  
  
    В сетке мер Обратите внимание на значок рядом с полем **InternetCurrentQuarterSalesPerformance** мер. Этот значок указывает, что мера служит базовым значением для KPI.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Для создания ключевого показателя Эффективности InternetCurrentQuarterMarginPerformance  
  
1.  В сетке мер для **FactInternetSales** таблицы, щелкните пустую ячейку.  
  
2.  В строке формул над таблицей введите следующую формулу:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Щелкните правой кнопкой мыши **InternetCurrentQuarterMarginPerformance** > **создать ключевой показатель Эффективности**.  
  
4.  В диалоговом окне ключевого индикатора производительности (KPI) в **целевой** выберите **абсолютное значение**, а затем введите **1,25**.   
  
5.  В поле **Определите пороговые значения состояния**переместите левое (нижнее) поле ползунка так, чтобы в нем отображалось значение **0,8**, а затем переместите правое (верхнее) поле ползунка так, чтобы в нем отображалось значение **1,03**.  
  
6.  На вкладке **Выберите стиль значка**выберите тип значков: ромб (красный), треугольник (желтый), круг (зеленый). Затем нажмите кнопку **OK**.  
  
## <a name="whats-next"></a>Дальнейшие действия
Перейдите к следующему занятию: [Занятие 8. Создание перспектив](lesson-8-create-perspectives.md).
  
  
