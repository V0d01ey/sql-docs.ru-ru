---
title: Часто задаваемые вопросы об ODBC в Linux и macOS | Документы Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aadbf8d0cc850d71626663883587195a8229ada8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785856"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Часто задаваемые вопросы об ODBC в Linux и macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Ниже приведены ответы на вопросы о драйвере ODBC для [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] в Linux и macOS.
  
## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

**Как работают с драйвером существующие приложения ODBC в Linux и macOS?**  
Вы должны быть в состоянии компилировать и запускать приложения ODBC, которые компилировались и запускались в Linux или macOS с использованием других драйверов. 
  
**Какие функции [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] поддерживает эта версия драйвера?**

Драйвер ODBC для Linux и macOS поддерживает все функции сервера в [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], за исключением LocalDB. Дополнительные сведения о поддерживаемых функциях [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] см. в статье [Programming Guidelines](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**Поддерживает ли драйвер проверку подлинности Kerberos?**  
Да. При наличии существующей процедуры настройки среды Kerberos, можно подключиться к серверам с помощью `Trusted_Connection=Yes` DSN или строке параметр соединения. Дополнительные сведения см. в статье [Использование встроенной проверки подлинности](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Какую кодировку Юникода должно использовать приложение?**  
UTF-8 для данных SQL_CHAR и UTF-16 для данных SQL_WCHAR.  

**Существуют ли примеры ODBC, которые я могу скачать и запустить с помощью драйвера, чтобы поэкспериментировать с ним или оценить его?**

Пример см. в статье [Использование существующих примеров MSDN C++ ODBC для драйвера ODBC в Linux](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) . Это также применимо к драйверу ODBC macOS. 

**— Драйвер ODBC в Linux или macOS с открытым исходным кодом?**

Нет, драйверы ODBC в Linux и macOS не продукт с открытым кодом.  

## <a name="see-also"></a>См. также:
[Установка Microsoft ODBC Driver for SQL Server в Linux и macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
