---
title: Известные проблемы в данной версии драйвера для SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 86b87d03a5b0a66ba1e77260a0ec0b43125fa98b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798763"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Известные проблемы в данной версии драйвера

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Эта статья содержит список известных проблем в Microsoft ODBC Driver 13, 13.1 и 17 for SQL Server на платформах Linux и macOS.

Дополнительные проблемы будут публиковаться в [блоге группы разработчиков драйвера Microsoft ODBC](https://blogs.msdn.com/b/sqlnativeclient/).  

- В Windows, Linux и macOS символы из кодировки области личных символов (PUA) или символов, определяемых конечными пользователями (EUDC), могут преобразовываться по-разному. Преобразования, выполняемые на сервере в пределах [!INCLUDE[tsql](../../../includes/tsql-md.md)], используют библиотеку функций преобразования Windows. Преобразования в драйвере используют библиотеки функций преобразования Windows, Linux или macOS. Каждая из библиотек может давать разные результаты при выполнении преобразований. Дополнительные сведения см. в статье [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Символы, определяемые конечными пользователями, и символы области личных символов).

- Если кодировка клиента — UTF-8, диспетчер драйверов не всегда выполняет преобразование из UTF-8 в UTF-16 правильно. В настоящее время повреждение данных происходит, когда один или несколько символов в строке не являются допустимыми символами UTF-8. Символы ASCII сопоставляются правильно. Диспетчер драйверов пытается выполнить такое преобразование при вызове SQLCHAR-версий интерфейса API ODBC (например, SQLDriverConnectA). Диспетчер драйверов не пытается выполнить такое преобразование при вызове SQLWCHAR-версий ODBC API (например, SQLDriverConnectW).  

- Параметр *ColumnSize* функции **SQLBindParameter** указывает на число символов в типе SQL, а *BufferLength* — это число байтов в буфере приложения. Тем не менее, если используется тип данных SQL `varchar(n)` или `char(n)`, приложение связывает параметр как SQL_C_CHAR или SQL_C_VARCHAR, а клиент использует кодовую страницу UTF-8, может появиться ошибка "Усечение данных строки справа" от драйвера, даже когда значение *ColumnSize* согласовано с размером типа данных на сервере. Эта ошибка возникает по той причине, что в результате преобразования между кодировками символов длина данных может измениться. Например, символ правого апострофа (U+2019) кодируется в CP-1252 как один байт 0x92, а в UTF-8 — как последовательность из трех байтов 0xe2 0x80 0x99.

Например, если используется кодировка UTF-8 и вы указали значение 1 для параметра *BufferLength* и *ColumnSize* в качестве выходного параметра функции **SQLBindParameter**, а затем пытаетесь получить предыдущий символ, хранящийся в столбце `char(1)` на сервере (в кодировке CP-1252), драйвер пытается преобразовать его в трехбайтовую кодировку UTF-8, однако результат не помещается в однобайтовый буфер. Значение *ColumnSize* сравнивается с *BufferLength* в **SQLBindParameter** перед выполнением преобразования между разными кодовыми страницами в клиенте и на сервере. Поскольку *ColumnSize* для 1 меньше, чем *BufferLength* , например, для 3, драйвер выдает ошибку. Чтобы избежать этой ошибки, убедитесь в том, что после преобразования данные поместятся в указанный буфер или столбец. Обратите внимание на то, что для типа `varchar(n)` значение *ColumnSize* не может превышать 8000.

## <a name="see-also"></a>См. также:  
[Указания по программированию](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Заметки о выпуске](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

