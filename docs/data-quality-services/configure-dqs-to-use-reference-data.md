---
title: Настройка служб DQS для использования эталонных данных | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: ad70828c8b25a9329d5069db204de360900dcb0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802151"
---
# <a name="configure-dqs-to-use-reference-data"></a>Настройка служб DQS для использования справочных данных

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В этом разделе описывается настройка служб [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) на использование ссылочных данных для очистки данных. Можно использовать ссылочные данные как из Windows Azure Marketplace, так и непосредственно от сторонних поставщиков ссылочных данных в сети.  

> [!IMPORTANT]
> В этой статье упоминаются сторонние службы ссылочных данных, которые ранее были доступны из Azure DataMarket. DataMarket и службы Data Services — включая данные об адресах Melissa — не поддерживаются после 31 декабря 2016 г. Таким образом, вы больше не можете запускать примеры в этой статье с помощью указанных служб из DataMarket. По-прежнему можно использовать службы эталонных данных, доступные через Интернет напрямую от сторонних поставщиков.

## <a name="before-you-begin"></a>Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Чтобы использовать ссылочные данные из Marketplace, необходим действительный ключ учетной записи Marketplace. Дополнительные сведения о создании ключа учетной записи Marketplace см. в статье [Создание учетной записи](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936) ). Ключ учетной записи Marketplace также можно создать с помощью [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , выбрав команду **Настройка** в разделе **Администрирование** главной страницы [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , а затем нажав кнопку **Создать идентификатор учетной записи DataMarket** на вкладке **Ссылочные данные** .  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для настройки параметров службы ссылочных данных в DQS необходимо иметь роль dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Marketplace"></a> Настройка служб DQS на использование ссылочных данных из Marketplace  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] в разделе **Администрирование**выберите команду **Настройка**.  
  
3.  На вкладке **Ссылочные данные** в области **Параметры сети** введите соответствующие значения в поля **Прокси-сервер** и **Порт** , если в вашей организации для подключения к Интернету используется прокси-сервер.  
  
4.  Укажите ключ учетной записи Marketplace в поле **Идентификатор учетной записи DataMarket** и щелкните значок **Проверить идентификатор учетной записи DataMarket** , чтобы проверить действительность ключа учетной записи. Отображается сообщение, указывающее, действителен ли заданный ключ учетной записи Marketplace.  
  
 Теперь можно использовать в DQS службы ссылочных данных из Marketplace, на которые подписан указанный ключ учетной записи Marketplace.  
  
##  <a name="ThirdParty"></a> Настройка служб DQS на использование ссылочных данных от сторонних поставщиков ссылочных данных в сети  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] в разделе **Администрирование**выберите команду **Настройка**.  
  
3.  На вкладке **Ссылочные данные** в области **Параметры сети** введите соответствующие значения в поля **Прокси-сервер** и **Порт** , если в вашей организации для подключения к Интернету используется прокси-сервер.  
  
4.  В области **Настройки службы ссылочных данных стороннего поставщика при непосредственном подключении по сети** щелкните значок **Добавить новый поставщик служб ссылочных данных** .  
  
5.  В области **Создать новый сторонний поставщик службы ссылочных данных с непосредственным подключением по сети** укажите следующие данные.  
  
    1.  В поле **Имя** введите имя нового поставщика служб ссылочных данных с прямой ссылкой для подключения.  
  
    2.  (Необязательно.) В поле **Описание** введите описание нового поставщика служб ссылочных данных с прямой ссылкой для подключения.  
  
    3.  В поле **Категория** введите категорию данных, предоставляемых новым поставщиком служб ссылочных данных с прямой ссылкой для подключения.  
  
    4.  В поле «Схема» укажите схему, определяющую строку полей (имен столбцов), которые будут получаться от поставщика служб ссылочных данных с прямой ссылкой для подключения. Имя поля не должно содержать пробелов, а поля должны разделяться запятыми. Например: `FirstName, LastName, City, State`.  
  
    5.  В поле **URI** введите URI нового поставщика служб ссылочных данных с прямой ссылкой для подключения. В службах DQS разрешены только безопасные идентификаторы URI (адрес начинается с "https://").  
  
    6.  В поле **Максимальный размер пакета** введите максимальное число записей в пакете, отправляемом поставщику служб ссылочных данных для очистки. Для действия по очистке можно указать до 100 записей в пакете включительно.  
  
    7.  В поле **Идентификатор учетной записи** введите идентификатор учетной записи подписчика для поставщика служб ссылочных данных.  
  
6.  Нажмите кнопку **ОК** , чтобы сохранить данные и закрыть диалоговое окно **Создать новый сторонний поставщик служб ссылочных данных с непосредственным подключением по сети** . Новый добавленный сторонний поставщик служб ссылочных данных с непосредственным подключением по сети будет доступен в поле **Сетка поставщиков служб ссылочных данных с прямой ссылкой для подключения** в службах DQS.  
  
 Теперь службы ссылочных данных из настроенного стороннего поставщика служб ссылочных данных с непосредственным подключением по сети можно использовать в DQS.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После настройки служб DQS на использование ссылочных данных  
 Теперь необходимо сопоставить требуемые домены базы знаний со ссылочными данными, доступными в только что настроенных поставщиках данных. Для этого см. раздел [Подсоединение обычного или составного домена к эталонным данным](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
  
