---
title: Массивы значений параметров | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03479a0187c7720a595b550290a8f5ac8197fa9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288412"
---
# <a name="arrays-of-parameter-values"></a>Массивы значений параметров
Часто бывает полезно для приложений, для передачи массивов параметров. Например, использование массивов параметров и параметризованную **вставить** инструкцию, приложение можно вставить несколько строк за один раз. Существует несколько преимуществ использования массивов. Во-первых сетевой трафик сокращается, так как данные для многих инструкций отправляются в одном пакете (если источник данных имеет встроенную поддержку массивы параметров). Во-вторых некоторые источники данных можно выполнять инструкции SQL, использование массивов быстрее, чем выполнение одинаковое количество отдельных инструкций SQL. Наконец, когда данные хранятся в массиве, как это обычно бывает для данных экрана, приложение можно привязать все строки в определенном столбце на отдельный вызов **SQLBindParameter** и обновите их, выполнив одну инструкцию.  
  
 К сожалению не многие источники данных поддерживают массивы параметров. Тем не менее драйвер можно эмулировать массивы параметров, выполнение инструкции SQL один раз для каждого набора значений параметров. Это может привести к увеличение скорости, так как драйвер затем можно подготовить инструкцию, которую он планирует выполнить один раз для каждого набора параметров. Он также может привести к более простой код приложения.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Привязка массивов параметров](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Использование массивов параметров](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
