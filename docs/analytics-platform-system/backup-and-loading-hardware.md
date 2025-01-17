---
title: Резервное копирование и загрузка оборудование — Parallel Data Warehouse
description: Чтобы развернуть данные end-to-end, удобное решение для хранения в Analytics Platform System (APS) с Parallel Data Warehouse (PDW), необходимо создать план резервного копирования в хранилище данных и загрузки данных. Применение этих рекомендаций позволит приобретать и настраивать серверы резервного копирования и загрузки, которые будут соответствовать вашим потребностям.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4d7f7b6b4edea9dacab7287a7936b7fd87fd7973
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065141"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Резервное копирование и загрузка оборудованию - Parallel Data Warehouse
Чтобы развернуть данные end-to-end, удобное решение для хранения в Analytics Platform System (APS) с Parallel Data Warehouse (PDW), необходимо создать план резервного копирования в хранилище данных и загрузки данных. Применение этих рекомендаций позволит приобретать и настраивать серверы резервного копирования и загрузки, которые будут соответствовать вашим потребностям.  
  
## <a name="acquire-and-configure-backup-servers"></a>Приобретение и настройка резервного копирования серверов  
![Резервное копирование процесс](media/backup-process.png "резервного копирования процесс")  
  
Чтобы создать резервную копию базы данных PDW, требуется один или несколько резервных серверов. Можно использовать существующее оборудование или приобретать новое компьютерное оборудование. Дополнительные сведения см. в разделе [приобретение и настройка сервера резервного копирования](acquire-and-configure-backup-server.md). Эти инструкции включают [резервного копирования таблица планирования емкости сервера](backup-capacity-planning-worksheet.md) помогут вам спланировать эффективное решение для резервного копирования.  
  
## <a name="acquire-and-configure-loading-servers"></a>Приобретение и настройка при загрузке серверов  
![Процесс загрузки](media/loading-process.png "процесс загрузки")  
  
Чтобы загрузить данные, требуется один или несколько серверов загрузки. Вы можете использовать собственные существующие ETL или других серверах, или вы можете приобрести новые серверы. Дополнительные сведения см. в разделе [запросов и настройка сервера для загрузки](acquire-and-configure-loading-server.md). Эти инструкции включают [загрузки таблица планирования емкости сервера](loading-server-capacity-planning-worksheet.md) помогут вам спланировать эффективное решение для загрузки.  
  
## <a name="see-also"></a>См. также  
[Обзор резервного копирования и восстановления](backup-and-restore-overview.md)  
[Обзор загрузки](load-overview.md)  
  
