---
title: Сопоставление SQLAllocConnect | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bdb63e9610d00c0736f640b6f4c4d743f3335c7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280978"
---
# <a name="sqlallocconnect-mapping"></a>Сопоставление SQLAllocConnect
Если приложение вызывает **SQLAllocConnect** через ODBC 3. *x* драйвера, вызов **SQLAllocConnect**(*henv*, *phdbc*) сопоставляется с **SQLAllocHandle** следующим образом:  
  
1.  Диспетчер драйверов выделяет соединение и возвращает его приложению.  
  
2.  Когда приложение устанавливает соединение, диспетчер драйверов вызывает  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     в драйвере с *InputHandle* присвоено *henv*, и *OutputHandlePtr* присвоено *phdbc*.
