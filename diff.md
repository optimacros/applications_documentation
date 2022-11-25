# Отличия от Скриптов 1.0

1. [Доступ к интерфейсам модели](#modelAccess)
1. [Доступ к входным параметрам](#inputParams)
1. [Запуск дочернего скрипта](#runScript)
1. [Вывод статусного сообщения](#status)
1. [Вывод приложения](#asyncOutput)

&nbsp;

## Доступ к интерфейсам модели<a name="modelAccess"></a>

В отличие от Скриптов 1.0, из системы Application Manager можно получить доступ к [интерфейсам](./API/om.md) любой модели на любом воркспейсе. Ссылка на интерфейсы модели записывается в локальную переменую скрипта после [установки соединения](./API/API.md#modelConnect) с моделью. Таким образом из одного скрипта можно установить соединение сразу с несколькими моделями.

В Скриптах 1.0 запуск скрипта осуществляется из модели, поэтому скрипт может получить доступ только к интерфейсам данной модели через глобальную переменную [`om: OM`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#singleModel).

&nbsp;

## Доступ к входным параметрам<a name="inputParams"></a>

В системе Application Manager передача параметров в скрипт осуществляется через свойство [params](./API/API.md#inputParams) глобального объекта `OM`. Скрипты в модели могут получать доступ к переменным окружения с помощью интерфейса [Environment](https://github.com/optimacros/scripts_documentation/blob/main/API/env.md#Environment).

&nbsp;

## Запуск дочернего скрипта<a name="runScript"></a>

В системе Application Manager запуск дочернего скрипта осуществляется с помощью метода [script](./API/API.md#runScript) глобального объекта `OM`. В Скриптах 1.0 - с помощью интерфейса [ResultActionsInfo](https://github.com/optimacros/scripts_documentation/blob/main/API/scriptChains.md#ResultActionsInfo).

&nbsp;

## Вывод статусного сообщения<a name="status"></a>

В системе Application Manager метод [status](./API/API.md#status) глобального объекта `OM` является аналогом метода [setStatusMessage](https://github.com/optimacros/scripts_documentation/blob/main/API/common.md#RequestManager.setStatusMessage) в Скриптах 1.0.

&nbsp;

## Вывод приложения<a name="asyncOutput"></a>

Вывод приложения доступен непосредственно во время его работы в режиме реального времени в окне терминала вывода. [Вывод в Скриптах 1.0](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#syncOutput) был `доступен` только после завершения работы скрипта.

**`console.log()` добавляет символ переноса строки**<a name="lineBreak"></a>

В [отличие](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#noLineBreak) от скриптов 1.0 при выводе информации на экран не нужно специально добавлять символ `'\n'` переноса строки.

&nbsp;

[Оглавление](./README.md)
