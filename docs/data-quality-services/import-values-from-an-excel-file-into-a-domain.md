---
title: Импорт значений в домен из файла Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: 5c89956fca8f0295a0f78b9f61aa97a35c47684f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776458"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Импорт значений в домен из файла Excel

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В этом разделе описывается, как импортировать значения из файла Excel в домен [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Использование файла Excel для импорта значений домена в приложение [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] позволяет упростить процесс создания набора знаний, экономя время и усилия. Это позволяет пользователям, у которых имеется список допустимых значений данных в файле формата Excel или в текстовом файле, импортировать эти значения в домен. Из файла Microsoft Excel вы можете импортировать значения домена в домен или домены в базу знаний. (Дополнительные сведения об импорте доменов в базу знаний см. в разделе [Импорт доменов из файла Excel при обнаружении набора знаний](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).) Экспорт в файл Excel не поддерживается.  
  
 Импортировать значения данных вы можете двумя способами:  
  
-   Создание нового домена и импорт в него значений из файла Excel. В этом случае в домен добавляются все значения.  
  
-   Импорт значений в существующий, заполненный домен. В этом варианте импортируются только новые значения. Все значения, которые уже существуют, не будут импортированы.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Для импорта доменов из файла Excel, Excel должен быть установлен на компьютере, [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] приложение установлено на, чтобы импортировать значения домена или домен целиком; вам необходимо создать файл Excel со значениями домена (см. в разделе [как Импорт works](#How)); и вам необходимо создать и открыть базу знаний для импорта импортироваться домен.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для импорта значений доменов из файла Excel необходимо иметь роль dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Import"></a> Импорт значений из файла Excel в домен  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] откройте базу знаний в разделе управления доменами.  
  
3.  При добавлении значений к новому домену создайте новый домен с помощью значка **Создать домен** , а затем выберите этот новый домен в списке доменов.  
  
4.  При добавлении значений к существующему домену выберите домен в списке доменов.  
  
5.  Перейдите на вкладку **Значения домена** , щелкните значок **Импорт значений** на панели значков, а затем выберите элемент **Импорт допустимых значений из Excel**.  
  
6.  В диалоговом окне **Импорт значений домена** нажмите кнопку **Обзор**.  
  
7.  В диалоговом окне **Выбор файла** откройте папку, содержащую файл Excel, из которого требуется импортировать значения домена, выберите файл (с расширением .xlsx, .xls или .csv), а затем нажмите кнопку **Открыть**. Файл должен находиться либо на клиентском компьютере, с которого запускается DQS, либо в общей папке, к которой пользователь имеет доступ.  
  
8.  В раскрывающемся списке **Лист** выберите лист, из которого будет осуществляться импорт.  
  
9. Установите флажок **Использовать первую строку в качестве заголовка** , если первая строка в таблице представляет имя домена, а все другие строки представляют допустимые значения домена.  
  
10. Нажмите кнопку **ОК**. Отображается индикатор выполнения, показывающий, сколько значений импортировано успешно, сколько значений не импортировано, и общее количество значений. Для отмены процесса нажмите кнопку **Отмена** .  
  
11. Убедитесь, что в диалоговом окне **Импорт значений домена** отображается сообщение "Импорт завершен". В этом диалоговом окне также содержится информация о количестве успешно импортированных значений и количестве значений, которые импортированы не были. В окне также указано имя файла и путь к файлу, состояние завершения операции, количество успешно импортированных значений, количество неимпортированных значений и общее количество обработанных значений.  
  
12. Применительно к значениям, которые не были импортированы, нажмите кнопку **Журнал**, чтобы открыть диалоговое окно **Импорт значений домена — значения с ошибками** и просмотреть причины сбоев операции импорта. В столбце **Значения с ошибками** указаны значения, которые не удалось импортировать в домен из файла Excel. В столбце **Причина** содержится описание причины ошибки импорта. Нажмите кнопку **Копировать в буфер обмена** , чтобы скопировать таблицу **Значения с ошибками** в буфер обмена, из которого эту таблицу можно будет скопировать в другую программу, например в электронную таблицу Excel или в файл приложения «Блокнот». Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Значения с ошибками** .  
  
13. Нажмите кнопку **ОК** , чтобы завершить операцию импорта и закрыть диалоговое окно. После успешного завершения операции импорта список значений домена на странице **Значения домена** обновляется с учетом вновь импортированных значений. Фильтр изменяется на **Все значения** и устанавливается флажок **Показывать только новые** . Если после операции импорта установлен флажок **Показывать только новые** , отображаются только значения, импортированные из файла Excel.  
  
14. Нажмите кнопку **Готово** , чтобы добавить новые значения в базу знаний.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После импорта значений из файла Excel в домен  
 После импорта значений в домен вы можете выполнить другие задачи по управлению доменами для этого домена, провести обнаружение набора знаний для добавления его в домен или добавить в домен политику сопоставления. Дополнительные сведения см. в разделах [Обнаружение набора знаний](../data-quality-services/perform-knowledge-discovery.md), [Управление доменом](../data-quality-services/managing-a-domain.md) и [Создание политики сопоставления](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Synonyms"></a> Импорт синонимов  
 Синонимы импортируются следующим образом:  
  
-   Во-первых, импортируются все значения, затем устанавливается соединение с синонимами.  
  
-   Если соединение со значениями синонимов установить невозможно, на экране журнала отображается сообщение об ошибке. Возможна ситуация, когда ведущие значения и синонимы из файла импортируются в домен, но не задаются в качестве синонимов.  
  
 Следующие сведения справедливы для процесса установления соединения с синонимами:  
  
-   Если ведущее значение в файле Excel уже существует в домене в качестве синонима другого значения, необходимо задать синонимы вручную (например, в файле Excel значение А должно быть ведущим значением для значения В, но значение домена А отображается в качестве синонима значения С). Кроме того, для задания синонимов вручную после завершения импорта вы можете отменить связь со значениями, которые в настоящее время являются синонимами (например, отменить связь с упомянутыми выше значениями A и C), а затем импортировать файл.  
  
-   Если синоним уже соединен с другим ведущим значением, необходимо задать синонимы вручную.  
  
-   Если по какой-либо причине невозможно подсоединить вручную значения в приложении, эти значения в операции импорта не используются.  
  
##  <a name="How"></a> Как работает Импорт  
 При выполнении этой операции импортируются следующие значения.  
  
 В ходе операции импорта DQS выполняет импорт из файла Excel следующим образом:  
  
-   Импортируются правильные и новые значения. Если одно или несколько из импортируемых значений домена уже существует, эти значения не импортируются.  
  
-   Значение, которое противоречит правилу домена, импортируется как недопустимое значение.  
  
-   Значение не импортируется из файла, если оно не является значением типа данных домена или равно NULL.  
  
-   Значения импортируются в порядке, в котором они следуют в файле.  
  
-   Каждая строка представляет значение домена.  
  
-   Первая строка представляет имена доменов либо первое значение или запись данных, в зависимости от того, установлен ли флажок **Использовать первую строку в качестве заголовка** . Если выбран флажок **Использовать первую строку в качестве заголовка** при использовании XSLX- или XLS-файла, имена столбцов, равные NULL, автоматически преобразуются в имена F*n*, а к именам повторяющихся столбцов добавляется номер.  
  
-   Если отменить операцию импорта до ее завершения, выполняется откат операции, а импорт данных не выполняется.  
  
-   Значения в первом столбце импортируются в домен. Если помимо первого столбца дополнительно заполняются один или несколько столбцов, значения в этих столбцах добавляются в качестве синонимов (см. раздел [Импорт синонимов](#Synonyms)).  
  
    -   Ожидаемый формат — первый столбец содержит ведущие значения, а второй и следующие столбцы — синонимы.  
  
    -   Вы можете импортировать несколько синонимов в одной строке или в разных строках. Например, если требуется импортировать значения NYC и New York City в качестве синонимов значения New York, вы можете импортировать одну строку со значением New York в столбец 1, строку со значением NYC в строку 2 и строку со значением New York City в столбец 3; или можно импортировать одну строку со значением New York в столбец 1, строку со значением NYC в столбец 2, а другую строку со значением New York в столбец 1 и строку со значением New York City в столбец 2. Следует отметить, что если значение New York уже существует в домене, то добавляются только синонимы. В процессе импорта пользователю не выдается сообщение об ошибке, информирующее о том, что значение уже существует. Если первое значение еще не существует, оно будет добавлено в домен.  
  
 К файлу Excel, который используется для импорта, применяются следующие правила:  
  
-   Файл Excel может иметь расширение .xlsx, .xls или .csv. Чтобы импортировать значения домена или весь домен, на компьютере, на котором установлено приложение [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , необходимо установить Microsoft Excel. Поддерживаются Excel 2003 и более поздние версии. При использовании 64-разрядной версии Excel поддерживаются только файлы Excel 2003; файлы Excel 2007 и 2010 не поддерживаются.  
  
-   Файлы Excel с расширением .xlsx не поддерживаются для 64-разрядной версии Excel. При использовании 64-разрядной версии Excel сохраните файл с расширением .xls или .csv, либо вместо данной версии установите 32-разрядную версию Excel.  
  
-   В XLSX- и XLS-файлах тип данных столбца определяется по первым восьми строкам. Если в первых восьми строках содержатся данные с различными типами, используется тип данных столбца string. Если данные в ячейке строки 9 и в ячейках следующих строк не соответствуют этому типу данных, ячейке присваивается значение NULL.  
  
-   В CSV-файле тип данных определяется по преобладающему типу данных в первых восьми строках.  
  
-   Если файл Excel поврежден или представлен в недопустимом формате, операция импорта вызывает ошибку.  
  
  
