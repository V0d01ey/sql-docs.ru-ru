---
title: Определения ролей — стандартные роли | Документация Майкрософт
ms.date: 05/24/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], defaults
- default security
- role-based security [Reporting Services], defaults
ms.assetid: 6b46db51-7c30-467d-a251-50f50647fe21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: edb599f3ae735ddc07755f73499a3e71d0c20746
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66270242"
---
# <a name="role-definitions---predefined-roles"></a>Определения ролей — стандартные роли
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] устанавливаются с набором стандартных ролей, которые можно использовать для предоставления доступа к операциям сервера отчетов. Каждой стандартной ролью описывается набор взаимосвязанных задач. Можно назначить учетные записи групп и пользователей для стандартных ролей, чтобы обеспечить немедленный доступ к операциям сервера отчетов.  
  
## <a name="how-to-use-predefined-roles"></a>Как использовать стандартные роли  
  
1. Ознакомьтесь со списком стандартных ролей и определите, допустимо ли использовать их без изменений. Если необходимо изменить набор задач для ролей или определить дополнительные роли, это следует сделать до назначения пользователям каких-либо ролей.  
  
2. Выясните, каким пользователям и группам требуется доступ к серверу отчетов и на каком уровне. Большинству пользователей следует назначить роль **Браузер** или роль **Построитель отчетов** . Меньшему числу пользователей следует назначить роль **Издатель** . В роль **Диспетчер содержимого**должно быть включено весьма небольшое число пользователей.  

3. Назначить определенные роли учетным записям пользователей и групп можно на веб-портале. Дополнительные сведения см. в статье [Предоставление пользователям доступа к серверу отчетов](../../reporting-services/security/grant-user-access-to-a-report-server.md).  
  
##  <a name="bkmk_rolelist"></a> Определения стандартных ролей  
 Стандартные роли определяются задачами, которые ими поддерживаются. Эти роли можно изменить или заменить их пользовательскими ролями.  
  
 *Область* определяет границы, в пределах которых используются роли. Ролями на уровне элементов обеспечиваются различные уровни доступа к элементам сервера отчетов и операциям, выполняемым с этими элементами. Роли на уровне элементов определяются в корневом узле (Home) и во всех элементах иерархии папок сервера отчетов. Ролями на уровне системы регламентируется доступ на уровне веб-сайта. Роли на уровне элементов и на уровне системы являются взаимоисключающими, однако используются совместно, чтобы обеспечить возможность гибкой настройки разрешений для содержимого и операций сервера отчетов.  
  
 В следующей таблице описаны стандартные области для ролей:  
  
|Стандартная роль|Область|Описание|  
|---------------------|-----------|-----------------|  
|[Роль «Диспетчер содержимого»](#bkmk_content)|Элемент|Позволяет управлять содержимым сервера отчетов, в том числе папками, отчетами и ресурсами.|  
|[Роль «Издатель»](#bkmk_publisher)|Элемент|Позволяет публиковать отчеты и связанные отчеты на сервере отчетов.|  
|[Роль «Браузер»](#bkmk_browser)|Элемент|Позволяет просматривать папки, отчеты и подписки на отчеты.|  
|[Роль «Построитель отчетов»](#bkmk_reportbuilder)|Элемент|Позволяет просматривать определения отчетов.|  
|[Роль «Мои отчеты»](#bkmk_myreports)|Элемент|Позволяет публиковать отчеты и связанные отчеты, управлять папками, отчетами и ресурсами в папке пользователя "Мои отчеты".|  
|[Роль «Системный администратор»](#bkmk_systemadministrator)|Система|Просмотр и изменение назначений системных ролей, определений системных ролей, свойств системы и общих расписаний, а также возможность создания определений ролей и управления заданиями в среде Management Studio.|  
|[Роль «Пользователь системы»](#bkmk_systemuser)|Система|Просмотр системных свойств, общих расписаний, предоставление разрешения на использование построителя отчетов или других клиентов, выполняющих определения отчетов.|  
  
##  <a name="bkmk_content"></a> Роль "Диспетчер содержимого"  
 Роль **Диспетчер содержимого** — это стандартная роль, предусматривающая задания для пользователя, который может управлять отчетами и веб-содержимым, но не являться автором отчетов или администратором веб-сервера либо экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Диспетчер содержимого разворачивает отчеты, управляет моделями отчетов и соединениями с источниками данных, а также принимает решения о способе использования отчетов. Для определения роли **Диспетчер содержимого** по умолчанию выбраны все задачи уровня элемента.  
  
 Роль **Диспетчер содержимого** часто используется вместе с ролью **Системный администратор** . Вместе определения этих двух ролей обеспечивают полный набор задач для пользователей, которым требуется полный доступ ко всем элементам на сервере отчетов. Хотя роль **Диспетчер содержимого** обеспечивает полный доступ к отчетам, моделям отчетов, папкам и другим элементам в иерархии папок, она не дает доступа к элементам или операциям на уровне сайта. Такие задачи, как создание общих расписаний и управление ими, настройка свойств сервера и управление определениями ролей, являются задачами системного уровня, которые включены в роль **Системный администратор** . По этой причине рекомендуется создавать второе назначение роли на уровне сайта, которое обеспечит доступ к общим расписаниям.  
  
### <a name="content-manager-tasks"></a>Задачи диспетчера содержимого  
 В следующей таблице перечислены задачи роли **Диспетчер содержимого**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Использование отчетов|Считывание определений отчетов.|  
|Создание связанных отчетов|Создание связанных отчетов, основанных на несвязанном отчете.|  
|Управление всеми подписками|Просмотр, изменение и удаление любой подписки для отчетов и связанных отчетов, независимо от владельца подписки. Эта задача также поддерживает создание управляемых данными подписок.|  
|Управление источниками данных|Создание и удаление общих элементов источника данных, просмотр и изменение свойств и содержимого источника данных.|  
|Управление папками|Создание, просмотр и удаление папок; просмотр и изменение их свойств.|  
|Управление моделями|Создание, просмотр и удаление моделей, а также просмотр и изменение свойств моделей.|  
|Управление отдельными подписками|Создание, просмотр и удаление принадлежащих пользователям подписок на отчеты и связанные отчеты.|  
|Управление журналом отчета|Создание, просмотр и удаление журнала отчетов, просмотр свойств журнала отчетов, просмотр и изменение параметров, определяющих ограничения журнала моментальных снимков и характер выполнения кэширования.|  
|Управление отчетами|Добавление и удаление отчетов, изменение параметров отчетов, просмотр и изменение свойств отчетов, просмотр и изменение источников данных, предоставляющих содержимое отчетам, просмотр и изменение определений отчетов, а также установка политики безопасности на уровне отчета.|  
|Управление ресурсами|Создание, изменение и удаление ресурсов; просмотр и изменение их свойств.|  
|Установка политики безопасности для элементов|Определение политики безопасности для отчетов, связанных отчетов, папок, ресурсов и источников данных. Дополнительные сведения см. в разделе [Защищаемые элементы](../../reporting-services/security/securable-items.md).|  
|Просмотр источников данных|Просмотр общих элементов источника данных в иерархии папок.|  
|Просмотр отчетов|Выполнение отчетов и просмотр их свойств.|  
|Просмотр моделей|Просмотр моделей в иерархии папок, использование моделей как источников данных для отчета и выполнение запросов по модели для получения данных.|  
|Просмотр ресурсов|Просмотр ресурсов и их свойств.|  
|Просмотр папок|Просмотр содержимого папок и навигация по иерархии папок.|  
  
### <a name="customizing-the-content-manager-role"></a>Настройка роли "Диспетчер содержимого"  
 Данная роль предназначена для доверенных пользователей, обладающих общей ответственностью за управление и обслуживание содержимого сервера отчетов. Из определения данной роли можно удалять задачи, но это может внести неоднозначность в процесс управления. Например, удаление задачи «Просмотр отчетов» из определения этой роли не позволит **диспетчеру содержимого** просматривать содержимое отчетов и, следовательно, он не сможет проверять изменения настроек параметров и учетных данных.  
  
 Роль **Диспетчер содержимого** используется в настройках безопасности по умолчанию.  
  
##  <a name="bkmk_publisher"></a> Роль "Издатель"  
 Роль **Издатель** — это встроенное определение роли, содержащее задачи, позволяющие пользователям добавлять содержимое на сервер отчетов. Эта роль предопределена для удобства. Она не используется, пока не создано включающее ее назначение ролей. Эта роль предназначена для пользователей, создающих отчеты или модели в конструкторе отчетов или моделей и публикующих их на сервере отчетов.  
  
> [!CAUTION]  
> Разрешение на публикацию отчетов на сервере отчетов следует предоставлять только доверенным пользователям. Роль «Издатель» предоставляет широкие права, позволяющие пользователям передавать на сервер отчетов файлы любого типа. Если переданный отчет или HTML-файл содержит вредоносный скрипт, любой пользователь, щелкнув отчет или HTML-документ, запустит этот скрипт со своими учетными данными.  
  
 Определения отчетов могут включать скрипты и другие элементы, уязвимые для атак в момент преобразования отчета в формат HTML в процессе выполнения. Если опубликованный отчет содержит вредоносный скрипт, каждый пользователь, запускающий отчет, непреднамеренно вызовет выполнение этого скрипта при открытии отчета. Если пользователь обладает повышенными разрешениями, скрипт будет выполняться с этими разрешениями.  
  
 Для снижения опасности того, что пользователи непреднамеренно запустят вредоносный скрипт, следует ограничить число пользователей, имеющих разрешение на публикацию содержимого, и убедиться, что пользователи опубликовали только документы и отчеты, полученные из надежных источников. Если нет уверенности в безопасности публикации отчета, откройте файл определения отчета в текстовом редакторе и поищите в нем теги скриптов. Вредоносный скрипт может быть скрыт в выражениях и URL-адресах (например, в URL-адресе действия, связанного с перемещением).  
  
### <a name="publisher-tasks"></a>Задачи роли "Издатель"  
 В следующей таблице приведены задачи роли **Издатель**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Создание связанных отчетов|Создание связанных отчетов и их публикация в папке сервера отчетов.|  
|Управление источниками данных|Создание и удаление общих элементов источника данных, просмотр и изменение свойств и содержимого источника данных.|  
|Управление папками|Создание, просмотр и удаление папок; просмотр и изменение их свойств.|  
|Управление отчетами|Добавление и удаление отчетов, изменение параметров отчетов, просмотр и изменение свойств отчетов, просмотр и изменение источников данных, предоставляющих содержимое для отчетов, просмотр и изменение определений отчетов.|  
|Управление моделями|Создание, просмотр и удаление моделей отчетов; просмотр и изменение свойств моделей.|  
|Управление ресурсами|Создание, просмотр и удаление ресурсов; просмотр и изменение их свойств.|  
  
### <a name="customizing-the-publisher-role"></a>Настройка роли "Издатель"  
 Роль **Издатель** можно изменять в соответствии со своими потребностями. Например, можно удалить задачу «Создание связанных отчетов», если нужно, чтобы пользователи не могли создавать и публиковать связанные отчеты, или добавить задачу «Просмотр папок», чтобы пользователи могли перемещаться по иерархии папок при выборе размещения нового элемента.  
  
 Пользователям, публикующим отчеты в конструкторе отчетов, как минимум необходима задача «Управление отчетами», позволяющая добавлять отчет на сервер отчетов. Если пользователь должен публиковать отчеты, использующие общие источники данных или внешние файлы, следует также добавить задачи «Управление источниками данных» и «Управление ресурсами». Если пользователю необходима возможность создания папки в процессе публикации, следует добавить «Управление папками».  
  
##  <a name="bkmk_browser"></a> Роль "Браузер"  
 Роль **Браузер** — это стандартная роль, включающая задачи, необходимые для пользователя, который просматривает отчеты, но не обязательно их создает или изменяет. Эта роль обеспечивает основные возможности прямого использования сервера отчетов, так как без выполнения этих задач пользователям было бы трудно пользоваться сервером отчетов.  
  
 Роль **Браузер** должна использоваться вместе с ролью **Системный пользователь** . Вместе определения этих двух ролей обеспечивают полный набор задач для пользователей, которые взаимодействуют с элементами на сервере отчетов. Хотя роль **Браузер** предоставляет доступ для просмотра отчетов, моделей отчетов, папок и других элементов в иерархии папок, она не обеспечивает доступ к элементам уровня сайта, таким как общие расписания, которые полезны при создании подписок. По этой причине рекомендуется создавать второе назначение роли на уровне сайта, которое обеспечит доступ к общим расписаниям.  
  
### <a name="browser-tasks"></a>Задачи роли "Браузер"  
 В следующей таблице описаны задачи роли **Браузер**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Просмотр отчетов|Запуск отчета и просмотр его свойств.|  
|Просмотр ресурсов|Просмотр ресурсов и их свойств.|  
|Просмотр папок|Просмотр содержимого папки и перемещение по иерархии папок.|  
|Просмотр моделей|Просмотр моделей в иерархии папок, использование моделей как источников данных для отчета и выполнение запросов по модели для получения данных.|  
|Управление отдельными подписками|Создание, просмотр, изменение и удаление принадлежащих пользователю подписок на отчеты и связанные отчеты, а также создание расписаний для поддержки этих подписок.|  
  
### <a name="customizing-the-browser-role"></a>Настройка роли "Браузер"  
 Роль **Браузер** можно изменить в соответствии с имеющимися потребностями. Например, можно удалить задачу «Управление отдельными подписками», если не нужно поддерживать подписки или задачу «Просмотр ресурсов», если нежелательно, чтобы пользователи видели дополнительную документацию или другие элементы, которые могут быть переданы на сервер отчетов.  
  
 Как минимум, эта роль должна поддерживать задачи «Просмотр отчетов» и «Просмотр папок», чтобы обеспечить просмотр и перемещение между папками. Задачу «Просмотр папок» не следует удалять, если не ставится цель запретить пользователю перемещение между папками. Подобным же образом, не следует удалять задачу «Просмотр папок», если не ставится цель предотвратить просмотр пользователями отчетов. Эти виды изменений предполагают определение пользовательской роли, применяемой выборочно к особой группе пользователей.  
  
##  <a name="bkmk_reportbuilder"></a> Роль "Построитель отчетов"  
 Роль **Построитель отчетов** — это стандартная роль, включающая задачи загрузки отчетов в построитель отчетов, их просмотра и навигации по иерархии папок. Для создания и изменения отчетов в построителе отчетов пользователь должен также относиться к системной роли, включающей задачу «Выполнение определений отчетов», что необходимо для локальной обработки отчетов в построителе отчетов.  
  
### <a name="report-builder-tasks"></a>Задачи построителя отчетов  
 В следующей таблице описаны задачи роли **Построитель отчетов**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Использование отчетов|Считывание определений отчетов.|  
|Просмотр отчетов|Запуск отчета и просмотр его свойств.|  
|Просмотр ресурсов|Просмотр ресурсов и их свойств.|  
|Просмотр папок|Просмотр содержимого папки и перемещение по иерархии папок.|  
|Просмотр моделей|Просмотр моделей в иерархии папок, использование моделей как источников данных для отчета и выполнение запросов по модели для получения данных.|  
|Управление отдельными подписками|Создание, просмотр, изменение и удаление принадлежащих пользователю подписок на отчеты и связанные отчеты, а также создание расписаний для поддержки этих подписок.|  
  
### <a name="customizing-the-report-builder-role"></a>Настройка роли "Построитель отчетов"  
 Роль **Построитель отчетов** можно изменить в соответствии со своими потребностями. Общие рекомендации при этом будут практически такими же, что для роли **Browser** : удалите задачу «Управление отдельными подписками», если не нужна поддержка подписок, удалите задачу «Просмотр ресурсов», если не нужно, чтобы пользователи могли просматривать ресурсы, и сохраните задачи «Просмотр отчетов» и «Просмотр папок» для поддержки просмотра отчетов и навигации по иерархии папок.  
  
 Самой важной в определении этой роли является задача «Использование отчетов», которая позволяет пользователю загрузить определение отчета из сервера отчетов в локальный экземпляр построителя отчетов. Если поддержка данной задачи не нужна, то можно удалить это определение роли и воспользоваться ролью **Браузер** , поддерживающей обычный доступ к серверу отчетов.  
  
##  <a name="bkmk_myreports"></a> Роль "Мои отчеты"  
 Стандартная роль **Мои отчеты** включает в себя набор задач, полезных для пользователей, использующих возможность «Мои отчеты». Это определение роли включает в себя задачи, предоставляющие пользователям административные разрешения на папку «Мои отчеты», которой они владеют.  
  
 Хотя можно избрать другую роль для использования возможности «Мои отчеты», рекомендуется выбирать ту, которая будет использоваться только для безопасности «Моих отчетов». Дополнительные сведения см. в разделе [Обеспечение безопасности "Моих отчетов"](../../reporting-services/security/secure-my-reports.md).  
                          
### <a name="my-reports-tasks"></a>Задачи роли "Мои отчеты"  
 Следующая таблица содержит задачи роли **Мои отчеты**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Создание связанных отчетов|Создание связанных отчетов, основанных на отчетах, сохраненных в папке пользователя «Мои отчеты».|  
|Управление папками|Создание, просмотр и удаление папок; просмотр и изменение их свойств.|  
|Управление источниками данных|Создание и удаление общих элементов источника данных, просмотр и изменение свойств и содержимого источника данных.|  
|Управление отдельными подписками|Создание, просмотр, изменение и удаление подписок для отчетов и связанных отчетов.|  
|Управление отчетами|Добавление и удаление отчетов, изменение параметров отчетов, просмотр и изменение свойств отчетов, просмотр и изменение источников данных, предоставляющих содержимое для отчетов, просмотр и изменение определений отчетов, а также установка политики безопасности на уровне отчета.|  
|Управление ресурсами|Создание, изменение и удаление ресурсов, а также просмотр и изменение свойств ресурсов.|  
|Просмотр отчетов|Запуск отчетов, сохраненных в папке пользователя «Мои отчеты», и просмотр свойств отчетов.|  
|Просмотр источников данных|Просмотр общих элементов источника данных в иерархии папок.|  
|Просмотр ресурсов|Просмотр ресурсов и их свойств.|  
|Просмотр папок|Просмотр содержимого папок.|  
  
### <a name="customizing-the-my-reports-role"></a>Настройка роли "Мои отчеты"  
 Можно изменять эту роль, чтобы она соответствовала текущим нуждам. Однако рекомендуется сохранить задачи «Управление отчетами» и «Управление папками», чтобы позволить управлять основным содержимым. В дополнение эта роль должна поддерживать все основанные на представлениях задачи, чтобы пользователи могли видеть содержимое папок и запускать управляемые ими отчеты.  
  
 Хотя задача «Установка политики безопасности для элементов» не является частью определения роли по умолчанию, можно добавить эту задачу к роли **Мои отчеты** , чтобы пользователи могли изменять настройки безопасности для вложенных папок и отчетов.  
  
##  <a name="bkmk_systemadministrator"></a> Роль "Системный администратор"  
 Роль **Системный администратор** является стандартной ролью, которая включает задачи, необходимые администратору сервера отчетов, отвечающему за сервер отчетов в целом, но необязательно за его содержимое.  
  
 Чтобы создать назначение роли, включающее эту роль, воспользуйтесь страницей "Параметры сайта" на веб-портале или командами, появляющимися при правом щелчке мышью узла сервера отчетов в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Роль **Администратор системы** не передает тот же самый полный набор разрешений, которым должен обладать локальный администратор компьютера. Скорее, роль **Администратор системы** включает операции, которые выполняются на уровне веб-сайта, а не элемента. Для пользователей, которым необходим доступ к операциям уровня веб-сайта и элементам, хранимым на сервере отчетов, создайте второе назначение ролей на корневую папку, включающее роль **Диспетчер содержимого** . Вместе определения этих двух ролей обеспечивают полный набор задач для пользователей, которым требуется полный доступ ко всем элементам на сервере отчетов.  
  
### <a name="system-administrator-tasks"></a>Задачи роли "Системный администратор"  
 В следующей таблице приводится список задач роли **Системный администратор**:  
  
|Задача|Описание|  
|----------|-----------------|  
|Выполнение определений отчета|Запуск выполнения определения отчета без публикации на сервере отчетов.|  
|Управление заданиями|Просмотр и отмена работающих заданий. Дополнительные сведения см. в разделе [Управление запущенным процессом](../../reporting-services/subscriptions/manage-a-running-process.md).|  
|Управление свойствами сервера отчетов|Просмотр и изменение свойств, относящихся к серверу отчетов и к элементам, которыми управляет сервер отчетов.<br /><br /> Эта задача позволяет переименовывать веб-портал, включать "Мои отчеты" и устанавливать настройки журнала отчета по умолчанию.|  
|Управление ролями|Создание, просмотр, изменение и удаление определений ролей.<br /><br /> Члены роли **Системный администратор** могут управлять ролями через страницу «Настройки сайта».|  
|Управление общими расписаниями|Создание, просмотр, изменение и удаление общих расписаний, используемых для выполнения или обновления отчетов.|  
|Управление безопасностью сервера отчетов|Просмотр и изменение назначений ролей в масштабе системы|  
  
 Роль **Системный администратор** используется в настройках безопасности по умолчанию.  
  
##  <a name="bkmk_systemuser"></a> Роль "Пользователь системы"  
**Пользователь системы** — это стандартная роль, которая содержит задачи, позволяющие пользователям просматривать основные сведения о сервере отчетов. Кроме того, эта роль поддерживает выгрузку отчетов в построитель отчетов. Построитель отчетов — это клиентское приложение, которое может обрабатывать отчеты независимо от сервера отчетов. Задача «Выполнение определений отчета» предназначена для использования в построителе отчетов. Если построитель отчетов не используется, то эту задачу можно удалить из роли **System User** .  

В следующей таблице перечислены задачи, включенные в определение роли **Пользователь системы**:  
  
### <a name="system-user-tasks"></a>Задачи роли "Пользователь системы"  
  
|Задача|Описание|  
|----------|-----------------|  
|Выполнение определений отчета|Запуск отчета без публикации на сервере отчетов.|  
|Просмотр свойств сервера отчетов|Просмотр таких свойств сервера отчетов, как имя приложения, состояние параметра "Мои отчеты", а также параметров по умолчанию для журнала отчета.<br /><br /> При удалении этой задачи из роли **System User** страница «Настройки сайта» становится недоступной. Кроме того, заголовок приложения в верхней части каждой страницы отображаться не будет. По умолчанию для веб-портала используется заголовок "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]".|  
|Просмотр общих расписаний|Просмотр общих расписаний, по которым запускаются отчеты или их обновления.<br /><br /> Если эта задача будет удалена из роли **System User** , то пользователи не смогут выбрать общие расписания для использования с подписками и другими операциями расписания.|  
  
 Роль **System User** можно использовать в качестве дополнения к мерам безопасности по умолчанию. Можно включать эту роль в новые назначения ролей, позволяющие пользователям отчетов получить доступ к серверу отчетов. Дополнительные сведения см. в статье [Предоставление разрешений на сервер отчетов в собственном режиме](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
## <a name="see-also"></a>См. также раздел  
[Создание, удаление и изменение ролей (среда Management Studio)](../../reporting-services/security/role-definitions-create-delete-or-modify.md)  
[Предоставление пользователям доступа к серверу отчетов](../../reporting-services/security/grant-user-access-to-a-report-server.md)  
[Изменение или удаление назначения роли (веб-портал SSRS)](../../reporting-services/security/role-assignments-modify-or-delete.md)  
[Предоставление разрешений на сервер отчетов в собственном режиме](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
[Задачи и разрешения](../../reporting-services/security/tasks-and-permissions.md)
  
