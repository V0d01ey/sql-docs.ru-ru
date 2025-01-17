---
title: Получить данные из Независимых - Analytics Platform System | Документация Майкрософт
description: Сведения, получаемые от независимого поставщика Оборудования о Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57b61ed7741bc6d36b7531a62416893e7cc10fb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150232"
---
# <a name="information-to-obtain-from-your-ihv"></a>Сведения, получаемые от независимого поставщика Оборудования
Когда поставщиком независимых оборудования (IHV) позволяет вашей новым устройством SQL Server PDW, они также позволяют предоставлять сведения о конфигурации оборудования устройства, выполняли на устройстве. Вам потребуется эта информация для администрирования устройства.  
  
Ниже перечислены сведения, которые обычно требуется, от независимого поставщика Оборудования. В некоторых случаях требуется дополнительные или другие сведения. Обратитесь к независимому поставщику Оборудования, чтобы убедиться в том, что вся необходимая информация была передана вам с доставкой устройства.  
  
|||  
|-|-|  
|**Сведения или документа**|**Описание**|  
|Ведомость материалов (BOM)|Ведомости материалов перечислены компоненты, включенные в устройстве. Эта информация необходима для подтверждения того, что все компоненты были доставлены.<br /><br />**Внимание!** Ведомости материалов должен включать весовые коэффициенты для каждого из узлов устройства, а также для каждого полный стойки. Эта информация важна при планировании и как обрабатывать и перемещать компоненты устройства и позволяющий удостовериться в том центре обработки данных могут обеспечивать устройства. Если вашей Спецификации, не имеет весовые коэффициенты узлов, убедитесь, что для получения этих сведений из независимого поставщика Оборудования для всех узлов.|  
|Кабели схем|Кабельных диаграммы показывают способ подключения сети, питания и кабели, другие для каждого устройства для установки в стойку. Эти схемы необходимы при установке устройства в центре обработки данных, и в любое время, вам нужно удалить или заменить компонент.|  
|Требования к стоек устройства|Перед установкой устройства в центре обработки данных, необходимо знать, если центр обработки данных отвечает воздушный поток и длина кабеля требованиям для устройства, а также размер и энергопотребление компонентов. См. также спецификации (Спецификация) выше сведения о весовые коэффициенты компонента устройства, который также является обязательным.|  
  
