# Отличия от Скриптов 1.0

1. [Доступ к интерфейсам модели](#model-access)
1. [Доступ к входным параметрам](#input-params)
1. [Запуск дочернего скрипта](#run-script)
1. [Вывод статусного сообщения](#status)
1. [Вывод приложения](#async-output)

&nbsp;

## Доступ к интерфейсам модели<a name="model-access"></a>

В отличие от Скриптов 1.0, из системы Application Manager можно получить доступ к [интерфейсам](./API/om.md) любой модели на любом воркспейсе. Ссылка на интерфейсы модели записывается в локальную переменую скрипта после [установки соединения](./API/API.md#model-connect) с моделью. Таким образом из одного скрипта можно установить соединение сразу с несколькими моделями.

В Скриптах 1.0 запуск скрипта осуществляется из модели, поэтому скрипт может получить доступ только к интерфейсам данной модели через глобальную переменную [`om: OM`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#single-model).

&nbsp;

## Доступ к входным параметрам<a name="input-params"></a>

В системе Application Manager передача параметров в скрипт осуществляется через свойство [params](./API/API.md#input-params) глобального объекта `OM`. Скрипты в модели могут получать доступ к переменным окружения с помощью интерфейса [Environment](https://github.com/optimacros/scripts_documentation/blob/main/API/env.md#environment).

&nbsp;

## Запуск дочернего скрипта<a name="run-script"></a>

В системе Application Manager запуск дочернего скрипта осуществляется с помощью метода [script](./API/API.md#run-script) глобального объекта `OM`. В Скриптах 1.0 - с помощью интерфейса [ResultActionsInfo](https://github.com/optimacros/scripts_documentation/blob/main/API/scriptChains.md#result-actions-info).

&nbsp;

## Вывод статусного сообщения<a name="status"></a>

В системе Application Manager метод [status](./API/API.md#status) глобального объекта `OM` является аналогом метода [setStatusMessage](https://github.com/optimacros/scripts_documentation/blob/main/API/common.md#request-manager.set-status-message) в Скриптах 1.0.

&nbsp;

## Вывод приложения<a name="async-output"></a>

Вывод приложения доступен непосредственно во время его работы в режиме реального времени в окне терминала вывода. [Вывод в Скриптах 1.0](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#sync-output) был `доступен` только после завершения работы скрипта.

**`console.log()` добавляет символ переноса строки**<a name="line-break"></a>

В [отличие](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#no-line-break) от скриптов 1.0 при выводе информации на экран не нужно специально добавлять символ `'\n'` переноса строки.

&nbsp;

[Оглавление](./README.md)
