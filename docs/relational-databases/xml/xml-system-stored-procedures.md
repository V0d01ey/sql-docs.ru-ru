---
title: Системные хранимые процедуры XML | Документация Майкрософт
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7ecfcddc242bc9a30dd91acc7863e449ce82729
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703991"
---
# <a name="xml-system-stored-procedures"></a>Системные хранимые процедуры XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  СУБД SQL Server предоставляет следующие системные хранимые процедуры, которые используются вместе с инструкцией OPENXML:  
  
-   [sp_xml_preparedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 Чтобы составлять запросы с помощью OPENXML, нужно сначала создать внутреннее представление XML-документа, вызвав процедуру **sp_xml_preparedocument**. Эта хранимая процедура возвращает дескриптор внутреннего представления XML-документа. Затем этот дескриптор передается инструкции OPENXML. Инструкция OPENXML предоставляет представления наборов строк документа, основанные на выражениях XPaths. Точнее, это одна комбинация для строк и одна или несколько для столбцов.  
  
> [!NOTE]  
>  Дескриптор документа, возвращаемый процедурой **sp_xml_preparedocument** , действителен в течение сеанса.  
  
 Внутреннее представление XML-документа можно удалить из памяти вызовом системной хранимой процедуры **sp_xml_removedocument** .  
  
## <a name="see-also"></a>См. также:  
 [OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML (SQL Server)](../../relational-databases/xml/openxml-sql-server.md)  
  
  
