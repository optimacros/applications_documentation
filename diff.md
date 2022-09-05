# Отличия от Скриптов 1.0

1. [Соединение с моделью](#modelConnect)
1. [Запуск дочернего скрипта](#runScript)
1. [Вывод статусного сообщения](#status)
1. [Веб-обработчик](#webHandler)
1. [Вывод приложения](#asyncOutput)

## Соединение с моделью<a name="modelConnect"></a>

```js
OM.connect(https: string, wss: string, token: string, modelId: string, env?: Object): OM
```
Статический метод интерфейса `OM`. Устанавливает соединение с моделью `modelId` по адресу `https`, используя [WebSocket](https://ru.wikipedia.org/wiki/WebSocket) `wss` и токен пользователя `userToken`, и устанавливает [переменные окружения](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) `env`. Доступ к переменным окружения можно получить с помощью интрефейса [Environment](./API/env.md#Environment). Возвращает ссылку на интерфейс модели [OM](./API/API.md#OM), [аналог](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#singleModel) глобальной переменной `om: OM` скриптов 1.0.

&nbsp;

```js
OM.connectAsync(https: string, wss: string, token: string, modelId: string, env?: Object): Promise<OM>
```
Статический метод интерфейса `OM`. Выполняет асинхронную операцию соединения с моделью. Возвращает ссылку на объект [Promise](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Promise). Чтобы получить соединение с моделью, необходимо дождаться, когда `промис` завершиться. 

При создании соединения с помощью `connectAsync` отключаются и выдают ошибку все синхронные методы всех интерфейсов API, их асинхронные пары продолжают работать.

&nbsp;

## Запуск дочернего скрипта<a name="runScript"></a>

```js
OM.script(relativePathOrId: string, params: Object): EventPromise
```
Статический метод интерфейса `OM`. Запускает скрипт `relativePathOrId` с параметрами `params`. В качестве параметра `relativePathOrId` можно передать идентификатор скрипта, существующего в Application Manager (скрипт может находиться в другом приложении), или относительный путь к скрипту в текущем приложении. **Важно! Скрипт должен быть запускаемым.** Список запускаемых скриптов и их идентификаторы можно найти, нажав на кнопку `Edit Application` -> `Executable Scripts`.

Метод возвращает ссылку на объект класса [EventPromise](#EventPromise). Родительский скрипт может ждать результата выполнения дочернего скрипта или продолжить работу параллельно с дочерним скриптом.

### Класс EventPromise<a name="EventPromise"></a>
```ts
class EventPromise extends EventEmitter {
    then(callback: (result) => void): this;
    catch(callback: (error) => void): this;
}
```
Комбинация возможностей обычного [Promise](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Promise) с возможностью подписываться на результат или ожидать с помощью [await](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/await) и [EventEmitter](https://nodejsdev.ru/doc/event-emitter/#eventemitter) генерирующего события из источника. ***Описание данного класса находиться в доработке.***

&nbsp;

## Вывод статусного сообщения<a name="status"></a>

```js
OM.status(...args: any[]): OM
```
Статический метод интерфейса `OM`. Устанавливает статусное сообщение `args`. Если `args` задано в виде массива, то выводит элементы в заданном порядке, разделяя их пробелом. Имеет смысл во время длительной работы скриптов сообщать пользователю об этапах или процентах выполненных работ. Аналог метода [setStatusMessage](https://github.com/optimacros/scripts_documentation/blob/main/API/common.md#RequestManager.setStatusMessage) в Скриптах 1.0. ***Не реализовано, выводит подсвеченное зеленым цветом сообщение в терминале вывода.***

&nbsp;

## Веб-обработчик<a name="webHandler"></a>

```js
OM.web(eventName, callback: (args: {}) => string | WebHandlerResponse)
```
***Метод находиться в разработке.***

Статический метод интерфейса `OM`. Из функций `callback` web-обработчиков нельзя использовать `OM.connect`, можно только `OM.connectAsync`.

### Интерфейс WebHandlerResponse<a name="WebHandlerResponse"></a>
```ts
interface WebHandlerResponse {
    headers: { [x: string]: string };
    body: string;
}
```

&nbsp;

## Вывод приложения<a name="asyncOutput"></a>

Вывод приложения доступен непосредственно во время его работы в режиме реального времени в окне терминала вывода. [Вывод в Скриптах 1.0](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#syncOutput) был `доступен` только после завершения работы скрипта.

### `console.log()` добавляет символ переноса строки<a name="lineBreak"></a>

В [отличие](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#noLineBreak) от скриптов 1.0 при выводе информации на экран не нужно специально добавлять символ `'\n'` переноса строки.

&nbsp;

[Оглавление](../README.md)
