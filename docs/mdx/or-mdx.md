---
title: OR (МНОГОМЕРНЫЕ ВЫРАЖЕНИЯ) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae6b6602d7968bb444dcf4838537bb000b97dd53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278262"
---
# <a name="or-mdx"></a>OR (многомерные выражения)


  Выполняет логическое сложение двух числовых выражений.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Параметры  
 Expression1  
 Допустимое многомерное выражение, возвращающее числовое значение.  
  
 Expression2  
 Допустимое многомерное выражение, возвращающее числовое значение.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Логическое значение, возвращающее **true** , если один или оба аргумента имеют значение **true**; в противном случае **false**.  
  
## <a name="remarks"></a>Примечания  
 **Или** оператор рассматривает оба аргумента как логические (значение 0, соответствует **false**; в противном случае **true**) прежде, чем оператор выполнит логическое сложение. В следующей таблице показано как **или** оператор выполнит логическое сложение.  
  
|*Expression1*|*Expression2*|Возвращаемое значение|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Пример  
 Приведенный ниже запрос содержит вычисляемую меру, возвращающую строку «MARRIED OR MALE», если текущий элемент иерархии Gender измерения Customer имеет значение Male либо текущий элемент иерархии измерения «Заказчик» семейное женился; в противном случае возвращается строка «UNMARRIED или FEMALE».  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по операторам многомерных Выражений &#40;многомерных Выражений&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
