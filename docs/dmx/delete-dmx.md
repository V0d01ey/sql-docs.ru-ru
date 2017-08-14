---
title: "DELETE (DMX) | Документы Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DELETE
dev_langs:
- DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00be9b52e652e2a2456cdbcd589f048d8a971d47
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="delete-dmx"></a>DELETE (расширения интеллектуального анализа данных)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Позволяет удалить модель, структуру интеллектуального анализа данных или структуру вместе со всеми связанными моделями, в зависимости от используемых предложений расширений интеллектуального анализа данных.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Аргументы  
 *model*  
 Идентификатор модели.  
  
 *Структура*  
 Идентификатор структуры.  
  
## <a name="remarks"></a>Замечания  
 Если вы не укажете **модель интеллектуального анализа данных** или **СТРУКТУРА интеллектуального анализа данных**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] выполняет поиск типа объекта, на основе имени и обрабатывает корректный объект. Если сервер содержит структуру и модель интеллектуального анализа данных с одинаковыми именами, возвращается ошибка.  
  
 В следующей таблице описан результат использования различных форм синтаксиса.  
  
|.|Результат|  
|---------------|------------|  
|УДАЛИТЬ из СТРУКТУРЫ интеллектуального анализа данных*\<структура >*<br /><br /> либо<br /><br /> УДАЛИТЬ из СТРУКТУРЫ интеллектуального анализа данных*\<структуры >*. СОДЕРЖИМОЕ|Выполняет ProcessClear структуры интеллектуального анализа данных. Все содержимое структуры интеллектуального анализа данных и связанных с ней моделей интеллектуального анализа данных удаляется.|  
|УДАЛИТЬ из СТРУКТУРЫ интеллектуального анализа данных*\<структуры >*. ВАРИАНТЫ|Выполняет ProcessClearStructureOnly структуры интеллектуального анализа данных. Все содержимое структуры интеллектуального анализа данных удаляется, а связанные с ней модели интеллектуального анализа данных остаются без изменений. После удаления структуры интеллектуального анализа данных детализация связанных с ней моделей становится невозможной.|  
|УДАЛИТЬ из МОДЕЛИ интеллектуального анализа данных*\<модели >*<br /><br /> либо<br /><br /> УДАЛИТЬ из МОДЕЛИ интеллектуального анализа данных*\<модели >*. СОДЕРЖИМОЕ|Выполняет ProcessClear по модели интеллектуального анализа данных, но значения состояний оставляются без изменений. Значения состояний представляют собой возможные состояния столбца. Например, значениями состояний для столбца «Пол» являются «Мужской» и «Женский».|  
  
 Дополнительные сведения о типах обработки см. в разделе [элемента типа &#40; XML для Аналитики &#41; ](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>Примеры  
 Следующий пример удаляет все содержимое модели NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>См. также:  
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции определения данных](../dmx/dmx-statements-data-definition.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции управления данными](../dmx/dmx-statements-data-manipulation.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
