# Новые возможности

## Соединение с моделью<a name="modelConnect"></a>

```ts
interface OM {
	connect(https: string, wss: string, token: string. modelId: string, env: Object): OM;
}
```

&nbsp;

```js
connect(https: string, wss: string, userToken: string, modelId: string, env: Object): OM
```
Соединяется с моделью `modelId` по адресу `https`, используя [`WebSocket`](https://ru.wikipedia.org/wiki/WebSocket) `wss` и токен пользователя `userToken`, и передаёт [`переменные окружения`](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) `env`. Возвращает интерфейс модели [`OM`](https://github.com/optimacros/scripts_documentation/blob/main/API/API.md#OM), [`аналог`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#singleModel) глобальной переменной `om: OM` скриптов 1.0.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)