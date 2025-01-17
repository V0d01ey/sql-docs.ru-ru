---
title: Параметры проекта (сопоставление типов) (AccessToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8a695217909641c737b7780fc4f8b80b2cb08152
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299133"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Параметры проекта (сопоставление типов) (AccessToSQL)
Параметры сопоставления типов проекта позволяет настроить сопоставления типов по умолчанию для проекта SSMA. Можно также указать сопоставления типов для отдельных объектов базы данных. Дополнительные сведения см. в разделе [сопоставление исходного и целевого типов данных](mapping-source-and-target-data-types-accesstosql.md).  
  
Сопоставление типов можно найти в **параметры проекта** и **параметры проекта по умолчанию** диалоговые окна:  
  
-   Используйте **параметры проекта** диалоговое окно, чтобы задать параметры конфигурации для текущего проекта. Для доступа к параметрам сопоставление типа, на **средства** меню, выберите **параметры проекта**, а затем нажмите кнопку **сопоставление типов** в левой области.  
  
-   Используйте **параметры проекта по умолчанию** диалоговое окно, чтобы задать параметры конфигурации для всех проектов. Чтобы открыть параметры сопоставления типов, в **средства** меню, выберите **параметры проекта по умолчанию**, выберите тип проекта миграции, для которого требуются параметры просмотра или изменения из  **Целевой версии миграции** раскрывающийся список, а затем нажмите кнопку **сопоставления типов** в левой области.  
  
## <a name="options"></a>Параметры  
**Исходный тип**  
Необходимо сопоставить тип данных доступа.  
  
**Тип целевого объекта**  
Целевой объект [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или тип данных SQL Azure для указанного типа данных доступа.  
  
В следующей таблице показано сопоставление по умолчанию между исходным и целевым типами данных.  
  
|Тип данных Microsoft Access|Тип данных SQL Server|  
|--------------------|------------------------|  
|**двоичные [\*.. \*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**Валюта**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**Идентификатор GUID**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**Long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**MEMO**|**nvarchar(max)**|  
|**MEMO** — для Access 97|**varchar(max)**|  
|**Единый**|**real**|  
|**text[\*..\*]**|**nvarchar [\*]**|  
|**текст [\*.. \*]** — для Access 97|**varchar [\*]**|  
  
**Добавить**  
Щелкните, чтобы добавить в список сопоставления типа данных.  
  
**Изменить**  
Щелкните, чтобы изменить тип данных в списке сопоставление.  
  
**Удалить**  
Щелкните, чтобы удалить сопоставление типов данных, выбранного в списке сопоставление.  
  
**Сброс до значений по умолчанию**  
Щелкните, чтобы сбросить все сопоставления типов данных по умолчанию SSMA.  
  
## <a name="see-also"></a>См. также  
[Сопоставление исходного и целевого типов данных](mapping-source-and-target-data-types-accesstosql.md)  
[Reference(Access) интерфейса пользователя](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
