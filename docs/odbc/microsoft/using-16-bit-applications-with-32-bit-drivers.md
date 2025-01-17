---
title: Использование 16-разрядных приложений с 32-разрядными драйверами | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209976"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Использование 16-разрядных приложений с 32-разрядными драйверами
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этой функции в новых разработках и запланируйте изменение приложений, которые сейчас ее используют. Вместо этого используйте диспетчер 32-разрядная или 64-разрядных драйверов.  
  
 До тех пор, пока 32-разрядный драйвер не вызывает явно функции Win32 API, создающих потоки, можете запустить 16-разрядных приложений с 32-разрядные драйверы на компьютер с системой Windows. Windows в подсистеме Windows (WOW) запускает приложения в 16-разрядном режиме и разрешает вызовы 16-разрядной операционной системе. Преобразование библиотеки DLL resolve 16-разрядное вызовы из приложения в 32-разрядные драйверы ODBC. 16-разрядных приложений использовать Windows API, и 32-разрядные драйверы используйте Win32 API.  
  
## <a name="architecture"></a>Architecture  
 На следующем рисунке показан как 16-разрядных приложений взаимодействовать с 32-разрядные драйверы. Между 16-разрядного диспетчера драйверов и 32-разрядные драйверы являются универсальными, преобразование библиотеки DLL, которые преобразуют вызовы ODBC 16-разрядное в 32-разрядных вызовы ODBC.  
  
 ![Как 16&#45;взаимодействия разрядных приложений с 32&#45;разрядные драйверы](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Каждый раз, когда это 16-разрядное приложение взаимодействует с 32-разрядный драйвер, 32-разрядного диспетчера драйверов всегда возвращает значение «2.0» как используемая версия ODBC драйвер поддерживает.  
  
## <a name="administration"></a>Администрирование  
 Источники данных для 32-разрядные драйверы можно управлять с помощью администратора источника данных ODBC. Открытие администратора ODBC на компьютерах под управлением Microsoft® Windows® 2000, откройте панель управления Windows, дважды щелкните **Администрирование**, а затем дважды щелкните **источники данных (ODBC)** . На компьютерах под управлением предыдущих версий Microsoft Windows, называется значок **32-разрядная версия ODBC** или просто **ODBC**.  
  
 Ниже показано, как это 16-разрядное приложение вызывает DLL-файлов установки 32-разрядный драйвер. Между библиотека DLL установщика 16-разрядных и 32-разрядный драйвер библиотека DLL программы установки представляет собой универсальный преобразования библиотеку DLL, который преобразует вызовы DLL 16-разрядный установщик в 32-разрядный установщик DLL вызовы.  
  
 ![Как 16&#45;бит приложение вызывает 32&#45;бит DLL-файлов установки драйвера](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 В Windows на Windows (преобразование 16-разрядное в 32-разрядное) дополнительного преобразования DLL с именем Ds32gt.dll преобразует 16-разрядного аргумента значения, переданные через 32-разрядной установке DLL обратно в 16-разрядное.  
  
## <a name="components"></a>Компоненты  
 Компонент ODBC SDK MDAC 2.8 с пакетом обновления 1 включает следующие файлы для работы 16-разрядных приложений с 32-разрядные драйверы. Эти компоненты находятся в каталоге \Redist.  
  
|Имя файла|Описание|  
|---------------|-----------------|  
|Odbc16gt.dll|16-разрядное универсального преобразования DLL-Библиотека ODBC|  
|Odbc32gt.dll|32-разрядных ODBC универсального преобразования библиотек DLL|  
|Odbccp32.dll|32-разрядный установщик DLL|  
|Odbcad32.exe|32-разрядной программы администратора|  
|Odbcinst.hlp|Файл справки установщика|  
|Ds16gt.dll|16-разрядный драйвер установки универсального преобразование библиотеки DLL|  
|Ctl3d32.dll|32-разрядного трехмерного окна стиль библиотеки|  
  
 Кроме того следующие файлы, а также диспетчера драйверов ODBC 2.10 16-разрядное, которые не являются частью ODBC 3.51, необходимы и должны быть установлены с 16-разрядным приложением.  
  
|Имя файла|Описание|  
|---------------|-----------------|  
|ODBC.dll|16-разрядного диспетчера драйверов|  
|Odbcinst.dll|16-разрядный установщик DLL|  
|Odbcadm.exe|16-разрядных программ администратора ODBC|
