---
title: xml (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a61816e39947bede45fff894facab912617b49be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859880"
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Тип данных, в котором хранятся XML-данные. Можно хранить экземпляры **xml** в столбце либо в переменной типа **xml**.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>Аргументы  
 CONTENT  
 Экземпляр **xml** должен быть XML-фрагментом правильного формата. XML-данные могут содержать несколько (0 или больше) элементов верхнего уровня. Текстовые узлы разрешены на верхнем уровне.  
  
 Это поведение по умолчанию.  
  
 DOCUMENT  
 Экземпляр **xml** должен быть XML-документом правильного формата. XML-данные должны содержать только один корневой элемент. Текстовые узлы на верхнем уровне запрещены.  
  
 *xml_schema_collection*  
 Имя коллекции XML-схем. Чтобы создать типизированный столбец или переменную **xml**, можно дополнительно указать имя коллекции XML-схем. Дополнительные сведения о типизированном и нетипизированном XML см. в разделе [Сравнение типизированного и нетипизированного XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="remarks"></a>Remarks  
 Размер хранимого представления экземпляров типа данных **xml** не может превышать 2 ГБ.  
  
 Аспекты CONTENT и DOCUMENT применяются только к типизованным XML. Дополнительные сведения см. в статье [Сравнение типизированного и нетипизированного XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="examples"></a>Примеры  
  
```  
USE AdventureWorks;  
GO  
DECLARE @DemographicData xml (Person.IndividualSurveySchemaCollection);  
SET @DemographicData =  (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Преобразование типов данных (ядро СУБД)](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [методов типа данных xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Справочник по языку XQuery (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)  
  
  
