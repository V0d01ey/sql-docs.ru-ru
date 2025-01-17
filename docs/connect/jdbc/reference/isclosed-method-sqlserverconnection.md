---
title: Метод isClosed (SQLServerConnection) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 509de1454b2f86aa52028fdd6921fb02fedf5f27
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796588"
---
# <a name="isclosed-method-sqlserverconnection"></a>Метод isClosed (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Указывает, был ли закрыт этот объект [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 **значение true,** значение Если соединение закрыто **false** Если это не так.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод isClosed указывается с помощью метода isClosed в интерфейсе java.sql.Connection.  
  
 Проверяет состояние вызванного объекта SQLServerConnection. Соединение считается закрытым, если для него вызван метод [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) либо если произошли определенные неустранимые ошибки. Этот метод будет возвращать значение **true**, только если он вызывается после вызова метода close.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Класс SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
