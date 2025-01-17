---
title: Новые возможности в SSMA для SAP ASE (SybaseToSQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 727ede7a057491eea2ea230d7057aa3228b5fc82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66841104"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Новые возможности в SSMA для SAP ASE (SybaseToSQL)
В этой статье перечислены SQL Server Migration Assistant (SSMA) для SAP ASE (прежнее название — SSMA для Sybase) изменения в каждом выпуске.

## <a name="ssma-v82"></a>SSMA v8.2

В выпуске v8.2 SSMA для SAP ASE дополнено целевой набор исправлений, призванных повысить качество и метрики преобразования, а также исправления для:

* Проблемы с отключенные некластеризованные индексы, после переноса данных.
* Обнаружение .NET Framework во время автоматической установки.
* Периодические сбой, который происходит при загрузке новой версии.

> [!NOTE]
> Известная проблема с помощью автоматического обновления могут вызвать сбой обновления из SSMA v8.1 для v8.2. Если эта ошибка возникает, загрузите новую версию и установить его вручную.

> [!IMPORTANT]
> SSMA v7.4 и более поздних версий .net 4.5.2 является необходимым условием установки.

## <a name="ssma-v81"></a>SSMA v8.1

В выпуске v8.1 SSMA для SAP ASE дополнено целевых исправлений, которые предназначены для улучшения показателей качества и преобразования.

> [!NOTE]
> Известная проблема с помощью автоматического обновления могут вызвать сбой обновления из SSMA v8.0 для версии 8.1. Если эта ошибка возникает, загрузите новую версию и установить его вручную.

## <a name="ssma-v80"></a>SSMA v8.0

В выпуске версии 8.0 SSMA для SAP ASE дополнено целевых исправлений, предназначенный для повышения качества и преобразования метрики. Кроме того этот выпуск предлагает следующие новые функции:

* Поддержка **Azure базы данных SQL управляемого экземпляра** как целевой объект. Теперь можно создать новые проекты, предназначенные для базы данных управляемого экземпляра SQL Azure:

  ![Проект базы данных SQL MI](../media/ssma-newproject-sqldbmi.png)

* После преобразования **advisor исправление**. Дополнительные сведения об этом [здесь](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Выбор предварительной базы данных или схемы.

  При подключении к источнику, пользователь теперь может выбрать баз данных и схем, интерес. Выбор только схемы, которые планируется перенести позволяет сэкономить время, во время начального подключения и повысить общую производительность SSMA.

  ![Объекты фильтра SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

В выпуске v7.10 SSMA для SAP ASE дополнено целевых исправлений, обеспечивает дополнительную безопасность и защиту конфиденциальности в соответствии с изменения в глобальным требованиям.

## <a name="ssma-v79"></a>SSMA v7.9

В выпуске v7.9 SSMA для SAP ASE содержит следующие изменения:

* Целевых исправлений, повышающих качество и преобразования метрики.
* Поддержка в SSMA командной строки, чтобы изменить сопоставление типов данных и настройки проекта.
* Поддержка переноса данных с помощью SQL Server Integration Services (SSIS). После преобразования схемы, можно создать пакет служб SSIS с помощью контекстного меню.
* Диалоговое окно подключения базы данных SQL Azure в SSMA также был изменен, чтобы указать полное имя сервера. В предыдущих версиях SSMA пришлось явно указаны в параметрах проектов префикс базы данных SQL Azure.

## <a name="ssma-v78"></a>SSMA v7.8

В выпуске v7.8 SSMA для SAP ASE содержит следующие изменения:

* Изменить сопоставление типов, выделенным в параметрах проекта.
* Возможности для пользователей отключить сбор данных телеметрии.

## <a name="ssma-v77"></a>SSMA v7.7

В выпуске v7.7 SSMA для SAP ASE содержит следующие изменения:

* SSMA для SAP ASE была улучшена с помощью целевых исправлений, повышающих качество и преобразования метрики.
* В зависимости от спроса популярных 32-разрядная версия SSMA для SAP ASE — обратно. По сравнению с предыдущей реализации (перед для v7.4), существует два пакета установщика, но их нельзя устанавливать параллельно. Таким образом необходимо выбрать наиболее подходящий версию для компонентов подключения что у вас есть. Всегда предпочтительнее использовать 64-разрядной версии, если это возможно.

## <a name="ssma-v76"></a>SSMA v7.6

В выпуске v7.6 SSMA для SAP ASE содержит следующие изменения:

* Целевых исправлений, повышающих качество и преобразования метрик и поддержка SQL Server 2017 (Предварительная версия). Поддержка SQL Server 2017 в Windows и Linux в общедоступной предварительной версии и не должны использоваться для миграции в рабочей среде.
* Поддержка преобразования функций Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

В выпуске версии 7.5 SSMA для SAP ASE (прежнее название — SSMA для Sybase) содержит следующие изменения:

* Несколько улучшений, чтобы обеспечить большую доступность для людей с ограниченными возможностями.
* Поддержка синтаксиса CREATE или REPLACE.

## <a name="ssma-v74"></a>SSMA v7.4

В выпуске v7.4 SSMA для Sybase содержит следующие изменения:

* **Время ожидания запроса** теперь доступен при обнаружении объекта схемы в исходной и целевой.

  ![параметр времени ожидания запроса](../media/query-timeout_red.png)
* Показатель качества и преобразования был улучшен с помощью целевых исправлений, на основании отзывов пользователей.

  > [!IMPORTANT]
  > .NET 4.5.2 является необходимым условием для установки SSMA v7.4. Кроме того начиная с v7.4, 32-разрядной версии SSMA прекращается.  

## <a name="ssma-v73"></a>SSMA v7.3

В выпуске v7.3 SSMA для Sybase содержит следующие изменения:

* Улучшенное качество и преобразования метрики с целевых исправлений, на основании отзывов пользователей.
* Инфраструктура расширяемости SSMA, предоставляемые через следующие элементы:
  * Экспорт функций в проект SQL Server Data Tools (SSDT).
    * Теперь можно экспортировать скрипты схемы из SSMA для проекта SSDT. Скрипты схемы можно использовать для внесения изменений дополнительные схемы и развертывания базы данных.

        ![Сохранить как команда проекта SSDT](../media/export-schema-scripts_red.png)
  * Библиотеки, которые могут быть использованы SSMA для выполнения пользовательских преобразований.
    * Можно создавать код, который может обрабатывать пользовательский синтаксис преобразования и преобразования, которые не были устранены ранее SSMA.
      * Инструкции о том, как создать пользовательский преобразователь доступны в записи блога [расширение SQL Server Migration Assistant возможности преобразования](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Скачайте пример проекта для преобразования из этого [блога](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

В выпуске v7.2 SSMA для Sybase содержит следующие изменения:

* Улучшенное качество и преобразования метрики с целевых исправлений, на основании отзывов пользователей.
* Усовершенствования телеметрии для предоставления более точек данных для устранения неполадок клиента и повышения коэффициента преобразования в SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

В выпуске версии 7.1 SSMA для Sybase содержит следующие изменения:

* SQL Server 2017 в Windows и Linux CTP-версия 1 теперь является поддерживаемой целевой платформы для миграции. Эта функция доступна в предварительной технической версии и поддерживает перемещение схему и данные к целевым серверам SQL.
* Поддержка автоматического обновления скачать последнюю версию SSMA, как только он доступен.
* SSMA устанавливаемых двоичных файлов теперь доставляются через файлы пакета установщика Windows (.msi).

## <a name="may-2016"></a>Май 2016 г.

Май 2016 г. выпуск SSMA для Sybase содержит следующие изменения:  

* Добавлена поддержка SQL Server 2016.
* Удалена проверка установщика для .net 2.0.
* Обновленный пакет расширений зависимость от .net 3.5 в .net 4.0.
* Исправлена «сохранить проект» и «открыть проект» команд консоли SSMA.
* Исправлена команда «securepassword» для команд консоли SSMA.
* Исправлена подсчет объектов для начальной загрузки.
* Исправлена ошибка в глобальных параметрах.

## <a name="march-2016"></a>Март 2016 г.

Март 2016 г. Предварительный выпуск SSMA для Sybase добавляет поддержку для миграции на SQL Server 2016.  
  
## <a name="january-2016"></a>Январь 2016 г.

Выпуск за январь 2016 обслуживания SSMA для Sybase содержит следующие изменения.  
  
* Пункт меню добавлены представления журнала в SSMA (RFC 5706203).  
* Добавлена Телеметрия.

## <a name="july-2014"></a>Июль 2014 г.

Июль 2014 г. выпуск SSMA для Sybase содержит следующие изменения:  
  
* Улучшенные преобразования кода базы данных SQL Azure.  
* Расширение функциональности пакета переместить схему для поддержки базы данных SQL Azure.  
* Для баз данных с более чем 10k добавлена производительность проверки объектов.  
* Добавлены улучшения пользовательского интерфейса для работы с большим числом объектов.  
* Добавлена возможность выделения «хорошо известным» схемы LOB (поэтому они могут быть пропущены при преобразовании).  
* Добавить увеличение скорости преобразования.  
* Добавлена возможность отображения счетчиков объектов в пользовательском Интерфейсе.
* Размер ограниченной отчета на более чем 25%.  
* Улучшенные сообщения об ошибках для непроанализированной конструкций.  
  
## <a name="april-2014"></a>Апрель 2014 г.

В выпуске за апрель 2014 SSMA для Sybase содержит следующие изменения:  
  
* Добавлена поддержка MS SQL Server 2014.  
* Исправленные ошибки относительно преобразование в Azure.  
* Исправленные ошибки относительно страницы невидимым отчетов в Internet Explorer 10.  
  
## <a name="january-2012"></a>Январь 2012 г.

Январь 2012 г. выпуск SSMA для Sybase содержит следующие изменения:  
  
* Добавлена поддержка для преобразования триггера отката.
* Указанное исправление для преобразования@ROWCOUNT и @@ERROR в той же инструкции SET.  
  
## <a name="july-2011"></a>Июль 2011 г.

В выпуске от июля 2011 SSMA для Sybase предоставляет улучшены сообщения об ошибках во время переноса данных.  
  
## <a name="april-2011"></a>Апреля 2011 г.

В выпуске апреля 2011 г. SSMA для Sybase содержит следующие изменения:  
  
* Консолидированные продукта «SSMA для Sybase», которая поддерживает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] «Denali» и Azure SQL.  
* Добавлена поддержка для подключения и переход на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] «Denali».  
* Добавлена новая возможность, преобразование и миграцию баз данных Sybase в Azure SQL.  
* Модуль миграции расширенных данных на стороне клиента с поддержкой параллельной миграции данных.  
* Улучшение миграции производительности данных с простой и массового войти в модели восстановления.
* Добавлена возможность правильно преобразовать и перенести с учетом регистра баз данных Sybase в SQL Server, с учетом регистра.  
* Добавлена поддержка для преобразования из Sybase ASE не совместимые с ANSI операторы join для инструкций соединения SQL Server ANSI была расширена для удаления и обновления инструкций.  
* Предоставляются дополнительные возможности подключения параметры для подключения к серверам Sybase ASE с помощью поставщика ODBC для Sybase ASE и поставщиков Sybase ASE ADO.Net.
* Удалена зависимость от отдельных базу данных с именем **SysDB**, который содержит Sybase эмуляции функции (устанавливается как часть пакета расширения).
* Добавлена возможность установить SSMA для Sybase Extension Pack на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] кластеров.
* Добавлена обратная совместимость проектов, созданных в более ранних версиях SSMA (версии 4.0 и версия 4.2).  
* Добавлена возможность установить SSMA для Sybase версии 5.0 продукта side-by-side (SxS) с более старыми версиями SSMA (версии 4.0 и версия 4.2).  
  
## <a name="july-2010"></a>Июль 2010 г.

Июль 2010 г. выпуск SSMA для Sybase добавлен:

* Поддержка перехода на SQL Server 2008 R2.  
* Новое приложение консоли SSMA для выполнения командной строки.  
* Поддержка переноса данных с помощью подсистемы миграции данных на стороне клиента и на стороне сервера.  
* Поддержка для инструкции «SELECT Custom» переноса данных.  
* Поддержка перехода с Sybase ASE 15.0.3 и 15.5.  
  
## <a name="june-2008"></a>Июнь 2008 г.

Июнь 2008 г. выпуск SSMA для Sybase содержит следующие изменения:  
  
* Добавлена SSMA тест-инженер, которой автоматически проверяет преобразования объекта базы данных и переноса данных, произведенные SSMA. После завершения всех шагов миграции SSMA позволяет убедиться, что преобразованные объекты работают так же, как и все данные было передано надлежащим образом тест-инженер SSMA.
* Добавлено преобразование до версии SQL. Теперь пользователь может указать временной таблицы (и другим объектом) объявления для каждого источника процедуру, используемую при преобразовании.
* Добавлены усовершенствования в преобразовании объекта:  
  * Присоединяет пересмотра преобразования.  
  * Статистические выражения и на нестатистические без необходимости/группа предложениями.  
  * Функцию IDENTITY с инструкцией SELECT INTO.  
  * Кластеризованного ограничения и индексы в данных только для блокировки.  
  * Временные таблицы, созданные SELECT INTO.  
  * Ограничения и индексы для временных таблиц.  
  * Новый [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживаются 2008 типы даты и времени.  
  * Поддержка возможности подключения и типов данных Sybase 15.0.  
  
## <a name="may-2007"></a>Мая 2007 г.

Мая 2007 г. выпуск SSMA для Sybase добавлен:  
  
* Возможность быстрее загружать содержимое базы данных при сохранении проекта.  
* Поддержка комментариев, введенный пользователем, в SQL Server в формате режим SQL.  
* Улучшения в объект преобразования.  

## <a name="november-2006"></a>Ноябрь 2006 г.

В выпуске за ноябрь 2006 г. SSMA для Sybase содержит следующие изменения:  
  
* Добавлены новые глобальные параметры:  
  * Вы можете выбрать для отображения номеров строк в окнах редактора.  
  * Можно настроить SSMA для запроса для замены дубликатов объектов или всегда или никогда не заменить повторяющиеся объекты во время преобразования схемы.  
* Добавлен новый параметр преобразования, который позволяет настроить SSMA обработку следующих ситуациях:  
  * Оператор CAST или CONVERT, содержащее двоичную строку.  
  * Проверяет наличие значений null в выражениях равенства.  
  * Таблицы прокси-сервера.  
  * Номера ошибок пользователя сообщения для инструкции RAISERROR.  
  * Инструкции UPDATE, которые содержат неразрешенные идентификаторы.  
* Добавлен новый параметр миграции, который позволяет указать порядок обработки дат, которые находятся за пределами SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] диапазон дат.  
* Добавлен **в формате SQL** на **SQL** вкладки, которая форматирует код для улучшения читаемости кода.  
* Исправления ошибок, включая:
  * SSMA теперь преобразует БЛОКИРОВКИ таблицы *таблицы* IN {SHARED | ЭКСКЛЮЗИВНЫЕ} инструкции режиме, добавив подсказку TABLOCK или TABLOCKX последующего запроса SELECT для таблицы.  
  * Необходимые приведения добавляются при использовании двоичных типов в символьных выражений.  
  * Память и производительность приложений.  
  
## <a name="july-2006"></a>Июль 2006 г.

Первый выпуск SSMA для СУБД Sybase был в июле 2006 г.  
  
## <a name="see-also"></a>См. также

[Начало работы с SSMA для Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
