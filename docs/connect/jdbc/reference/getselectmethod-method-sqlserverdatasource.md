---
title: Метод getSelectMethod (SQLServerDataSource) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6255d2e-0028-474a-afa8-553ef092243e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcdec15bb04af85cb068ea209625e9a10d8f85db
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792026"
---
# <a name="getselectmethod-method-sqlserverdatasource"></a>Метод getSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Возвращает тип курсора по умолчанию, используемый для всех результирующих наборов, созданных с помощью объекта [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public java.lang.String getSelectMethod()  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 Значение **String**, содержащее тип курсора по умолчанию.  
  
## <a name="remarks"></a>Remarks  
 Свойство selectMethod задает тип курсора по умолчанию, который используется для результирующего набора. Это свойство полезно при работе с крупными результирующими наборами, когда не нужно сохранять результирующий набор целиком в памяти клиента. Если установить это свойство в значение cursor, то можно создать серверный курсор, который будет получать данные меньшими фрагментами. Если свойство selectMethod не задано, метод getSelectMethod возвращает значение по умолчанию (direct).  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Класс SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
