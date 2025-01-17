---
title: Методы дискретизации (интеллектуальный анализ данных) | Документация Майкрософт
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 610108ce4edb6e3beb5c13398d0a79eca200bdba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467765"
---
# <a name="discretization-methods-data-mining"></a>Методы дискретизации (Интеллектуальный анализ данных)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Некоторые алгоритмы, используемые для создания моделей интеллектуального анализа данных в службах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , для своей работы требуют наличия специальных типов содержимого. Например, упрощенный алгоритм Байеса [!INCLUDE[msCoName](../../includes/msconame-md.md)] не может использовать непрерывные столбцы на входе и прогнозировать непрерывные значения. Кроме того, некоторые столбцы могут содержать так много значений, что алгоритм будет не в состоянии легко выявить содержательные закономерности в данных, из которых создается модель.  
  
 В таких случаях можно дискретизировать данные в столбцах, чтобы воспользоваться алгоритмами для выработки модели интеллектуального анализа данных. *Дискретизация* — это процесс разделения значений на сегменты, результатом которого является ограниченное число допустимых состояний. С самими сегментами обращаются как с упорядоченными дискретными значениями. Можно дискретизировать как численные, так и строковые столбцы.  
  
 Существует несколько способов дискретизации данных. Если в решении по интеллектуальному анализу данных используются реляционные данные, можно ограничить число сегментов, используемых для группирования данных, задав свойство <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . Число сегментов по умолчанию равно 5.  
  
 Если в решении интеллектуального анализа данных используются данные из куба оперативной аналитической обработки (OLAP), то алгоритм интеллектуального анализа данных автоматически вычислит число создаваемых сегментов по следующей формуле, где n — это число уникальных значений данных в столбце:  
  
 `Number of Buckets = sqrt(n)`  
  
 Если вам не нужно, чтобы службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] вычисляли число сегментов, можно воспользоваться свойством <xref:Microsoft.AnalysisServices.DimensionAttribute.DiscretizationBucketCount%2A> и указать число сегментов вручную.  
  
 Следующая таблица описывает методы, которые можно использовать для дискретизации данных в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Метод дискретизации|Описание|  
|---------------------------|-----------------|  
|**AUTOMATIC**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] определяют, какой метод дискретизации использовать.|  
|**CLUSTERS**|Алгоритм разделяет данные на группы путем создания выборки обучающих данных, инициализации по ряду случайных точек и дальнейшего запуска несколько итераций алгоритма кластеризации (Майкрософт) с помощью метода кластеризации с максимизацией ожидания (EM). Метод **CLUSTERS** полезен, так как он работает с любой кривой распределения. Однако он требует большего времени на обработку, чем другие методы дискретизации.<br /><br /> Этот метод можно использовать только для числовых столбцов.|  
|**EQUAL_AREAS**|Алгоритм делит данные на группы, содержащие равное число значений. Этот метод лучше всего использовать для кривых нормального распределения, но он не работает, если распределение содержит большое число значений, встречающихся в узкой группе непрерывных данных. Например, если половина элементов имеет значение цены 0, то половина данных окажется в одной точке кривой. При таком распределении, этот метод разрушит данные в попытке установить равномерную дискретизацию по нескольким областям. Это вызовет неточное представление данных.|  
  
## <a name="remarks"></a>Примечания  
  
-   Метод **EQUAL_AREAS** позволяет выполнять дискретизацию строк.  
  
-   Метод **CLUSTERS** использует случайную выборку из 1 000 записей для дискретизации данных. Если вам не нужно, чтобы алгоритм отбирал данные, выбирайте метод **EQUAL_AREAS** .  
  
  
  
## <a name="see-also"></a>См. также  
 [Типы содержимого (интеллектуальный анализ данных)](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Типы содержимого (расширения интеллектуального анализа данных)](../../dmx/content-types-dmx.md)   
 [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Структуры интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Типы данных (интеллектуальный анализ данных)](../../analysis-services/data-mining/data-types-data-mining.md)   
 [Столбцы структуры интеллектуального анализа данных](../../analysis-services/data-mining/mining-structure-columns.md)   
 [Распределения столбцов (интеллектуальный анализ данных)](../../analysis-services/data-mining/column-distributions-data-mining.md)  
  
  
