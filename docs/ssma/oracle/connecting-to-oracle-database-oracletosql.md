---
title: Подключение к базе данных Oracle (OracleToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 4ad868122fd8986c642bace1b2c9cf419bb89182
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288402"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Подключение к базе данных Oracle (OracleToSQL)
Для переноса баз данных Oracle в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], необходимо подключиться к базе данных Oracle, которые требуется перенести. При подключении, SSMA получает метаданные о всех схем Oracle и затем отображается в панели обозревателя метаданных Oracle. SSMA хранит сведения о сервере базы данных, но не хранит пароли.  
  
Подключение к базе данных остается активным, пока не закрыть проект. При повторном открытии проекта, необходимо повторно подключить, если требуется активное подключение к базе данных.  
  
Метаданные о базе данных Oracle не обновляется автоматически. Вместо этого Если вы хотите обновить метаданные в обозревателе метаданных Oracle, необходимо вручную обновить его. Дополнительные сведения см. в разделе «Обновление метаданных Oracle» далее в этом разделе.  
  
## <a name="required-oracle-permissions"></a>Oracle необходимые разрешения  
Учетная запись, которая используется для подключения к базе данных Oracle должен иметь по крайней мере **CONNECT** разрешения. Это позволяет SSMA для получения метаданных из схемы, принадлежащие подключающийся пользователь. Получить метаданные для объектов в другие схемы, а затем преобразовать объекты в этих схемах, учетная запись должна иметь следующие разрешения:  
  
-   ЛЮБАЯ ПРОЦЕДУРА, СОЗДАНИЕ  
  
-   ВЫПОЛНЕНИЕ ЛЮБОЙ ПРОЦЕДУРЫ  
  
-   ВЫБЕРИТЕ ЛЮБУЮ ТАБЛИЦУ  
  
-   ВЫБЕРИТЕ ЛЮБУЮ ПОСЛЕДОВАТЕЛЬНОСТЬ  
  
-   СОЗДАНИЕ ЛЮБОГО ТИПА  
  
-   СОЗДАНИЕ ЛЮБОГО ТРИГГЕРА  
  
-   ВЫБЕРИТЕ ЛЮБОЙ СЛОВАРЬ  
  
## <a name="establishing-a-connection-to-oracle"></a>Подключения к Oracle  
При подключении к базе данных, SSMA считывает метаданные базы данных и добавляет эти метаданные в файл проекта. Эти метаданные используются с SSMA при преобразовании данных объектов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] синтаксис, и когда оно переносит данные [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Можно просматривать эти метаданные в панели обозревателя метаданных Oracle и просмотрите свойства отдельных объектов базы данных.  
  
> [!IMPORTANT]  
> Перед попыткой подключения, убедитесь, что сервер базы данных запущен и может принимать подключения.  
  
**Для подключения к Oracle**  
  
1.  На **файл** меню, выберите **подключение к Oracle**.  
  
    Если вы ранее подключались к базе данных Oracle, команда будет называться **повторное соединение с базой данных Oracle**.  
  
2.  В **поставщика** выберите **поставщик клиента Oracle** или **поставщик OLE DB**, в зависимости от установки какой поставщик. По умолчанию используется клиент Oracle.  
  
3.  В **режим** выберите либо **стандартный режим**, **режим TNSNAME**, или **режим строки подключения**.  
  
    Позволяет указать имя сервера и порт в стандартном режиме. Используйте режим имя службы, чтобы вручную указать имя службы Oracle. Используйте режим строки подключения для предоставления полную строку подключения.  
  
4.  При выборе **стандартного режима**, введите следующие значения:  
  
    1.  В **имя_сервера** введите или выберите имя или IP-адрес сервера базы данных.  
  
    2.  Если сервер базы данных не настроен на прием подключений на значение по умолчанию порт (1521), введите номер порта, который используется для подключения к Oracle в **порт сервера** поле.  
  
    3.  В **ИД безопасности Oracle** введите идентификатор системы.  
  
    4.  В **имя пользователя** введите учетной Oracle, которая имеет необходимые разрешения.  
  
    5.  В **пароль** введите пароль для указанного имени пользователя.  
  
5.  При выборе **TNSNAME режим**, введите следующие значения:  
  
    1.  В **подключения идентификатор** введите подключения (TNS alias) идентификатор базы данных.  
  
    2.  В **имя пользователя** введите учетной Oracle, которая имеет необходимые разрешения.  
  
    3.  В **пароль** введите пароль для указанного имени пользователя.  
  
6.  При выборе **режим строки подключения**, укажите строку подключения в **строку подключения** поле.  
  
    В следующем примере строки подключения к OLE DB:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    В следующем примере показано строку подключения клиента Oracle, использующий встроенную безопасность:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Дополнительные сведения см. в разделе [подключения к Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Повторное подключение к базе данных Oracle  
Подключение к серверу базы данных остается активным, пока не закрыть проект. При повторном открытии проекта, необходимо повторно подключить, если требуется активное подключение к базе данных. Можно работать вне сети, пока вы хотите обновить метаданные, загрузки объектов базы данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и перенести данные.  
  
## <a name="refreshing-oracle-metadata"></a>Обновление метаданных Oracle  
Метаданные о базе данных Oracle не обновляется автоматически. Метаданные в обозревателе метаданных Oracle — это снимок метаданные при первом подключении, или время последнего обновления метаданных вручную. Можно вручную обновить метаданные для всех схем, одной схемы или отдельных объектов базы данных.  
  
**Для обновления метаданных**  
  
1.  Убедитесь, что вы подключены к базе данных.  
  
2.  В обозревателе метаданных Oracle установите флажок рядом с каждым объектом схемы или базы данных, который требуется обновить.  
  
3.  Щелкните правой кнопкой мыши **схемы**, или отдельные схемы, или базы данных объекта, а затем выберите **обновление из базы данных**.  
  
    Если у вас нет активного подключения, отобразит SSMA **подключение к Oracle** диалоговом таким образом, можно подключиться.  
  
4.  В обновление из базы данных-диалоговое окно укажите объекты для обновления.  
  
    -   Чтобы обновить объект, нажмите **Active** поле рядом с объектом, пока не появится стрелка.  
  
    -   Чтобы предотвратить объекта к обновлению, нажмите кнопку **Active** поле возле объект, пока не **X** отображается.  
  
    -   Чтобы обновить или отклонить категорию объектов, щелкните **Active** поле возле папка категории.  
  
    Чтобы просмотреть определения цветовое выделение синтаксиса, щелкните **условных обозначений** кнопки.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>Следующий шаг  
  
-   Следующий шаг в процессе миграции является [соединиться с экземпляром SQL Server](connecting-to-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>См. также  
[Переход с Oracle баз данных в SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
