---
title: NOT NULL в инструкциях CREATE TABLE | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4147e560d953b97ecba2e707d354bb6bf2ead59b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254227"
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL в инструкциях CREATE TABLE
Некоторые базы данных и особенно настольных баз данных, не поддерживают **NOT NULL** ограничение столбца в **CREATE TABLE** инструкций. Дополнительные сведения см. в описании параметра SQL_NON_NULLABLE_COLUMNS в [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) описание функции.
