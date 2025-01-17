---
title: Функция SQLColumnPrivileges | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10d05310f7d9580b652f24bffa0896e32b23a40a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537711"
---
# <a name="sqlcolumnprivileges-function"></a>Функция SQLColumnPrivileges
**Соответствие стандартам**  
 Представленные версии: Соответствие стандартам 1.0 ODBC: интерфейс ODBC  
  
 **Сводка**  
 **SQLColumnPrivileges** возвращает список столбцов и связанные привилегии для указанной таблицы. Драйвер возвращает сведения, в виде результирующего набора на указанном *StatementHandle*.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Аргументы  
 *StatementHandle*  
 [Вход] Дескриптор инструкции.  
  
 *CatalogName*  
 [Вход] Имя каталога. Если драйвер поддерживает имена для некоторые каталоги, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») обозначает эти каталоги, которые не имеют имен. *CatalogName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *CatalogName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *CatalogName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения. Дополнительные сведения см. в разделе [аргументов в функции работы с каталогами](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Вход] Длина в символах **CatalogName*.  
  
 *SchemaName*  
 [Вход] Имя схемы. Если драйвер поддерживает схемы, для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») обозначает этих таблиц, у которых нет схемы. *SchemaName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *SchemaName* рассматривается как идентификатор. Если это значение SQL_FALSE, *SchemaName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength2*  
 [Вход] Длина в символах **SchemaName*.  
  
 *TableName*  
 [Вход] Имя таблицы. Этот аргумент не может быть пустым указателем. *TableName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *TableName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *TableName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength3*  
 [Вход] Длина в символах **TableName*.  
  
 *ColumnName*  
 [Вход] Строка шаблона поиска для имен столбцов.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *ColumnName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *ColumnName* — это аргумент значения шаблона; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength4*  
 [Вход] Длина в символах **ColumnName*.  
  
## <a name="returns"></a>Возвращает  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR, or SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLColumnPrivileges** возвращает значение SQL_ERROR или SQL_SUCCESS_WITH_INFO, а связанное значение SQLSTATE может быть получен путем вызова **SQLGetDiagRec** с *HandleType* значение SQL_HANDLE_STMT и *обрабатывать* из *StatementHandle*. В следующей таблице перечислены значения SQLSTATE, обычно возвращаемые **SQLColumnPrivileges** и объясняется каждый из них в контексте этой функции; описания SQLSTATE, возвращаемых драйвером предшествует обозначение «(DM)» Диспетчер. Возвращается связанный с каждого значения SQLSTATE значение SQL_ERROR, если не указано иное.  
  
|SQLSTATE|Ошибка|Описание|  
|--------------|-----------|-----------------|  
|01000|Общее предупреждение|Специфические для драйвера информационное сообщение. (Функция возвращает значение SQL_SUCCESS_WITH_INFO).|  
|08S01|Отказ канала связи|Сбой в канале связи между драйвером и источника данных, к которому был подключен драйвер перед обработкой функции было завершено.|  
|24000|Недопустимое состояние курсора|Курсор был открыт на *StatementHandle,* и **SQLFetch** или **SQLFetchScroll** бы вызывалась. Если эта ошибка возвращается диспетчером драйверов **SQLFetch** или **SQLFetchScroll** не вернула значение SQL_NO_DATA и возвращается с помощью драйвера, если **SQLFetch** или **SQLFetchScroll** вернула значение SQL_NO_DATA.<br /><br /> Курсор был открыт на *StatementHandle*, но **SQLFetch** или **SQLFetchScroll** не был вызван.|  
|40001|Сбой сериализации|Выполнен откат транзакции из-за взаимоблокировки ресурсов с другой транзакцией.|  
|40003|Состояние транзакции неизвестно|Не удалось выполнить связанное соединение во время выполнения этой функции и не удается определить состояние транзакции.|  
|HY000|Общая ошибка|Произошла ошибка, для которой было нет конкретных SQLSTATE и SQLSTATE не зависящие от реализации, который был определен. Сообщение об ошибке, возвращенные **SQLGetDiagRec** в  *\*MessageText* буфера описывает ошибку и его причины.|  
|HY001|Ошибка выделения памяти|Драйвер не удалось выделить память, необходимую для поддержки выполнения или завершения функции.|  
|HY008|Операция отменена|Асинхронная обработка была включена для *StatementHandle*. Функция была вызвана, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для *StatementHandle*. Затем функция был снова вызван для *StatementHandle*.<br /><br /> Функция была вызвана, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для *StatementHandle* из другого потока в многопоточные приложения.|  
|HY009|Недопустимое использование пустого указателя|*TableName* аргумент был пустым указателем.<br /><br /> Атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE, *CatalogName* аргумент был пустым указателем, а также SQL_CATALOG_NAME *InfoType* возвращает этот каталога имена поддерживаются.<br /><br /> (DM) атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE и *SchemaName* или *ColumnName* аргумент был пустым указателем.|  
|HY010|Ошибка последовательности функций|(DM) был вызван асинхронно выполняемой функции для дескриптора соединения, связанный с *StatementHandle*. При вызове этой функции по-прежнему выполнении асинхронной функции.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults** был вызван для *StatementHandle* и возвращается SQL_PARAM_DATA_ ДОСТУПНО. Прежде чем данные были получены для всех параметров потоковой вызове этой функции.<br /><br /> (DM) асинхронно выполняемой функции (не такой) был вызван для *StatementHandle* и еще выполнялась при вызове этой функции.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, или **SQLSetPos** был вызван для  *StatementHandle* и возвращается значение SQL_NEED_DATA. Эта функция был вызван перед отправкой данных для всех параметров данных времени выполнения или столбцов.|  
|HY013|Ошибка управления памятью|Не удалось обработать вызов функции, так как базовые объекты памяти оказываются недоступны, возможно из-за нехватки памяти.|  
|HY090|Недопустимая длина строки или буфера|(DM) значение одного из аргументов длина имени меньше 0, но не равно SQL_NTS.|  
|||Значение одного из аргументов длина имени превышает значение максимальной длины для соответствующего имени. (См. в разделе «Комментарии».)|  
|HY117|Подключение будет приостановлена из-за состояние транзакции неизвестно. Только отключиться и разрешены функции, доступные только для чтения.|(DM) Дополнительные сведения о состоянии приостановки, см. в разделе [функция SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Дополнительная возможность не реализована|Было указано имя каталога, а драйверу или источнику данных не поддерживает каталоги.<br /><br /> Было указано имя схемы, а драйверу или источнику данных не поддерживает схемы.<br /><br /> Для имени столбца указан шаблон поиска строки, а источник данных не поддерживает шаблоны поиска для этого аргумента.<br /><br /> Сочетание текущие параметры SQL_CONCURRENCY и SQL_CURSOR_TYPE атрибутов инструкции не поддерживается драйвером или источником данных.<br /><br /> Атрибут инструкции SQL_ATTR_USE_BOOKMARKS было присвоено SQL_UB_VARIABLE и атрибут инструкции SQL_ATTR_CURSOR_TYPE было присвоено тип курсора, для которого драйвер не поддерживает закладки.|  
|HYT00|Время ожидания истекло|Время ожидания запроса истекло раньше, чем источник данных вернул результирующий набор. Период ожидания задается с помощью **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Время ожидания подключения истекло|Время ожидания подключения истекло раньше, чем ответил на запрос источника данных. Период времени ожидания задается с помощью **SQLSetConnectAttr**, sql_attr_connection_timeout не учитывается.|  
|IM001|Драйвер не поддерживает эту функцию|Драйвер (DM), связанные с *StatementHandle* не поддерживает функцию.|  
|IM017|Опрос недоступен в режиме асинхронное уведомление|Каждый раз, когда используется модель уведомлений, отключен опроса.|  
|IM018|**SQLCompleteAsync** не был вызван для завершения предыдущей асинхронной операции на этот дескриптор.|Если предыдущий вызов функции в дескриптор возвращает SQL_STILL_EXECUTING, и если включен режим уведомлений, **SQLCompleteAsync** должен вызываться с дескриптором постобработки и завершить операцию.|  
  
## <a name="comments"></a>Комментарии  
 **SQLColumnPrivileges** возвращает результаты в виде стандартных результирующий набор, упорядоченный по TABLE_CAT, по значениям TABLE_SCHEM, TABLE_NAME, COLUMN_NAME и ПРИВИЛЕГИЙ.  
  
> [!NOTE]  
>  **SQLColumnPrivileges** могут не возвращать привилегии для всех столбцов. Например драйвер могут не возвращать информацию о правах для псевдо столбцов, таких как Oracle ROWID. Приложения могут использовать любой допустимый столбец, независимо от того, он возвращается в виде **SQLColumnPrivileges**.  
  
 Длин столбцы типа VARCHAR не отображаются в таблице. фактические значения длины зависит от источника данных. Чтобы определить фактический длин столбцов CATALOG_NAME, SCHEMA_NAME, TABLE_NAME и COLUMN_NAME, приложение может вызвать **SQLGetInfo** с SQL_MAX_TABLE_NAME_ SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, LEN и SQL_MAX_COLUMN_NAME_LEN параметры.  
  
> [!NOTE]  
>  Дополнительные сведения о общего использования, аргументы и возвращаемые данные функций каталога ODBC, см. в разделе [функций каталога](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Следующие столбцы были переименованы для ODBC 3. *x*. Изменения имен столбцов не влияют на обратную совместимость так, как выполнить привязку приложения, номер столбца.  
  
|Столбец ODBC 2.0|ODBC 3. *x* столбца|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 В следующей таблице перечислены столбцы в результирующем наборе. Дополнительные столбцы вслед за столбец 8 (IS_GRANTABLE) можно определить с помощью драйвера. Приложения должны получить доступ к от драйвера, отсчет от конца результирующего набора, вместо указания явной порядковый номер. Дополнительные сведения см. в разделе [данные, возвращаемые функциями каталога](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Имя столбца|Номер столбца|Тип данных|Комментарии|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Идентификатор каталога; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает каталоги для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет каталогов.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Идентификатор схемы; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает схемы для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет схемы.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|Идентификатор таблицы.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar not NULL|Имя столбца. Драйвер возвращает пустую строку для столбца, который не имеет имени.|  
|ОБЪЕКТ, ПРЕДОСТАВЛЯЮЩИЙ РАЗРЕШЕНИЕ (ODBC 1.0)|5|Varchar|Имя пользователя, который предоставил права; Значение NULL, если не применим к источнику данных.<br /><br /> Для всех строк, в которых значение в столбце участника, КОТОРОМУ владелец объекта столбец GRANTOR будет «_SYSTEM».|  
|УЧАСТНИК (ODBC 1.0)|6|Varchar not NULL|Имя пользователя, которому предоставлено право доступа.|  
|ПРАВ ДОСТУПА (ODBC 1.0)|7|Varchar not NULL|Идентифицирует столбец привилегий. Может принимать одно из следующих (или других поддерживаемых данными источника при реализации):<br /><br /> ВЫБЕРИТЕ: Пользователь GRANTEE для получения данных для столбца.<br /><br /> ВСТАВЬТЕ: Получатель прав может предоставлять данные для столбца во всех строках, которые вставляются в связанной таблице.<br /><br /> ОБНОВЛЕНИЕ: Получатель прав может обновлять данные в столбце.<br /><br /> ССЫЛКИ: Пользователь GRANTEE для ссылки на столбец в ограничение (например, уникальный, данных, или проверочное ограничение таблицы).|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|Указывает, разрешено ли участнику предоставлять права другим пользователям; «YES», «Нет» или «NULL», если неизвестно или неприменимо к источнику данных.<br /><br /> Привилегия является либо предоставляемых, либо не предоставляемых, но не оба. Результирующий набор, возвращаемый **SQLColumnPrivileges** никогда не будет содержать две строки, для которых все столбцы, кроме столбца IS_GRANTABLE содержат одинаковое значение.|  
  
## <a name="code-example"></a>Пример кода  
 Пример кода ту же функцию, см. в разделе [функция SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Привязка к столбцу в результирующем наборе буфер|[Функция SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Отмена обработка инструкций|[Функция SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Возврат столбцов в таблице или таблицах|[Функция SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Блока данных или прокрутке результирующего набора|[Функция SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Получение нескольких строк данных|[Функция SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Возвращает привилегии для таблицы или таблиц|[Функция SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|Возвращает список таблиц в источнике данных|[Функция SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>См. также  
 [Справочник по API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Файлы заголовков ODBC](../../../odbc/reference/install/odbc-header-files.md)
