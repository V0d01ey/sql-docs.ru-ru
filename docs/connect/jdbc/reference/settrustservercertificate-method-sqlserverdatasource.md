---
title: Метод setTrustServerCertificate (SQLServerDataSource) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 93feffdb0135e4530b43a6f092c581d145b5c0c6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783527"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Метод setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Задает значение типа **Boolean**, определяющее, включено ли свойство trustServerCertificate.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Параметры  
 *trustServerCertificate*  
  
 Значение **true**, если SSL-сертификат должен автоматически считаться доверенным, когда на уровне связи применяется SSL-шифрование. В противном случае — **false**.  
  
## <a name="remarks"></a>Remarks  
 Если свойство trustServerCertificate имеет значение **true**, то SSL-сертификат [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] автоматически считается доверенным, когда на уровне связи применяется SSL-шифрование. Иными словами, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] не будет выполнять проверку SSL-сертификата [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Значение по умолчанию — **false**.  
  
 Если свойство trustServerCertificate имеет значение **false**, то [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] будет проверять SSL-сертификат сервера.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Класс SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
