---
title: mssqlctl bdc pool status reference
titleSuffix: SQL Server big data clusters
description: Справочная статья по mssqlctl bdc пула состояние команды.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6eba925adeb7f18adff133ba8110c6766bfed79
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394316"
---
# <a name="mssqlctl-bdc-pool-status"></a>состояние пула mssqlctl bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

В следующей статье приведены ссылки для **состояния пула bdc** команды в **mssqlctl** средство. Дополнительные сведения о других **mssqlctl** команды, см. в разделе [mssqlctl ссылку](reference-mssqlctl.md).

## <a name="commands"></a>Команды
|     |     |
| --- | --- |
[Показать состояние пула bdc mssqlctl](#mssqlctl-bdc-pool-status-show) | Состояние пула.
## <a name="mssqlctl-bdc-pool-status-show"></a>Показать состояние пула bdc mssqlctl
Состояние пула.
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>Примеры
Получение состояния пула носителей.
```bash
mssqlctl bdc pool status show --kind storage --name default
```
Получение состояния пула данных.
```bash
mssqlctl bdc pool status show --kind data --name default
```
Получение состояния пула вычислений.
```bash
mssqlctl bdc pool status show --kind compute --name default
```
Получение состояния пула master.
```bash
mssqlctl bdc pool status show --kind master --name default
```
Получение состояния пула spark.
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Обязательные параметры
#### `--kind -k`
Тип пула BDC.
### <a name="optional-parameters"></a>Необязательные параметры
#### `--name -n`
Имя пула BDC.
`default`
### <a name="global-arguments"></a>Глобальные аргументы
#### `--debug`
Увеличьте уровень подробного ведения журнала для отображения всех журналов отладки.
#### `--help -h`
Отображение этого справочного сообщения и выход.
#### `--output -o`
Формат выходных данных.  Допустимые значения: json, jsonc, table, tsv.  По умолчанию: json.
#### `--query -q`
Строка запроса JMESPath. См. в разделе [ http://jmespath.org/ ](http://jmespath.org/]) Дополнительные сведения и примеры.
#### `--verbose`
Увеличьте уровень подробного ведения журнала. Используйте параметр--debug, чтобы получить полные журналы отладки.

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения об установке **mssqlctl** инструмент, см. в разделе [установить mssqlctl для управления кластерами больших данных SQL Server 2019](deploy-install-mssqlctl.md).