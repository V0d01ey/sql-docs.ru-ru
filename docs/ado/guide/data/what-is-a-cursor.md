---
title: Что такое курсор? | Документы Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9ad683af9cea8ca4f5bc1736a48f0662656b6ef1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704514"
---
# <a name="what-is-a-cursor"></a>Что такое курсор?
Операции в реляционной базе данных выполняются над множеством строк. Набор строк, возвращаемый инструкцией SELECT, содержит все строки, которые удовлетворяют условиям, указанным в предложении WHERE инструкции. Такой полный набор строк, возвращаемых инструкцией, называется результирующим набором. Приложения, особенно тех, которые являются интерактивными и online, не всегда эффективно работают с результирующим набором как единое целое. Им нужен механизм, позволяющий обрабатывать одну строку или небольшое их число за один раз. Курсоры являются расширением результирующих наборов, которые предоставляют такой механизм.  
  
 Библиотека курсоров реализуют курсор. Библиотека курсоров — это программное обеспечение, часто реализуется как часть системы базы данных или API, для доступа к данным, который используется для управления атрибутами данные, возвращенные из источника данных (результирующий набор). Эти атрибуты включают управление параллелизмом, положение в результирующем наборе, число возвращаемых строк и можно ли переместить вперед или назад (или оба) результат задание (прокручиваемость).  
  
 Курсор отслеживает положение в результирующем наборе и позволяет выполнять несколько операций по строкам для результирующего набора, с или без возврата в исходную таблицу. Другими словами по существу курсоры возвращают результирующий набор, основанный на таблицах в базах данных. Курсор называется так, как он указывает текущее положение в результирующем наборе, так же, как курсор на экране компьютера указывает текущее положение.  
  
 Очень важно ознакомиться с концепцией курсоры перед переходом к Узнайте особенностей их использования в ADO.  
  
 Использование курсоров, вы можете:  
  
-   Укажите расположение на отдельные строки в результирующем наборе.  
  
-   Получить одну строку или блока строк, в зависимости от текущей позиции результирующего набора.  
  
-   Измените данные в строках в текущей позиции в результирующем наборе.  
  
-   Определения различных уровней чувствительности к изменения данных, сделанные другими пользователями.  
  
 Например рассмотрим приложение, отображающее список продуктов, доступных для потенциальных покупателей. Покупатель прокручивать список, чтобы просмотреть сведения о продукте и затрат и наконец выбирает продукт для приобретения. Дополнительные прокрутку и выбор происходит конца списка. Как беспокоится покупателя, продукты отображаются по одному, но приложение использует прокручиваемого курсора вверх и вниз Просмотр результирующего набора.  
  
 Можно использовать курсоры в различными способами:  
  
-   Вообще без строк.  
  
-   С некоторых или всех строк в одной таблице.  
  
-   Некоторые или все строки из логически соединенных таблиц.  
  
-   Как только для чтения или может обновляться на уровне курсора или поля.  
  
-   Только для прямого или полностью прокрутки.  
  
-   С помощью курсора keyset, расположенных на сервере.  
  
-   Чувствительность к базовой таблице изменения, вызванные другими приложениями (например, членство, сортировки, вставки, обновления и удаления).  
  
-   Существующие на сервере или клиенте.  
  
 Курсоры только для чтения, помогают пользователям просматривать результирующий набор, а также чтения и записи, что курсоры можно реализовать обновления отдельных строк. Сложные курсоры могут определяться с наборы ключей, указывающие на основе строк таблицы. Несмотря на то, что некоторые курсоры только для чтения в прямом направлении, другие пользователи могли переходить вперед и назад и предоставляют динамические обновления результирующего набора, с учетом изменений, которые больше всего другие приложения к базе данных.  
  
 Не все приложения должны использовать курсоры для доступа или обновления данных. Некоторые запросы просто не требуют обновления не удалось направить строку с помощью курсора. Курсоры должно быть одним из последнего приемов, вы решили получить данные- и затем следует выбрать наименьшее влияние курсор невозможно. При создании результирующего набора с помощью хранимой процедуры, результирующий набор не обновляется с помощью курсора изменять или обновлять методы.  
  
## <a name="concurrency"></a>Параллелизм  
 В некоторых многопользовательских приложений очень важно для отображаемые данные быть наиболее актуальная конечному пользователю. Классическим примером такой системы — это система бронирования авиабилетов, где множество пользователей могут конкурируют за же место, в заданной рейса (и, следовательно, одну запись). В данном случае архитектуры приложения должен обрабатывать параллельных операций на одну запись.  
  
 В других приложениях параллелизма это не так важно. В таких случаях не может быть оправдано расходов, участвующих в сохраняя при этом текущий данные в любое время.  
  
## <a name="position"></a>Положение  
 Курсор также сохраняет сведения о текущей позиции в результирующем наборе. Можно рассматривать позицию курсора, как указатель на текущую запись, аналогично тому, как массив точек индекса со значением в определенном месте в массиве.  
  
## <a name="scrollability"></a>Прокручиваемость  
 Тип курсора, чтобы позволить приложению также влияет на возможность перемещения вперед и назад по строкам в результирующем наборе; Иногда это называется прокручивание. Возможность перемещения вперед *и* назад по результирующего набора усложняет курсора и поэтому более высокая стоимость реализации. По этой причине следует запросить курсора с помощью этой функции только в случае необходимости.
