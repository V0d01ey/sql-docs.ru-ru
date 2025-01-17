---
title: Подготовка и выполнение команд | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bf2120468a00de2150f6105f4d79ec5a2ed4278
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700454"
---
# <a name="preparing-and-executing-commands"></a>Подготовка и выполнение команд
Команды, инструкции для поставщика на выполнение некоторых операций с базового источника данных. Инструкция SQL, например, — это команда для поставщика данных Microsoft SQL. В ADO команды обычно представляется **команда** объектов, несмотря на то, что простые команды также могут выдаваться через **подключения** или **записей** объектов.  
  
 Можно использовать **команда** объекта, чтобы запросить любой поддерживаемый тип операции от поставщика, при условии, что поставщик может интерпретировать строку, команда должным образом. Это распространенная операция, для поставщиков данных можно выполнить запрос к базе данных и вернуть записей в **записей** объект, который, может рассматриваться как контейнер для хранения результата и средство для просмотра результатов. Как и в случае с множеством объектов ADO, некоторые **команда** коллекций объектов, методов или свойств, которые могут вызывать ошибки при обращении к зависимости от того, функциональные возможности поставщика.  
  
 Помимо использования **команда** объектов, которые можно использовать **Execute** метод **подключения** объекта или **откройте** метод  **Набор записей** объект команды, который будет выполнен. Тем не менее, следует использовать **команда** объекта, если вам нужно повторно использовать команды в коде, или если необходимо передать параметр подробные сведения с помощью вашей команды. Эти сценарии рассматриваются более подробно далее в этом разделе.  
  
> [!NOTE]
>  Определенные **команда**s может возвращать результирующий набор в виде двоичного потока или одного **записи** , а не как **записей**, если это поддерживается поставщиком. Кроме того, некоторые **команда**s не предназначены для возврата любой результирующий набор, вообще (например, запрос SQL Update). В этом разделе рассматриваются наиболее типичный сценарий, однако: выполнение **команда**, которые возвращают результаты в виде **записей** объекта. Дополнительные сведения о возврате результатов в **записи**s или **Stream**s, см. в разделе [записи и потоки](../../../ado/guide/data/records-and-streams.md).  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Обзор объекта Command](../../../ado/guide/data/command-object-overview.md)  
  
-   [Создание и выполнение простой команды](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Параметры объекта Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Вызов хранимой процедуры с использованием команды](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Вызов хранимой процедуры в качестве метода объекта Connection](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Именованные команды](../../../ado/guide/data/named-commands.md)  
  
-   [Передача параметров именованной команде](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
