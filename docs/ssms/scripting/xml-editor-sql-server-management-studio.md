---
title: Редактор XML (среда SQL Server Management Studio) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.editor.xml.f1
- sql13.swb.editorxml.f1
- vs.xmleditor
- sql13.swb.xmleditor.f1
helpviewer_keywords:
- XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eda7c83e982bbf6c006ac9a6c470b116009420ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821550"
---
# <a name="xml-editor-sql-server-management-studio"></a>Редактор XML (среда SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Предоставляет набор визуальных средств для работы с XML-схемами, наборами данных ADO.NET и XML-документами. Конструктор XML поддерживает язык определения схем XML (XSD), определенный консорциумом World Wide Web (WC3). Этот конструктор не поддерживает определения DTD (определения типов файлов) или другие языки XML-схем, например XDR (XML-Data Reduced).  
  
 Чтобы открыть конструктор, добавить набор данных, XML-схему или XML-файл к проекту или открыть любой файл одного из типов, перечисленных в следующей таблице.  
  
> [!CAUTION]  
>  Команда **Отменить** отсутствует при работе в представлении «Схема». Тщательно спланируйте свою работу и чаще сохраняйте файлы.  
  
 Конструктор предоставляет следующие три представления (или режима) для работы с XML-файлами, XML-схемами и наборами данных.  
  
|Представление|Описание|Поддерживаемые типы файлов|  
|----------|-----------------|--------------------------|  
|**Схема**|Для визуального создания и изменения XML-схем и наборов данных ADO.NET.|.xsd|  
|**Данные**|Для визуального изменения файлов XML-данных в структурированной сетке данных.|XML|  
|**XML**|Для редактирования кода XML; редактор кода предоставляет цветовое выделение синтаксиса и технологию IntelliSense, включая команды «Завершить слово» и «Показать элементы».|.xml .xsd .xslt .wsdl.web.resx.tdl.wsf.hta.disco.vsdisco.config|  
|**Инструкция ShowPlan**|Выводит планы запросов xml, созданные в режиме SET SHOWPLAN_XML ON.|.showplan|  
  
## <a name="schema-view"></a>Представление схемы  
 Представление схемы предоставляет визуальное отображение элементов, атрибутов, типов и т. д., которые делают наглядными XML-схемы и наборы данных ADO.NET.  
  
 В представлении схемы можно конструировать схемы и наборы данных, перенося элементы в области конструктора с вкладки области элементов «XML-схема» или из обозревателя серверов. Кроме того, можно добавить в конструктор элементы, щелкнув область конструктора правой кнопкой мыши и выбрав пункт «Добавить» из контекстного меню.  
  
 В представлении схемы можно:  
  
-   создавать и изменять существующие XML-схемы и наборы данных ADO.NET;  
  
-   создавать и изменять связи между таблицами;  
  
-   создавать и изменять ключи;  
  
-   формировать наборы данных ADO.NET из XML-схем.  
  
> [!NOTE]  
>  Расположение элементов в представлении схемы сохраняется в файле с расширением XSX, который можно увидеть, нажав кнопку **Показать все файлы** на панели инструментов в обозревателе решений и развернув файл с расширением XSD. Если XSX-файлы отсутствуют, это значит, что XSD-файл никогда не открывался в конструкторе XML.  
  
### <a name="customizing-schema-view"></a>Настройка представления схемы  
 Следующие функции изменяют визуальное расположение элементов в представлении схемы:  
  
-   изменение масштаба;  
  
-   развертывание или свертывание вложенных элементов;  
  
-   автоматическое расположение элементов;  
  
-   сброс до стандартного состояния свернутых элементов.  
  
##### <a name="to-expand-hidden-nested-elements"></a>Развертывание скрытых вложенных элементов  
  
-   Щелкните значок «плюс» внизу элемента.  
  
##### <a name="to-collapse-nested-elements"></a>Сворачивание вложенных элементов  
  
-   Щелкните значок «минус» у самого нижнего элемента, который должен остаться в конструкторе.  
  
## <a name="data-view"></a>Представление данных  
 Представление данных предоставляет сетку данных для изменения XML-файлов. В этом представлении можно изменять только содержимое XML-файла (но не теги и структуру).  
  
 В представлении "Данные" есть две отдельные области: **Таблицы данных** и **Данные**. Область **Таблица данных** — это список взаимоотношений, определенных в XML-файле в порядке вложенности (от самых внешних к самым внутренним). Область **Данные** — это сетка данных, отображающая данные на основании выбора в области «Таблица данных».  
  
> [!NOTE]  
>  Новые файлы XML не содержат данных и не могут отображаться в представлении данных. Есть также некоторые XML-документы, для которых не может быть применено представление данных. Хотя XML считается допустимым форматом, при попытке переключения на неструктурированные данные представление "Данные" создаст следующее сообщение: "Документ имеет правильный формат, но в нем содержится структура, не отображаемая представлением «Данные»".  
  
 В представлении данных можно:  
  
-   вручную заполнять таблицы данных;  
  
-   изменять существующие таблицы данных;  
  
-   формировать XML-схемы из XML-документа.  
  
## <a name="xml-view"></a>Представление XML  
 Представление XML — это редактор для работы с кодом XML, обеспечивающий технологию IntelliSense и выделение кода цветом. Завершение операторов доступно при работе с файлами XSD и XML, для которых есть соответствующие схемы. Введите < для начала набора тега, и программа выведет список доступных в данном месте элементов. После ввода элемента и нажатия клавиши ПРОБЕЛ программа выводит список атрибутов, поддерживаемых данным элементом.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] недоступны на панели инструментов. Для доступа к этим параметрам в XML-редакторе в меню **Правка** выберите пункт **технология IntelliSense**.  
  
## <a name="showplan-view"></a>Представление инструкции SHOWPLAN  
 Планы запросов можно сохранить в XML-формате, если они создавались с использованием параметра SET SHOWPLAN_XML ON. Дважды щелкните мышью по файлу с расширением SHOWPLAN, чтобы открыть план запроса.  
  
## <a name="see-also"></a>См. также:  
 [Сохранение плана выполнения в формате XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
