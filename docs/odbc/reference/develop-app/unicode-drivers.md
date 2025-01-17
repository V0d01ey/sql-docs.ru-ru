---
title: Драйверы Юникода | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473037"
---
# <a name="unicode-drivers"></a>Драйверы Юникода
Следует ли драйвер драйвер Юникода или ANSI полностью зависит от характера источника данных. Если источник данных поддерживает данные в Юникоде, драйвер должен быть драйвер Юникода. Если источник данных поддерживает только данных ANSI, драйвер должен оставаться драйвером ANSI.  
  
 Драйвер Юникода необходимо экспортировать **SQLConnectW** распознается как драйвер Юникода диспетчером драйверов.  
  
 Драйвер Юникода необходимо принять функции Юникода (с суффиксом *W*) и хранения данных в Юникоде. Он также может принимать функции ANSI, но не требуется. (Диспетчер драйверов не передает вызов функции ANSI с *A* суффикс драйвер, но преобразует его в ANSI вызов_функции без суффикса и затем передает его к драйверу.)  
  
 Драйвер Юникода должен иметь возможность возвращать результирующие наборы в Юникоде или ANSI, в зависимости от привязки приложения. Если приложение имеет привязку к SQL_C_CHAR, драйвер Юникода необходимо преобразовать SQL_WCHAR SQL_CHAR. Сопоставляется SQL_C_WCHAR SQL_C_CHAR ANSI драйверов диспетчера драйверов в отличие без сопоставления для Юникода драйверов.  
  
> [!NOTE]  
>  При определении типа драйверов, диспетчер драйверов вызывает **SQLSetConnectAttr** и присвойте атрибуту SQL_ATTR_ANSI_APP во время установления соединения. Если приложение использует интерфейсы API ANSI, SQL_ATTR_ANSI_APP будет присвоено SQL_AA_TRUE и при использовании Юникода, он будет присвоено значение SQL_AA_FALSE. Этот атрибут используется, чтобы драйвер можно работать иначе, в зависимости от типа приложения. Атрибут нельзя задать для приложения напрямую, а не поддерживается **SQLGetConnectAttr**. Если драйвер выполняет то же поведение для приложений, ANSI и Юникод, он должен вернуть значение SQL_ERROR для этого атрибута. Если драйвер возвращает значение SQL_SUCCESS, диспетчер драйверов будет разделить соединения ANSI и Юникод, при использовании пула соединений.
