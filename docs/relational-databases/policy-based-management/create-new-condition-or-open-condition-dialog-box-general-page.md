---
title: Диалоговое окно "Создание нового условия" или "Открытие условия", страница "Общие" | Документация Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7c5c0a596b943724ccfedc9dc2e1dec57f6c0520
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63009855"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>Диалоговое окно «Создание нового условия» или «Открытие условия», страница «Общие»
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  С помощью этого диалогового окна можно создать или изменить условие управления на основе политик. Условие — это логическое выражение, задающее набор допустимых состояний для управляемой цели управления на основе политик по отношению к аспектам. Свойства, которые можно выбрать в поле **Выражение/поле** , зависят от используемого аспекта. Дополнительные сведения о связи условий с аспектами и политиками см. в статье [Администрирование серверов с помощью управления на основе политик](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="options"></a>Параметры  
 **Название**  
 Введите имя для нового условия. Если условие уже существует, отображается его имя.  
  
 **Аспект**  
 Аспект, используемый данным условием.  
  
 **AndOr**  
 Если было создано несколько выражений, показывает, соединяются ли они с помощью оператора **And** или оператора **Or**. Если существует только одно выражение, то поле остается пустым.  
  
 **Поле**  
 Каждый аспект отображает одно или несколько настраиваемых свойств. Выберите в списке доступных свойств одно из свойств, чтобы создать выражение для данного условия.  
  
 **Оператор**  
 Выберите оператор сравнения для этого выражения. Доступны следующие операторы: =, !=, >, >=, <, <=, [NOT]LIKE, [NOT]IN. Для некоторых свойств доступны не все операторы.  
  
 **Значение**  
 Установленное значение для данного выражения. Доступные значения зависят от аспекта. Значения могут быть истинными или ложными, строковыми или числовыми. Строковые значения необходимо брать в одинарные кавычки, например: **'AdventureWorks'** . Для некоторых свойств доступны не все операторы.  
  
## <a name="group-clauses"></a>Предложения группы  
 Предложения можно группировать, чтобы они действовали как единый блок отдельно от остального запроса. Это аналогично размещению скобок вокруг выражения в математической формуле или логическом выражении. Группирование предложений полезно при построении сложных запросов.  
  
 **Группирование предложений**  
  
-   Нажмите клавишу SHIFT или CTRL, а затем щелкните несколько предложений, чтобы выбрать диапазон. Щелкните правой кнопкой мыши выделенную область и выберите пункт **Предложения группы**.  
  
## <a name="see-also"></a>См. также:  
 [Администрирование серверов с помощью управления на основе политик](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
