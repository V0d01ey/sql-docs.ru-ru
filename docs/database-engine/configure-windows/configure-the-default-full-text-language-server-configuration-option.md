---
title: Настройка параметра конфигурации сервера "язык полнотекстового поиска по умолчанию" | Документы Майкрософт
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 5b7d8a4cb398e984ede05ad411623a9e33653ac1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803327"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>Настройка параметра конфигурации сервера «язык полнотекстового поиска по умолчанию»
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  В этом разделе описываются способы настройки параметра конфигурации сервера **default full-text language** в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Параметр **default full-text language** предназначен для указания языка по умолчанию для полнотекстовых индексов. Лингвистический анализ выполняется для всех данных с полнотекстовой индексацией и зависит от языка, в котором эти данные представлены. Значением по умолчанию для этого параметра является язык сервера. Для локализованной версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] задает в качестве значения параметра **default full-text language** язык сервера, если для него существует совпадение. Для нелокализованной версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]параметр **default full-text language** по умолчанию имеет значение, соответствующее английскому языку.  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
     [Рекомендации](#Recommendations)  
  
     [безопасность](#Security)  
  
-   **Настройка параметра default full-text language с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Дальнейшие действия.**  [После настройки параметра default full-text language](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Значение параметра **default full-text language** применяется в полнотекстовом индексе в том случае, если язык для столбца не указан в параметре LANGUAGE **language_term** инструкции CREATE FULLTEXT INDEX или ALTER FULLTEXT INDEX. Если установленный по умолчанию язык полнотекстового поиска не поддерживается или отсутствует пакет лингвистического анализа, операция CREATE или ALTER завершится ошибкой, а [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вернет сообщение об указании недопустимого языка.  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Это расширенный параметр, и изменять его следует только опытным администраторам баз данных или сертифицированным по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] специалистам.  
  
-   Параметр **default full-text language** требует значения кода языка. Список поддерживаемых кодов LCID и соответствующих им языков см. в разделе [sys.fulltext_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md). Могут быть доступны также и другие языки, например, от независимых поставщиков программного обеспечения. Если не найден указанный диалект языка, средство полнотекстового поиска автоматически переключается на основной язык.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Разрешения на выполнение хранимой процедуры **sp_configure** без параметров или только с первым параметром по умолчанию предоставляются всем пользователям. Для выполнения процедуры **sp_configure** с обоими параметрами для изменения параметра конфигурации или запуска инструкции RECONFIGURE необходимо иметь разрешение ALTER SETTINGS на уровне сервера. Разрешение ALTER SETTINGS неявным образом предоставлено предопределенным ролям сервера **sysadmin** и **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Настройка параметра default full-text language  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши сервер и выберите пункт **Свойства**.  
  
2.  Щелкните узел **Дополнительно** .  
  
3.  На вкладке "Разное" с помощью параметра **Язык полнотекстового поиска по умолчанию** можно задать значение языка по умолчанию для полнотекстовых индексированных столбцов.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Настройка параметра default full-text language  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере описывается использование хранимой процедуры [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) для присвоения параметру `default full-text` значения "Голландский" (`1043`).  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Дополнительные сведения см. в разделе [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После настройки параметра default full-text language  
 Параметр вступает в силу немедленно, без перезапуска сервера.  
  
## <a name="see-also"></a>См. также:  
 [sys.fulltext_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
