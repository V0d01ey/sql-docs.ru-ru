---
title: Правила использования методов типа данных XML | Документы Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 890e5d02f72f9af0d0609602e3815b872d870b45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62928976"
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Правила использования методов типа данных XML

[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

В этом разделе описываются правила использования методов типа данных **xml**.

## <a name="the-print-statement"></a>Инструкция PRINT

Методы типа данных **xml** не могут быть использованы в инструкции PRINT, как показано в следующем примере. Методы типа данных **xml** обрабатываются как подзапросы, а подзапросы в инструкции PRINT не разрешены. В результате следующий пример возвращает ошибку:

```sql
DECLARE @x xml
SET @x = '<root>Hello</root>'
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)
```

В качестве решения можно вначале присвоить результат метода **value()** переменной типа **xml**, а потом использовать переменную в запросе.

```sql
DECLARE @x xml
DECLARE @c varchar(max)
SET @x = '<root>Hello</root>'
SET @c = @x.value('/root[1]', 'varchar(11)')
PRINT @c
```

## <a name="the-group-by-clause"></a>Предложение GROUP BY

Методы типа данных **xml** интерпретируются внутри как подзапросы. Так как предложение GROUP BY требует скалярного выражения и не принимает статистических вычислений или подзапросов, нельзя указывать методы типа данных **xml** в предложении GROUP BY. Решением является вызов пользовательской функции, которая использует методы XML.

## <a name="reporting-errors"></a>Ведение отчетов об ошибках

При сообщении об ошибках методы типа данных **xml** вызывают ошибки в следующем формате:

```
Msg errorNumber, Level levelNumber, State stateNumber:
XQuery [database.table.method]: description_of_error
```

Пример:

```
Msg 2396, Level 16, State 1:
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element
```

## <a name="singleton-checks"></a>Одноэлементные проверки

Шаги определения расположения данных, параметры функций и операторы, которым нужны единственные значения, возвращают ошибку, если компилятор не может определить, будет ли в период выполнения гарантирована единственность элемента. Эта проблема часто возникает при работе с нетипизированными данными. Например, при уточняющем запросе атрибута необходима информация о единственном родительском элементе. Указать порядковый номер, выбирающий единственный родительский узел, недостаточно. Чтобы извлечь значения атрибутов при обработке комбинации **node()** -**value()** , указание порядкового номера, возможно, не потребуется. Это показано в следующем примере.

### <a name="example-known-singleton"></a>Пример Известный единственный экземпляр

В этом примере метод **nodes()** создает отдельную строку для каждого элемента `<book>`. Метод **value()** , выполняемый для узла `<book>`, извлекает значение `@genre`, которое, будучи атрибутом, является единственным.

```sql
SELECT nref.value('@genre', 'varchar(max)') LastName
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)
```

Чтобы проверить типы типизированного XML, используется XML-схема. Если в XML-схеме узел указан как единственный, компилятор это учитывает, и ошибки не возникают. В противном случае необходим порядковый номер, выбирающий единственный узел. В частности, применение оси нижнего или этого же уровня (//), такой как `/book//title`, ослабляет вывод единственности элемента `<title>`, несмотря на то что в схеме XML он указан именно так. Поэтому следует переписать его как `(/book//title)[1]`.

Важно знать о различии между выражениями `//first-name[1]` и `(//first-name)[1]` при проверке типов. Первое из них возвращает последовательность узлов `<first-name>`, в которой каждый узел является самым левым узлом `<first-name>` среди узлов с общим родителем. Второе возвращает первый единственный узел `<first-name>` в порядке документа в экземпляре XML.

### <a name="example-using-value"></a>Пример Использование метода value()

Следующий запрос данных из нетипизированного столбца XML приводит к статической ошибке компиляции. Это объясняется тем, что метод **value()** ожидает в качестве первого аргумента единственный узел, а компилятор не может определить, будет ли в период выполнения существовать только один узел `<last-name>`:

```sql
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName
FROM   T
```

Вот решение этой проблемы, которое возможно как вариант:

```sql
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName
FROM   T
```

Однако это решение не устраняет ошибку, потому что в каждом экземпляре XML могут содержаться несколько узлов `<author>`. Следующий вариант работает:

```sql
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName
FROM   T
```

Этот запрос возвращает значение первого элемента `<last-name>` в каждом из экземпляров XML.

## <a name="see-also"></a>См. также:

- [Методы для типа данных XML](../../t-sql/xml/xml-data-type-methods.md)
