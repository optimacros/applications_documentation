# Отличия от Скриптов 1.0

1. [Соединение с моделью](#modelConnect)
1. [Запуск дочернего скрипта](#runScript)
1. [Вывод статусного сообщения](#status)
1. [Веб-обработчик](#webHandler)
1. [Вывод приложения](#asyncOutput)

## Соединение с моделью<a name="modelConnect"></a>

```js
OM.connectAsync(https: string, wss: string, token: string. modelId: string, env?: Object): Promise<OM>
```
Описание.

&nbsp;

```js
OM.connect(https: string, wss: string, token: string, modelId: string, env?: Object): OM
```
Статический метод интерфейса `OM`. Устанавливает соединение с моделью `modelId` по адресу `https`, используя [WebSocket](https://ru.wikipedia.org/wiki/WebSocket) `wss` и токен пользователя `userToken`, и устанавливает [переменные окружения](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) `env`. Доступ к переменным окружения можно получить с помощью интрефейса [Environment](./API/env.md#Environment). Возвращает интерфейс модели [OM](./API/API.md#OM), [аналог](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#singleModel) глобальной переменной `om: OM` скриптов 1.0.

&nbsp;

## Запуск дочернего скрипта<a name="runScript"></a>

```js
OM.script(relativePathOrId: string, params: Object): EventPromise
```
Статический метод интерфейса `OM`. Запускает скрипт `relativePathOrId` с параметрами `params`. В качестве параметра `relativePathOrId` можно передать идентификатор скрипта, существующего в Application Manager (скрипт может находиться в другом приложении), или относительный путь к скрипту в текущем приложении. **Важно! Скрипт должен быть запускаемым.**  Список запускаемых скриптов и их идентификаторы можно найти, нажав на кнопку `Edit Application` -> `Executable Scripts`.

Метод возвращает ссылку на объект [EventPromise](#EventPromise).

### Интерфейс EventPromise<a name="EventPromise"></a>
```ts
interface EventPromise {
    then(callback: (result) => void): void;
    catch(callback: (error) => void): void;
    on('start', callback: () => void): void;
    on('stop', callback: () => void): void;
    on('console', callback: (...args: any[]) => void): void;
    on('status', callback: (...args: any[]) => void): void;
    on('error', callback: () => void): void; // предшествует ошибке, которую можно поймать через catch
}
```

&nbsp;

## Вывод статусного сообщения<a name="status"></a>

```js
OM.status(...args: any[]): OM
```
Статический метод интерфейса `OM`.

&nbsp;

## Веб-обработчик<a name="webHandler"></a>

```js
OM.web(eventName, callback: (args: {}) => string | WebHandlerResponse)
```
Статический метод интерфейса `OM`.

&nbsp;

## Вывод приложения<a name="asyncOutput"></a>

Вывод приложения доступен непосредственно во время его работы в режиме реального времени. [Вывод в Скриптах 1.0](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#syncOutput) был `доступен` только после завершения работы скрипта.

&nbsp;

### `console.log()` добавляет символ переноса строки<a name="lineBreak"></a>

В [отличие](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#noLineBreak) от скриптов 1.0 при выводе информации на экран не нужно специально добавлять символ `'\n'` переноса строки.

&nbsp;

[Оглавление](../README.md)
