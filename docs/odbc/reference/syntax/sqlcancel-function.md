---
title: Функция SQLCancel | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ad701efe914780a74bba3b8f0530b4881d7709
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537630"
---
# <a name="sqlcancel-function"></a>Функция SQLCancel
**Соответствие стандартам**  
 Представленные версии: Соответствие стандартам 1.0 ODBC: ISO-92  
  
 **Сводка**  
 **SQLCancel** отменяет обработку на инструкции.  
  
 Чтобы отменить обработку на соединение или оператор, используйте [функция SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Аргументы  
 *StatementHandle*  
 [Вход] Дескриптор инструкции.  
  
## <a name="returns"></a>Возвращает  
 Значение SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, значение SQL_ERROR или SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLCancel** возвращает значение SQL_ERROR или SQL_SUCCESS_WITH_INFO, а связанное значение SQLSTATE можно получить, вызвав **SQLGetDiagRec** с *HandleType* из SQL_ HANDLE_STMT и *обрабатывать* из *StatementHandle*. В следующей таблице перечислены значения SQLSTATE, обычно возвращаемые **SQLCancel** и объясняется каждый из них в контексте этой функции; описания SQLSTATE, возвращаемых диспетчером драйверов предшествует обозначение «(DM)». Возвращается связанный с каждого значения SQLSTATE значение SQL_ERROR, если не указано иное.  
  
|SQLSTATE|Ошибка|Описание|  
|--------------|-----------|-----------------|  
|01000|Общее предупреждение|Специфические для драйвера информационное сообщение. (Функция возвращает значение SQL_SUCCESS_WITH_INFO).|  
|HY000|Общая ошибка|Произошла ошибка, для которой было нет конкретных SQLSTATE и SQLSTATE не зависящие от реализации, который был определен. Сообщение об ошибке, возвращенные [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) в аргументе  *\*MessageText* буфера описывает ошибку и его причины.|  
|HY001|Ошибка выделения памяти|Драйвер не удалось выделить память, необходимую для поддержки выполнения или завершения функции.|  
|HY010|Ошибка последовательности функций|(DM) был вызван асинхронно выполняемой функции для дескриптора соединения, связанный с *StatementHandle*. Если по-прежнему выполнении асинхронной функции **SQLCancel** была вызвана функция.<br /><br /> (DM) отменить операцию, не удалось, так как асинхронная операция выполняется в дескрипторе соединения, связанный с *StatementHandle*.|  
|HY013|Ошибка управления памятью|Не удалось обработать вызов функции, так как базовые объекты памяти оказываются недоступны, возможно из-за нехватки памяти.|  
|HY018|Сервер отклонил запрос на отмену|Сервер отклонил запрос на отмену.|  
|HY117|Подключение будет приостановлена из-за состояние транзакции неизвестно. Только отключиться и разрешены функции, доступные только для чтения.|(DM) Дополнительные сведения о состоянии приостановки, см. в разделе [функция SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Время ожидания подключения истекло|Время ожидания подключения истекло раньше, чем ответил на запрос источника данных. Период времени ожидания задается с помощью **SQLSetConnectAttr**, sql_attr_connection_timeout не учитывается.|  
|IM001|Драйвер не поддерживает эту функцию|Драйвер (DM), связанные с *StatementHandle* не поддерживает функцию.|  
  
## <a name="comments"></a>Комментарии  
 **SQLCancel** можно отменить следующие виды обработки при получении инструкции:  
  
-   Функция, работающего асинхронно на инструкцию.  
  
-   Функция для инструкции нужны данные.  
  
-   Функции, выполняемой в инструкцию в другом потоке.  
  
 В ODBC 2. *x*, если приложение вызывает **SQLCancel** когда обработка не выполняется в операторе, **SQLCancel** имеет тот же эффект, что **SQLFreeStmt** с параметром SQL_CLOSE; Это поведение определяется только для полноты информации, и приложение должно вызывать **SQLFreeStmt** или **SQLCloseCursor** закрытия курсора.  
  
 Когда **SQLCancel** вызывается для отмены функции, выполняемой асинхронно в инструкции или функции в инструкции, очистку данных потребностей, отправляются, используйте функцию отмены диагностические записи и **SQLCancel**  отправляет свой собственный диагностические записи; когда **SQLCancel** вызывается для отмены функции, работающей на инструкцию в другом потоке, однако она не очищает диагностические записи возвращаемого отменено функции и не не опубликовать свой собственный диагностических записей.  
  
## <a name="canceling-asynchronous-processing"></a>Отмена асинхронной обработки  
 После приложение вызывает функцию асинхронно, он вызывает функцию многократно, чтобы определить, является ли обработка завершена. Если функция по-прежнему обрабатывается, возвращается значение SQL_STILL_EXECUTING. Если функция завершения обработки, он возвращает другого кода.  
  
 После любого вызова функции, которая возвращает значение SQL_STILL_EXECUTING, приложение может вызвать **SQLCancel** для отмены функции. При успешном выполнении запроса отмены, драйвер возвращает SQL_SUCCESS. Это сообщение указывает, что функция фактически было отменено; он показывает, что запрос на отмену был обработан. Когда или если функция отменяется фактически является зависящих от драйвера и зависит от источника данных. Приложение должно продолжить вызывать у исходной функции, пока код возврата не SQL_STILL_EXECUTING. Если функция успешно отменено, возвращается значение SQL_ERROR и SQLSTATE HY008 (операция отменена). Если функция завершения обработки, возвращается значение SQL_SUCCESS или SQL_SUCCESS_WITH_INFO, если функция выполнена успешно или SQL_ERROR и SQLSTATE, отличный от HY008 (операция отменена) Если не удалось выполнить функцию.  
  
> [!NOTE]  
>  В ODBC 3.5 вызов **SQLCancel** когда обработка не выполняется в операторе не рассматривается как **SQLFreeStmt** с параметром SQL_CLOSE, но имеет все это не повлияет. Чтобы закрыть курсор, приложение должно вызывать **SQLCloseCursor**, а не **SQLCancel**.  
  
 Дополнительные сведения об асинхронной обработке см. в разделе [асинхронное выполнение](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Отмена функции, которым требуются данные  
 После **SQLExecute** или **SQLExecDirect** возвращает SQL_NEED_DATA и до передачи данных для всех параметров данных времени выполнения, приложение может вызвать **SQLCancel** Чтобы отменить выполнение инструкции. После отмены инструкцию, приложение может вызвать **SQLExecute** или **SQLExecDirect** еще раз. Дополнительные сведения см. в разделе [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 После **SQLBulkOperations** или **SQLSetPos** возвращает SQL_NEED_DATA и до передачи данных для всех столбцов данных времени выполнения, приложение может вызвать **SQLCancel** Чтобы отменить операцию. После отмены операции, приложение может вызвать **SQLBulkOperations** или **SQLSetPos** снова; Отмена не влияет на состояние курсора или текущую позицию курсора. Дополнительные сведения см. в разделе [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) или [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Отмена функции выполнение в другом потоке  
 В многопоточных приложений приложения можно отменить функцию, которая выполняется в другом потоке. Для отмены функции, приложение вызывает **SQLCancel** с тем же дескриптором инструкции, что используется целевой функции, но в другом потоке. Как функция отмены зависит от драйвера и операционной системы. Как и Отмена отдельная функция асинхронно, код возврата **SQLCancel** указывает, является ли драйвер успешно обработала запрос. Могут быть возвращены только SQL_SUCCESS или SQL_ERROR; диагностические данные не возвращаются. Если исходной функции отменяется, возвращается значение SQL_ERROR и SQLSTATE HY008 (операция отменена).  
  
 Значение, если выполняется инструкция SQL выполняется при **SQLCancel** в другом потоке для отмены выполнения инструкции является возможность для успешного выполнения и возвращаемое значение SQL_SUCCESS, указывая во время отмены также выполняется успешно. В этом случае диспетчер драйверов предполагается, что курсор, открытый при выполнении инструкции закрывается путем отмены, поэтому приложения не смогут использовать курсор.  
  
 Дополнительные сведения о работе с потоками см. в разделе [многопоточность](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Привязка буфер к параметру|[Функция SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Выполнение массовой операции вставки или обновления|[Функция SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Отменяет функции работающего асинхронно на дескриптор соединения, в дополнение к функциям **SQLCancel**.|[Функция SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Выполнение инструкции SQL|[Функция SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Выполнении подготовленной инструкции SQL|[Функция SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Освобождение дескриптора инструкции|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Получение полей диагностики записи или диагностики заголовка|[Функция SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Получение нескольких полей структуры диагностических данных|[Функция SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Возвращает следующий параметр для отправки данных|[Функция SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Отправка данных параметра во время выполнения|[Функция SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Позиционирование курсора в наборе строк, обновление данных в наборе строк, или обновление или удаление данных в результирующем наборе|[Функция SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>См. также  
 [Справочник по API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Файлы заголовков ODBC](../../../odbc/reference/install/odbc-header-files.md)
