---
title: IRowsetFastLoad::Commit (OLE DB) | Документация Майкрософт
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 1c1ac06ce8fe0d76858e10506d4ff6c054517f68
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761504"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Обозначает конец пакета вставляемых строк и записывает эти строки в таблицу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Примеры, см. в разделе [массового копирования данных с помощью IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) и [отправить данные больших двоичных ОБЪЕКТОВ SQL SERVER с помощью IROWSETFASTLOAD и ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Аргументы  
 *fDone*[in]  
 Если значение равно FALSE, то набор строк сохраняет достоверность и может использоваться пользователем для дополнительной вставки строк. Если значение равно TRUE, то набор строк теряет достоверность и пользователь не может выполнять дальнейшую вставку.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 S_OK  
 Метод завершился успешно, и все добавленные записи были записаны в таблицу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Произошла ошибка, зависящая от поставщика. Получите сведения об ошибке для конкретного текста ошибки из поставщика.  
  
 E_UNEXPECTED  
 Этот метод был вызван применительно к набору строк массового копирования, который ранее стал недействительным в результате выполнения метода **IRowsetFastLoad::Commit**.  
  
## <a name="remarks"></a>Remarks  
 Драйвер OLE DB для SQL Server набору строк массового копирования, ведет себя как набор строк в режиме отложенного обновления. По мере вставки пользователем данных строк с помощью набора строк добавленные строки обрабатываются таким же образом, как и ожидающие выполнения вставки для набора строк, поддерживающего **IRowsetUpdate**.  
  
 Пользователь должен вызвать метод **Commit** применительно к набору строк массового копирования, чтобы записать добавленные строки в таблицу [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] таким же образом, как и при использовании метода **IRowsetUpdate::Update** для отправки ожидающих строк в экземпляр SQL Server.  
  
 Если пользователь освобождает ссылку на набор данных массового копирования, не вызывая метод **Commit**, то все добавленные строки, которые не были записаны, теряются.  
  
 Пользователь может сгруппировать добавленные строки, вызывая метод **Commit** с аргументом *fDone* в значении FALSE. Если аргумент *fDone* установлен в значение TRUE, то набор строк становится недействительным. Недействительным набором строк массового копирования поддерживаются только интерфейс **ISupportErrorInfo** и метод **IRowsetFastLoad::Release**.  
  
## <a name="see-also"></a>См. также:  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
