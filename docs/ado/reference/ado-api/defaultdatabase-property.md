---
title: Свойство DefaultDatabase | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2eb89353c29ae58194f89b48502f0a9cc5522b58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695451"
---
# <a name="defaultdatabase-property"></a>Свойство DefaultDatabase
Указывает базу данных по умолчанию для [подключения](../../../ado/reference/ado-api/connection-object-ado.md) объекта.  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Возвращает или задает **строка** значению, которое возвращает имя базы данных от поставщика.  
  
## <a name="remarks"></a>Примечания  
 Используйте **DefaultDatabase** свойство задает или возвращает имя базы данных по умолчанию на определенной **подключения** объекта.  
  
 Если имеется база данных по умолчанию, строки SQL использовать неполное синтаксис для доступа к объектам в этой базе данных. Для доступа к объектам в базе данных, отличный от указанного в **DefaultDatabase** свойства, необходимо указать имена объектов имя нужной базы данных. При подключении, поставщик будет записывать сведения о базе данных по умолчанию для **DefaultDatabase** свойство. Некоторые поставщики разрешают только одну базу данных на соединение, в этом случае нельзя изменить **DefaultDatabase** свойство.  
  
 Некоторые источники данных и поставщики могут не поддерживать эту функцию и может вернуть ошибку или пустой строкой.  
  
> [!NOTE]
>  **Удаленное использование службы данных** это свойство доступно не на стороне клиента **подключения** объекта.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>См. также  
 [Provider и Defaultdatabase свойства (Visual Basic)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Примеры свойств Provider и DefaultDatabase (Visual C++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
