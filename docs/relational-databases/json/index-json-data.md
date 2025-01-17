---
title: Индексирование данных JSON | Документация Майкрософт
ms.custom: ''
ms.date: 06/01/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d87675c4feb0ab784f0003143406b3784f7e8a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62716688"
---
# <a name="index-json-data"></a>Индексирование данных JSON
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

JSON не является встроенным типом данных в SQL Server и базе данных SQL, а SQL Server не имеет пользовательских индексов JSON. Запросы к документам JSON можно оптимизировать с помощью обычных индексов. 

Индексы баз данных делают операции фильтрации и сортировки более эффективными. Без индексов SQL Server пришлось бы сканировать всю таблицу при каждом запросе данных.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Индексация свойств JSON с помощью вычисляемых столбцов  
При хранении данных JSON в SQL Server результаты запросов обычно нужно фильтровать или сортировать по одному или нескольким *свойствам* документов JSON.  

### <a name="example"></a>Пример 
В этом примере предполагается, что таблица AdventureWorks `SalesOrderHeader` включает столбец `Info`, содержащий различные сведения в формате JSON о заказах на продажу. Например, он содержит сведения о клиенте и менеджере по продажам, адреса доставки и выставления счетов и т. д. Значения из столбца `Info` можно использовать для фильтрования заказов на продажу по клиентам.

### <a name="query-to-optimize"></a>Запрос оптимизации
С помощью индекса можно оптимизировать запросы, например, указанного ниже типа.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Пример индекса
Чтобы ускорить применение фильтров или предложений `ORDER BY` к свойству в документе JSON, можно применить те же индексы, которые уже используются в других столбцах. При этом *напрямую* на свойства в документах JSON ссылаться нельзя.
    
1.  Сначала необходимо создать "виртуальный столбец", возвращающий значения, которые нужно использовать для фильтрации.
2.  а затем создать индекс в этом виртуальном столбце.  
  
В следующем примере создается вычисляемый столбец, который можно использовать для индексирования. Затем в новом вычисляемом столбце создается индекс. В этом примере создается столбец, содержащий имя клиента, которое хранится в документах JSON по пути `$.Customer.Name`. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Дополнительные сведения о вычисляемых столбцах 
Вычисляемый столбец не сохраняется Он вычисляется только в том случае, если индекс необходимо перестроить. и не занимает дополнительное место в таблице.   
  
Вычисляемый столбец необходимо создавать с тем же выражением, которое вы планируете использовать в запросах — в данном случае выражение `JSON_VALUE(Info, '$.Customer.Name')`.  
  
Запросы переписывать не нужно. Если выражения используются с функцией `JSON_VALUE`, как показано в предыдущем примере запроса, SQL Server определяет наличие эквивалентного вычисляемого столбца с тем же выражением и по возможности применяет индекс.

### <a name="execution-plan-for-this-example"></a>План выполнения для этого примера
Вот план выполнения запроса в этом примере:  
  
![План выполнения](../../relational-databases/json/media/jsonindexblog1.png "План выполнения")  
  
Вместо полного табличного сканирования SQL Server применяет оператор Index Seek к некластеризованному индексу и выявляет строки, отвечающие указанным условиям. Затем он выполняет поиск ключей по таблице `SalesOrderHeader`, чтобы получить другие указанные в запросе столбцы — в этом примере это столбцы `SalesOrderNumber` и `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Дополнительная оптимизация индекса с включенными столбцами
При добавлении требуемых столбцов в индекс такого дополнительного поиска по таблице можно избежать. Эти столбцы можно добавить как стандартные включенные столбцы, как показано в следующем примере, дополняющем предыдущий пример `CREATE INDEX`.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
В данном случае SQL Server не считывает дополнительные данные из таблицы `SalesOrderHeader`, так как все необходимое уже включено в некластеризованный индекс JSON. Этот тип индекса является хорошим способом объединения данных JSON и столбцов в запросах и создания оптимальных индексов для вашей рабочей нагрузки.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Индексы JSON — это индексы с учетом сортировки  
Важной особенностью индексов на основе JSON является то, что эти индексы учитывают параметры сортировки. Результатом выполнения функции `JSON_VALUE`, которая применяется при создании вычисляемого столбца, является текстовое значение, которое наследует параметры сортировки из входного выражения. Таким образом, значения в индексе упорядочиваются согласно правилам сортировки, определенным в исходных столбцах.  
  
Чтобы продемонстрировать, что индексы учитывают параметры сортировки, в следующем примере создается простая таблица коллекций с первичным ключом и данными в формате JSON.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
Указанная выше команда задает для столбца JSON сортировку по сербской кириллице. В следующем примере таблица заполняется и создается индекс по свойству name.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
Указанные выше команды создают стандартный индекс по значению `vName` вычисляемого столбца, которое соответствует свойству `$.name`. На странице кода сербской кириллицы буквы сортируются в следующем порядке: "А", "Б", "В", "Г", "Д", "Ђ", "Е" и т. д. Порядок элементов в индексе соответствует правилам сербской кириллицы, так как результат функции `JSON_VALUE` наследует параметры сортировки из исходного столбца. Следующий пример запрашивает эту коллекцию и сортирует результаты по имени.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Если посмотреть на фактический план выполнения, можно увидеть, что в нем используются отсортированные значения из некластеризованного индекса.  
  
 ![План выполнения](../../relational-databases/json/media/jsonindexblog2.png "План выполнения")  
  
 Несмотря на то что запрос содержит предложение `ORDER BY`, в плане выполнения не используется оператор Sort. Индекс JSON уже упорядочен по правилам сербской кириллицы. В связи с этим SQL Server может использовать некластеризованный индекс, в котором результаты уже отсортированы.  
  
 Но если порядок сортировки по выражению `ORDER BY` изменить, например добавить `COLLATE French_100_CI_AS_SC` после функции `JSON_VALUE`, план выполнения запроса станет совершенно иным.  
  
 ![План выполнения](../../relational-databases/json/media/jsonindexblog3.png "План выполнения")  
  
 Поскольку порядок значений в индексе не соответствует правилам сортировки для французского языка, SQL Server не может использовать этот индекс для упорядочивания результатов. В связи с этим он добавляет оператор Sort, который сортирует результаты по правилам сортировки для французского языка.  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Дополнительные сведения о JSON в SQL Server и базе данных SQL Azure  
  
### <a name="microsoft-videos"></a>Видео Майкрософт

Наглядные инструкции по встроенной поддержке JSON в SQL Server и базе данных SQL Azure см. в следующих видео.

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 и поддержка JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Использование JSON в SQL Server 2016 и базе данных SQL Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON как мост между NoSQL и реляционными решениями)
