---
title: Настройка виртуальных серверов в IIS | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 16130f9e96dfc70ef464e3ff48301c9f71c0bb06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704333"
---
# <a name="configuring-virtual-servers-on-iis"></a>Настройка виртуальных серверов в IIS
При создании виртуальных серверов в Internet Information Services 4.0, следующие два дополнительных действия необходимы для настройки виртуального сервера для работы с помощью служб удаленных рабочих СТОЛОВ.  
  
1.  При настройке сервера, проверьте «Разрешить доступ Execute».  
  
2.  Переместить msadcs.dll для *vroot*\msadc, где *vroot* является домашним каталогом виртуального сервера.  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ, больше не включаются в операционной системе Windows (см. в разделе Windows 8 и [настольная книга по совместимости Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будет поддерживаться в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ, следует перевести [WCF-сервиса данных](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>См. также  
 [Основные принципы RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


