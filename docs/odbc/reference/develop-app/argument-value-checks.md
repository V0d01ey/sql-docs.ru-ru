---
title: Проверки значения аргумента | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dfee0dd00e30f6446430156617ba45a5a39b994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288551"
---
# <a name="argument-value-checks"></a>Проверки значения аргумента
Диспетчер драйверов проверяет следующие типы аргументов. Если не указано иное, диспетчер драйверов возвращает ошибку SQL_ERROR для ошибок в значения аргументов.  
  
-   Обычно дескрипторов среды, подключения и инструкция не может быть пустыми указателями. Диспетчер драйверов возвращает SQL_INVALID_HANDLE, обнаружив значение null, дескриптор.  
  
-   Обязательные аргументы указателя, такие как *OutputHandlePtr* в **SQLAllocHandle** и *CursorName* в **SQLSetCursorName**, не может быть указатели NULL.  
  
-   Флаги, которые не поддерживают специфические для драйвера значения должен быть допустимым значением. Например *операции* в **SQLSetPos** должно быть SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE или SQL_ADD.  
  
-   Флаги должны поддерживаться в используемая версия ODBC, поддерживаемых драйвером. Например *InfoType* в **SQLGetInfo** не может быть SQL_ASYNC_MODE (впервые представлено в ODBC 3.0) при вызове драйвером ODBC 2.0.  
  
-   Номера параметров и столбцов должны быть больше 0 или больше или равно 0, в зависимости от функции. Драйвер должен проверить верхний предел значения аргументов, исходя из текущего результирующего набора или инструкции SQL.  
  
-   Аргументы длины и индикатора и аргументы длины буфера данных должен содержать соответствующие значения. Например, аргумент, указывающий длину имени таблицы в **SQLColumns** (*NameLength3*) должен быть SQL_NTS или значение больше 0; *BufferLength* в **SQLDescribeCol** должно быть больше или равно 0. Драйвер также может понадобиться вернуть эти аргументы. Например, оно может проверить, *NameLength3* меньше или равны максимальной длины имени таблицы в источнике данных.
