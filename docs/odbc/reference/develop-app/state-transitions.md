---
title: Состояний | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c1db4f850e6f181757d974ae74bb475b0cc5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148993"
---
# <a name="state-transitions"></a>Переходы состояния
ODBC определяет дискретных *состояний* для каждой среды, для каждого подключения и каждой инструкции. Например в среде имеет три возможных состояния: Свободен (в который выделяется среда не), выделенное место (в которой выделяется среде, но соединения не выделяются) и соединения (в котором среды и одно или несколько соединений выделяются). Соединение имеет семь состояний; инструкции имеют 13 возможных состояний.  
  
 Определенный элемент, который идентифицируется по дескриптору, перемещает из одного состояния в другое когда приложение вызывает определенные функции или функции и передает дескриптор этого элемента. Такое перемещение называется *перехода состояния*. Например, выделение дескриптора среды с **SQLAllocHandle** перемещает среду из нераспределенный выделенное и освобождение этого дескриптора с **SQLFreeHandle** возвращается из выделенных для Освобождено. ODBC определяет ограниченное число юридические переходов между состояниями, являющееся другим способом, говорит о том, что функции должен вызываться в определенном порядке.  
  
 Некоторые функции, такие как **SQLGetConnectAttr**, вообще не влияет на состояние. Другие функции, влияющие на состояние одного элемента. Например **SQLDisconnect** перемещение подключения из состояния подключения в выделенное состояние. Наконец некоторые функции, влияющие на состояние более одного элемента. Например, выделение дескриптора соединения с **SQLAllocHandle** перемещает подключения из нераспределенный в выделенное состояние и среды из выделенных в состояние подключения.  
  
 Если приложение вызывает функцию не по порядку, функция возвращает *состояния перехода ошибка*. Например, если среда — подключения, а приложение вызовы **SQLFreeHandle** с этот дескриптор среды **SQLFreeHandle** возвращает параметром SQLSTATE HY010 (функционировать ошибка последовательности), так как он может вызываться только в том случае, если среда находится в состоянии выделенное место. Определив это как недопустимую смену состояния, ODBC дает приложению освободить среды, пока имеются активные соединения.  
  
 Некоторые переходов между состояниями присущие архитектуре ODBC. Например это не нельзя выделить дескриптор соединения без первого выделение дескриптора среды, так как функция, которая выделяет дескриптор соединения требуется дескриптор среды. Другие переходов между состояниями, устанавливаемым диспетчера драйверов и драйверов. Например **SQLExecute** выполняет подготовленную инструкцию. Если передается дескриптор инструкции не в состоянии подготовки, **SQLExecute** возвращает параметром SQLSTATE HY010 (функционировать ошибка последовательности).  
  
 С точки зрения приложения переходы состояния обычно просты: Допустимые переходы между состояниями стремятся Рука в руку с потоком хорошо написанное приложение. Переходы состояния более сложны для диспетчера драйверов и драйверов, так как они должна отслеживать состояние среды, для каждого подключения и каждой инструкции. Большая часть этой работы выполняется диспетчером драйверов; Большая часть работы, которая должна быть выполнена драйверами происходит с операторами с ожидающие результаты.  
  
 1 и 2 части данного руководства («Введение в ODBC» и «Разработка приложений и драйверов») как правило, не говоря уже о явно переходов между состояниями. Вместо этого они описывают порядок вызова функции. Например, «Выполнение инструкции» сообщающее, что необходимо подготовить инструкцию с **SQLPrepare** перед его выполнением с **SQLExecute**. Полное описание состояний и переходов состояний, включая переходы проверяются диспетчером драйверов и который должен быть проверен, драйверы, см. в разделе [приложении б: Таблицы перехода состояния ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
