---
title: MSSQLSERVER_17130 | Документация Майкрософт
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d0c956c9144658c318a324ab540815291f9d9ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860686"
---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|17130|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|INIT_NOLOCKSPACE|  
|Текст сообщения|Недостаточно памяти для заданного количества блокировок. Выполняется попытка запуска с хэш-таблицей блокировок меньшего размера, что может негативно отразиться на производительности. Обратитесь к администратору базы данных с просьбой о выделении большего объема памяти для данного экземпляра компонента Database Engine.|  
  
## <a name="explanation"></a>Объяснение  
Недостаточно памяти для хэш-таблицы диспетчера блокировок нужного размера.  Будет произведена попытка запуска с уменьшенным размером хэш-таблицы блокировок.  
  
## <a name="user-action"></a>Действие пользователя  
Проверьте параметры конфигурации памяти сервера (min/max server memory) и нагрузку на память. Предоставьте больше памяти для работы SQL Server.  
  
