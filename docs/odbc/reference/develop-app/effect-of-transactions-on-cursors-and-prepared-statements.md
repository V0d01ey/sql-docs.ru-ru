---
title: Влияние транзакций на курсоры и подготовленные инструкции | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c2c6b06744965144ca9d5feb27e9ea16d9903c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305714"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Влияние транзакций на курсоры и подготовленные инструкции
Фиксация или откат транзакции имеет следующее влияние на курсоры и планы доступа:  
  
-   Закрываются все курсоры, и доступ планы для подготовленных инструкций для этого соединения будут удалены.  
  
-   Закрываются все курсоры, и сохранение планов доступа для подготовленных инструкций для этого соединения.  
  
-   Все курсоры остаются открытыми, и сохранение планов доступа для подготовленных инструкций для этого соединения.  
  
 Например предположим, что источник данных поведение первой в этом списке, наиболее строгие из этих процессов. Теперь предположим, что приложение делает следующее:  
  
1.  Задает режим фиксации для ручной фиксации.  
  
2.  Создает результирующий набор заказов на продажу в операторе 1.  
  
3.  Создает результирующий набор строк в заказе на продажу в инструкции 2, когда пользователь выделяет в указанном порядке.  
  
4.  Вызовы **SQLExecute** для выполнения инструкции позиционированного обновления, который был подготовлен на инструкцию 3, когда пользователь обновляет строку.  
  
5.  Вызовы **SQLEndTran** зафиксировать инструкции позиционированного обновления.  
  
 Из-за поведения источника данных, вызов **SQLEndTran** на шаге 5 приводит к его закрытия курсора инструкции 1 и 2 и удалить план доступа во всех инструкциях. Приложение должно был повторно исполнить наборы инструкций, 1 и 2 для повторного создания результата и reprepare оператором в инструкцию 3.  
  
 В режиме автоматической фиксации, функций, кроме **SQLEndTran** фиксации транзакции:  
  
-   **SQLExecute** или **SQLExecDirect** в предыдущем примере вызов **SQLExecute** на шаге 4 фиксирует транзакцию. Это приводит к источнику данных для закрытия курсора после инструкции 1 и 2 и удалить план доступ для всех инструкций для этого соединения.  
  
-   **SQLBulkOperations** или **SQLSetPos** в предыдущем примере, предположим, что на шаге 4 приложение вызывает **SQLSetPos** с параметром sql_update на инструкции 2, вместо выполнения инструкции позиционированного обновления в инструкции 3. Это фиксирует транзакцию и приводит к источнику данных для закрытия курсора после инструкции 1 и 2 и отбрасывает все планы доступа для этого соединения.  
  
-   **SQLCloseCursor** в предыдущем примере, предположим, что когда пользователь выделяет другом заказе на продажу, приложение вызывает **SQLCloseCursor** на инструкцию 2 перед созданием результат строк для новых продаж порядок. Вызов **SQLCloseCursor** фиксирует **ВЫБЕРИТЕ** оператор, который создал результирующий набор строк и приводит к источнику данных для закрытия курсора в инструкции 1, а затем удаляет все планы доступа, на который подключение.  
  
 Приложений, особенно на экране в которых пользователь прокручивает вокруг результирующего набора и обновлений или удаляются строки, необходимо соблюдать осторожность в код решения этой проблемы.  
  
 Чтобы определить, как ведет себя источника данных при фиксации или отката транзакции, приложение вызывает **SQLGetInfo** параметры SQL_CURSOR_COMMIT_BEHAVIOR и SQL_CURSOR_ROLLBACK_BEHAVIOR.
