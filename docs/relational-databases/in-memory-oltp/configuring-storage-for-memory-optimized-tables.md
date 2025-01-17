---
title: Настройка хранилища для таблиц, оптимизированных для памяти | Документация Майкрософт
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a35c519b2fa2085371ae07d35489d5417e885a59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047995"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Настройка хранилища оптимизированных для памяти таблиц
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Необходимо настроить емкость подсистемы хранения и количество операций ввода-вывода в секунду (IOPS).  
  
## <a name="storage-capacity"></a>Емкость хранилища  
 Чтобы оценить объем памяти, который потребуется для размещения надежных, оптимизированных для памяти таблиц баз данных, используйте сведения из раздела [Оценка требований к объему памяти для таблиц, оптимизированных для памяти](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) . Поскольку индексы не сохраняются в оптимизированных для памяти таблицах, не учитывайте размер индексов. После определения размера необходимо выделить место на диске, которое будет в четыре раза больше размера надежных, оптимизированных для памяти таблиц.  
  
## <a name="storage-iops"></a>IOPS хранилища  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] может значительно повысить количество операций, выполняемых в рамках рабочей нагрузки. Поэтому важно убедиться в том, что подсистема ввода-вывода не станет узким местом.  
  
-   При миграции таблиц, находящихся на диске, в оптимизированные для памяти таблицы убедитесь в том, что журнал транзакций находится на носителе, который способен поддерживать возросшее число операций журнала транзакций. Например, если носитель поддерживает обработку операций журнала транзакций на скорости в 100 МБ/сек, а оптимизированные для памяти таблицы работают в пять раз быстрее, носитель, на котором находится журнал транзакций, также должен позволять увеличить производительность в пять раз, чтобы операции журнала транзакций не стали узким местом в системе.  
  
-   Оптимизированные для памяти таблицы сохраняются в файлах контрольных точек, которые находятся в одном или нескольких контейнерах. Каждый контейнер обычно следует сопоставить с собственным запоминающим устройством. Он служит для увеличения емкости хранилища и числа операций ввода-вывода в секунду. Необходимо убедиться в том, что последовательные операции ввода-вывода носителя могут поддерживать пропускную способность журнала транзакций, которая будет в три раза выше. Объем данных, записываемых в файлы контрольных точек, составляет 256 КБ для файлов данных и 4 КБ для разностных файлов.
  
     - Например, если оптимизированные для памяти таблицы выполняют операции с журналом транзакций с постоянной скоростью 500 МБ/с, то хранилище оптимизированных для памяти таблиц должно поддерживать скорость ввода-вывода в 1,5 ГБ/с. Потребность в увеличении постоянной пропускной способности журнала транзакций в три раза обусловлена тем, что, как было отмечено, в пары файла данных и разностного файла сначала записываются начальные данные, а затем в рамках операции объединения их необходимо считывать и перезаписывать.  
  
- Еще одним фактором при оценке IOPS для хранилища является время восстановления оптимизированных для памяти таблиц. Данные из надежных таблиц должны быть считаны в память до того, как база данных станет доступна приложениям. Обычно загрузку данных в оптимизированные для памяти таблицы можно выполнять со скоростью IOPS. Поэтому, если общий объем хранилища для надежных, оптимизированных для памяти таблиц составляет 60 ГБ и необходимо обеспечить возможность загружать эти данные за одну минуту, для хранения должно быть задано значение IOPS в 1 ГБ/сек.  
  
-   Файлы контрольных точек, как правило, распределяются равномерно по всем контейнерам, если достаточно свободного места. В SQL Server 2014 необходимо подготавливать нечетное число контейнеров, чтобы обеспечить равномерное распределение. Начиная с версии SQL Server 2016 равномерное распределение достигается как при нечетном, так и при четном количестве контейнеров.
  
## <a name="encryption"></a>Шифрование  
 В [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] хранилище таблиц, оптимизированных для памяти, будет зашифровано в ходе включения прозрачного шифрования данных в базе данных. Дополнительные сведения см. в статье [Прозрачное шифрование данных (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md). В [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] файлы контрольных точек не шифруются, даже если для базы данных включено прозрачное шифрование данных.
  
## <a name="see-also"></a>См. также:  
 [Создание и управление хранилищем для оптимизированных для памяти объектов](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
