---
title: Метод CreateObject (служба удаленных рабочих СТОЛОВ) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 918836e949593672417240c1b91026e1e02c4788
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712319"
---
# <a name="createobject-method-rds"></a>Метод CreateObject (служба удаленных рабочих столов)
Создает прокси для целевого бизнес-объекта и возвращает указатель на него. Прокси-сервера пакетов и выполняет маршалинг данные заглушки на стороне сервера для обмена данными с бизнес-объект для отправки запросов и данных через Интернет. Для объектов в процессе компонент прокси-серверы не используются, предоставляется только указатель на объект.  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ, больше не включаются в операционной системе Windows (см. в разделе Windows 8 и [настольная книга по совместимости Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будет поддерживаться в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ, следует перевести [WCF-сервиса данных](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Синтаксис  
 Служба Remote Data Service поддерживает следующие протоколы: HTTP, HTTPS (HTTP через протокол SSL), DCOM и внутри процесса.  
  
|Protocol|Синтаксис|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|В процессе|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Параметры  
 *Объект*  
 Переменную объекта, результатом которого является объект, который является типом, указанным в *ProgID*.  
  
 *Пространство данных*  
 Объектную переменную, которая представляет [RDS. Пространство данных](../../../ado/reference/rds-api/dataspace-object-rds.md) объект, используемый для создания экземпляра нового объекта.  
  
 *Идентификатор progID*  
 Объект **строка** значение, содержащее программный идентификатор, указывающий на стороне сервера бизнес-объект, реализующий приложения бизнес-правила.  
  
 *awebsrvr* или *computername*  
 Объект **строка** значение, представляющее URL-адрес, идентифицирующий веб-службы Internet Information Services (IIS) сервера, где создается экземпляр сервера бизнес-объекта.  
  
## <a name="remarks"></a>Примечания  
 *Протокола HTTP* — стандартная веб-протокол; *HTTPS* — безопасный веб-протокол. Используйте *протокола DCOM* при выполнении локальной сети без HTTP. *В процессе* протокол — локальную библиотеку динамической компоновки (DLL); он использует сеть.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект DataSpace (служба удаленных рабочих столов)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>См. также  
 [Объект DataFactory, метод запроса и пример метода CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [Объекта DataSpace и метода CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Метод CreateRecordset (служба удаленных рабочих столов)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


