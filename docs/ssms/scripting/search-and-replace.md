---
title: Поиск и замена | Документация Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 869262f20b50e23a8e59f4a318fd70d73c339db9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821956"
---
# <a name="search-and-replace"></a>Поиск и замена
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Существует несколько способов поиска и замены текста. Пункт **Найти и заменить** из меню **Правка** содержит четыре команды: **Быстрый поиск**, **Быстрая замена**, **Найти в файлах** и **Заменить в файлах**. Каждая из этих команд открывает диалоговое окно **Найти и заменить** . Можно выполнить поиск и без диалогового окна с помощью сочетаний клавиш добавочного поиска. Эти методы позволяют управлять областью поиска и замены, а также выбирать способ просмотра совпадений при поиске и замене.  
  
 Выполняя поиск и замену текста, необходимо учитывать следующее.  
  
-   Параметры, установленные в диалоговом окне **Найти и заменить** , влияют на все поиски. В числе этих параметров такие, как **Учитывать регистр**, **Слово целиком**, **Искать вверх**, **Искать скрытый текст**, **Подстановочные знаки**, **Регулярные выражения**, **Искать во всех открытых документах**и **Искать в текущем проекте**. Не все эти параметры доступны во всех версиях диалогового окна **Найти и заменить** ;  
  
-   Кнопка**Отмена** доступна только для документов, оставшихся открытыми после операции замены.  
  
-   Команда**Отменить** для операции **Заменить все** , выполняемой над несколькими файлами, рассматривается как единичное массовое действие над всеми затронутыми файлами. При этом нельзя отменить изменения в одних файлах, сохранив их в других.  
  
 Обычно нельзя выполнять поиск в элементах с графическим отображением.  
  
## <a name="see-also"></a>См. также:  
 [Выполнение добавочного поиска в активном документе](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [осуществлять поиск в документах в интерактивном режиме](../../relational-databases/scripting/search-documents-interactively.md)   
 [Поиск документов с помощью списков результатов](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Поиск текста с символами-шаблонами](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Поиск текста с помощью регулярных выражений](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
