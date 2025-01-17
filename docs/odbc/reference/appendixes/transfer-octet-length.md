---
title: Длительность октета передачи | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8f64172685c42a5dde8de9027c8c7e621ddd9f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735070"
---
# <a name="transfer-octet-length"></a>Длительность октета передачи
Длительность октета передачи столбца — это максимальное число байтов, возвращаемых в приложение при передаче данных в тип данных C по умолчанию. Для символьных данных длительность октета передачи не включает свободное место для символа завершения null. Длительность октета передачи столбца может отличаться от количество байтов, необходимое для хранения данных в источнике данных.  
  
 В следующей таблице показана длительность октета передачи, определенных для каждого типа данных ODBC SQL.  
  
|Идентификатор типа SQL|Длина|  
|-------------------------|------------|  
|Все символьные типы [a]|Определенный или (для типа переменной) максимальную длину столбца в байтах. Это совпадает со значением поля дескриптора SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|Число байтов, необходимое для хранения символов представлением этих данных, если набор символов ANSI и дважды это число, если набор символов ЮНИКОДА. Это максимальное количество цифр, плюс два, так как данные возвращаются как строку символов и символов требуется для цифры, знак и десятичной запятой. Например передача длину столбец, определенный как NUMERIC(10,3) равна 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|Число байтов, необходимое для хранения символов представлением этих данных, если набор символов ANSI и дважды это число, если набор символов ЮНИКОДА, так как этот тип данных возвращается в виде символьной строки по умолчанию. Представление символа состоит из 20 символов. 19 цифр и знак, если автоматический или 20 знаков, без знака. Таким образом длина равна 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Все типы binary [a]|Число байтов, необходимое для хранения определенных (для основных типов) или (для типов переменных) количество символов.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (размер структуры SQL_DATE_STRUCT или SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (размер структуры SQL_TIMESTAMP_STRUCT).|  
|Все типы данных интервала|34 (размер структуры интервал).|  
|SQL_GUID|16 (размер структуры GUID).|  
  
 [a] Если драйвер не может определить значения столбца или параметра длины для типов переменных, он возвращает SQL_NO_TOTAL.
