---
title: Ограничения инструкции UPDATE | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6b854cc417898c5576c60ca129c597eae280df4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633136"
---
# <a name="update-statement-limitations"></a>Ограничения инструкции UPDATE
Для обновления таблицы драйвера для Paradox таблица должна иметь уникальный индекс (первичный ключ для Paradox). При использовании драйвер для Paradox без реализации СУБД Borland, не может изменять таблицу Paradox.  
  
 Не поддерживается драйвером текста.  
  
 При использовании драйвера Microsoft Excel можно обновлять значения, но нельзя удалить строку из таблицы, основанной на электронную таблицу Microsoft Excel. Таким образом инструкция UPDATE не является официально поддерживается драйвером Microsoft Excel. Только инструкция INSERT считается поддерживается.
