---
title: Предложение типов столбцов диалогового окна справочника по пользовательскому интерфейсу | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b76d9fd1d248d463f8b62a1c9358851db34fd3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728094"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>Предложение типов столбцов диалогового окна справочника по пользовательскому интерфейсу

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Диалоговое окно **Предлагаемые типы столбцов** используется для идентификации типа данных и длины столбцов в диспетчере соединений с неструктурированными файлами на основе содержимого файла.  
  
 Дополнительные сведения о типах данных, используемых в [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], см. в разделе [Типы данных служб Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="options"></a>Параметры  
 **Число строк**  
 Введите или выберите число строк в выборке, используемой алгоритмом.  
  
 **Предложить наименьший тип целочисленных данных**  
 Снимите этот флажок, чтобы пропустить оценку. Если он установлен, то определяет наименьший возможный целочисленный тип данных для столбцов, содержащих целочисленные данные.  
  
 **Предложить наименьший тип данных с плавающей точкой**  
 Снимите этот флажок, чтобы пропустить оценку. Если он установлен, то определяет возможность использования вещественных данных наименьшего типа DT_R4 для столбцов, содержащих числовые данные вещественного типа.  
  
 **Определить логические столбцы по следующим значениям**  
 Введите два значения, которые следует распознавать как логические значения true и false. Значения должны быть разделены запятой, а первое из них соответствует True.  
  
 **Заполнять столбцы строкового типа**  
 Выберите этот флажок, чтобы включить дополнение строк.  
  
 **Процент заполнения**  
 Введите или выберите процент от длины столбцов, добавляемый к длине столбцов символьных типов данных. Процент должен представлять собой целое число.  
  
## <a name="see-also"></a>См. также:  
 [Справочник по сообщениям об ошибках служб Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Диспетчер соединений с неструктурированными файлами](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
