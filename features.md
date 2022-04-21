# Новые возможности

## Соединение с моделью<a name="modelConnect"></a>

```ts
// комбинация возможностей обычного Promise, с возможностью подписываться на результат или ожидать с помощью await
// и EventEmitter, генерирующего события из источника
interface EventPromise {
    then(callback: (result) => void): void;
    catch(callback: (error) => void): void;
    on('start', callback: () => void): void;
    on('stop', callback: () => void): void;
    on('console', callback: (...args: any[]) => void): void;
    on('status', callback: (...args: any[]) => void): void;
    on('error', callback: () => void): void; // предшествует ошибке, которую можно поймать через catch
}

interface WebHandlerResponse {
    headers: { [x: string]: string };
    body: string;
}

interface OM {
    // при создании соединения с помощью connectAsync отключаются и выдают ошибку
    // все синхронные методы всех интерфейсов API, их асинхронные пары продолжают работать
	connectAsync(https: string, wss: string, token: string. modelId: string, env: Object): Promise<OM>;
	connect(https: string, wss: string, token: string. modelId: string, env: Object): OM;
	script(relativePathOrId: string, params: {}): EventPromise;
	status(...args: any[]): OM;
    // из функций callback web-обработчиков нельзя использовать OM.connect, можно только OM.connectAsync
    web(eventName, callback: (args: {}) => string | WebHandlerResponse);
}
```

&nbsp;

```js
connect(https: string, wss: string, userToken: string, modelId: string, env: Object): OM
```
Соединяется с моделью `modelId` по адресу `https`, используя [`WebSocket`](https://ru.wikipedia.org/wiki/WebSocket) `wss` и токен пользователя `userToken`, и передаёт [`переменные окружения`](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) `env`. Возвращает интерфейс модели [`OM`](https://github.com/optimacros/scripts_documentation/blob/main/API/API.md#OM), [`аналог`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#singleModel) глобальной переменной `om: OM` скриптов 1.0.

&nbsp;

[Оглавление](../README.md)