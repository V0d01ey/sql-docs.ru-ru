---
title: Элементы SQLServerXAConnection | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1399700551402870a4eeb7cd2339a7a2e937468f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797493"
---
# <a name="sqlserverxaconnection-members"></a>Элементы SQLServerXAConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  В следующих таблицах перечислены доступные элементы класса [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md).  
  
## <a name="constructors"></a>Конструкторы  
 Нет.  
  
## <a name="fields"></a>Поля  
 Нет.  
  
## <a name="inherited-fields"></a>Наследуемые поля  
 Нет.  
  
## <a name="methods"></a>Методы  
  
|Имя|Описание|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(Наследуется от [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)). Регистрирует заданный прослушиватель событий для получения уведомлений о событии в этом объекте Connection.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(Наследуется от [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)). Закрывает физическое соединение, представляемое этим объектом Connection.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(Наследуется от [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)). Создает дескриптор объекта для физического соединения, представляемого этим объектом Connection.|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|Возвращает объект [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md), который будет использоваться диспетчером транзакций для управления участием этого объекта [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) в распределенной транзакции.|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(Наследуется от [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)). Удаляет заданный прослушиватель событий.|  
  
## <a name="inherited-methods"></a>Наследуемые методы  
  
|Класс, из которого наследуется:|Методы|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>См. также:  
 [Класс SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
