---
title: Проверка общих ошибок | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5645e00d9e3f93b2479c88ba37ec4ccf6fc5d295
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049770"
---
# <a name="general-error-checks"></a>Проверка общих ошибок
Диспетчер драйверов проверяет одна общая ошибка. Он всегда возвращает значение SQL_ERROR, при обнаружении следующей ошибки: Функция должна поддерживается драйвером.
