---
title: Метод setIntegratedSecurity (SQLServerDataSource) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7d922c2c2fcfadb6b7807b8d2845f8d3e6c5188c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780449"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>Метод setIntegratedSecurity (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Задает значение типа **Boolean**, определяющее, включено ли свойство integratedSecurity.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Параметры  
 *enable*  
  
 Значение **true**, если включено integratedSecurity. В противном случае — **false**.  
  
## <a name="remarks"></a>Remarks  
 Установите значение "**true**", чтобы служба [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] использовала учетные данные Windows для проверки подлинности пользователя приложения. Если установлено значение "**true**", то [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] выполняет поиск учетных данных, которые уже были предоставлены при входе в сеть или на компьютер, в локальном кэше учетных данных компьютера. Если установлено значение "**false**", необходимо будет предоставить имя пользователя и пароль.  
  
> [!NOTE]  
>  Это свойство поддерживается только в операционных системах Windows [!INCLUDE[msCoName](../../../includes/msconame_md.md)].  
  
 Дополнительные сведения об использовании встроенной проверки подлинности см. в разделе [построения URL-АДРЕСЕ соединения](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Класс SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
