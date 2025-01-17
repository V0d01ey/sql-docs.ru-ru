---
title: Параметры (Синхронизация) (MySQLToSQL) проекта | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e82fa9d02fdbfe876f4097c54c6877c3a3a81fee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473910"
---
# <a name="project-settings-synchronization-mysqltosql"></a>Параметры проекта (синхронизация) (MySQLToSQL)
Синхронизация **параметры проекта** позволяют настраивать, как объекты базы данных MySQL синхронизируются с объектами базы данных SQL Server.  
  
Действия по умолчанию параметры по умолчанию для обновления объектов из базы данных MySQL, а также для синхронизации объектов с базой данных SQL Server. Дополнительные сведения см. в разделе [обновление из базы данных &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Двух различных страницах синхронизации, которые содержат те же параметры доступны:  
  
-   Чтобы указать параметры для всех будущих проектов SSMA на **средства** меню, нажмите кнопку **DefaultProject параметры**и нажмите кнопку **синхронизации** в нижней части левой панели.  
  
-   Для задания параметров для текущего проекта, на **средства** меню, нажмите кнопку **параметры проекта**, а затем нажмите кнопку **синхронизации** в нижней части левой панели.  
  
## <a name="options"></a>Параметры  
  
##### <a name="misc"></a>Разное  
  
##### <a name="attempts"></a>Попытки  
Предоставляет информацию о число проходов, принимают можно загрузить в SQL Server. Загрузка объектов в SQL Server обычно выполняется в несколько проходов. Объекты, которые не удалось загрузить в первом проходе, например внешние ключи, может успешно загрузить в следующей проверки.  
  
По умолчанию значение равно 2.  
  
## <a name="synchronization-for-mysql"></a>Синхронизация для MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Действие при изменении локальных и удаленных объектов  
Указывает значение по умолчанию в диалоговом окне синхронизации, при определении объекта в SSMA и на сервере базы данных.  
  
-   Если вы выбрали обновление из базы данных, SSMA загрузит определений базы данных в метаданные, при выполнении условия.  
  
-   При выборе Skip SSMA не выполняет каких-либо действий обновления.  
  
##### <a name="action-on-local-object-change"></a>Действие при изменении локального объекта  
Указывает значение по умолчанию в диалоговом окне синхронизации при изменении объекта в SSMA.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
##### <a name="action-on-remote-object-change"></a>Действие при изменении удаленного объекта  
Указывает значение по умолчанию в диалоговом окне синхронизации при изменении объектов на сервере базы данных.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Действие при отсутствии локального объекта метаданных  
Указывает значение по умолчанию в диалоговом окне синхронизации, при отсутствии локальные метаданные.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не выполняет каких-либо действий обновления  
  
## <a name="synchronization-for-sql-server"></a>Синхронизация для SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Действие при изменении объекта локальные и удаленные  
Указывает значение по умолчанию в диалоговом окне синхронизации, при определении объекта в SSMA и на сервере базы данных.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **запись в базу данных**, SSMA обновит объектов базы данных в соответствии с SSMA метаданные содержимого, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
##### <a name="action-on-local-object-change"></a>Действие при изменении локального объекта  
Указывает значение по умолчанию в диалоговом окне синхронизации при изменении объекта в SSMA.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **запись в базу данных**, SSMA будет обновить объект в базе данных в соответствии с SSMA метаданные содержимого, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
##### <a name="action-on-remote-object-change"></a>Действие при изменении удаленного объекта  
Указывает значение по умолчанию в диалоговом окне синхронизации при изменении объектов на сервере базы данных.  
  
-   При выборе **обновление из базы данных**, SSMA будет загружать определения базы данных в метаданные, при выполнении условия.  
  
-   При выборе **запись в базу данных**, SSMA будет обновить объект в базе данных в соответствии с SSMA метаданные содержимого, при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Действие при отсутствии локального объекта метаданных  
Указывает значение по умолчанию в диалоговом окне синхронизации, при отсутствии локальных метаданных.  
  
-   При выборе **обновление из базы данных**, SSMA выбирает обновления из параметра базы данных, при выполнении условия.  
  
-   При выборе **запись в базу данных**, SSMA приведет к удалению объекта из базы данных при выполнении условия.  
  
-   При выборе **Skip**, SSMA не будет выполнять какие-либо действия обновления.  
  
