# API Reference

1. [Доступ к входным параметрам](#input-params)
1. [Соединение с моделью](#model-connect)
1. [Закрытие соединения с моделью](#model-close)
1. [Запуск дочернего скрипта](#run-script)
1. [Вывод статусного сообщения](#status)
1. [Веб-интерфейсы](#web-handlers)
1. [Интерфейсы модели OM](./om.md)

&nbsp;

### Интерфейс OMStatic
```ts
export interface OMStatic {
	readonly params: Object;
	
	connect(https: string, wss: string, token: string, modelId: string, env?: Object, ignoreSslErrors?: boolean): OM;
	async connectAsync(https: string, wss: string, token: string, modelId: string, env?: Object, ignoreSslErrors?: boolean): Promise<OM>;
	
	close(): void;
	async closeAsync(): Promise<void>;
	
	script(relativePathOrId: string, params: Object): EventPromise;
	status(...args: any[]): OM;
	web(eventName: string, callback: (request: OMWebRequest) => string | WebHandlerResponse): void;
}
```
Интерфейс `OMStatic` являет собой набор методов глобального объекта `OM` в системе Application Manager.

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

## Доступ к входным параметрам<a name="input-params"></a>

```js
OM.params: Object
```
Позволяет получить доступ к параметрам, переданным в скрипт при его запуске в виде [JSON](https://habr.com/ru/post/554274/).

`Запуск скрипта с параметрами` позволяет передать в скрипт входные параметры. В системе Application Manager параметры задаются в виде [JSON](https://habr.com/ru/post/554274/) в модальном окне `General parameters` или в модальном окне при запуске скрипта.

![Script parameters](./pic/scriptParameters.png)

Окно ввода параметров в формате JSON.

![JSON parameters](./pic/jsonParameters.png)

&nbsp;

### Отладочный вывод

Для получения отладочного вывода AM нужно передать параметр `{"debugLevel": "debug"}`.

&nbsp;

## Соединение с моделью<a name="model-connect"></a>

```js
OM.connect(https: string, wss: string, token: string, modelId: string, env?: Object, ignoreSslErrors?: boolean): OM | undefined;
```
Устанавливает соединение с моделью `modelId` по адресу `https`, используя [WebSocket](https://ru.wikipedia.org/wiki/WebSocket) `wss` и токен пользователя `token`, и устанавливает в модели [переменные окружения](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) `env`. В случае успешного соединения возвращает интерфейс модели [`OM`](./om.md#om), [аналог](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#single-model) глобальной переменной `om: OM` скриптов 1.0. В случае безуспешного – возвращает `undefined`.

Обязательные параметры:
- `https` - URL-адрес воркспейса с указанием протокола HTTP/HTTPS.
- `wss` - URL-адрес воркспейса с указанием протокола WS/WSS.
- `token` - токен пользователя для доступа к данным модели. Это уникальная секретная строка, которую можно получить в профиле пользователя через «Логин-центр» (Create Named Token). Токен может быть создан только администратором ЛЦ и имеет ограничение по времени жизни, которое нужно выбрать при его создании.
- `modelId` - идентификатор модели. Индентификатор можно узнать в адресной строке браузера.

Опциональные параметры:
- `env` - переменные окружения, которые будут переданы в модель после установки соединения. Доступ к переменным окружения можно получить с помощью интерфейса [`Environment`](./env.md#environment).
- `ignoreSslErrors` - параметр, отключающий проверку [SSL](https://ru.wikipedia.org/wiki/SSL).

**Внимание!** Токен пользователя обязательно должен быть передан в скрипт как [входной параметр](#input-params), иначе ваш личный секретный токен может увидеть любой пользователь, у которого есть доступ к коду вашего приложения!

### Пример установки соединения и получения ссылки на интерфейс модели

1. Получаем URL-адрес воркспейса и идентификатор модели.

![URL-адрес и modelId](./pic/modelId.png)

2. Если версия *Workspace Middle-End* меньше `2.3.2`, то `wss`, как правило, будет таким: `wss://ws116.optimacros.com:8081`. Если версия *Workspace Middle-End* больше или равна `2.3.2`, то `wss`, как правило, будет таким: `wss://ws116.optimacros.com/ws`. 

3. Задаём токен пользователя в модальном окне `General parameters` в системе Application Manager.

![Secret Token](./pic/secretToken.png)

4. Запускаем скрипт с параметрами.

```js
const om = OM.connect(
	'https://ws116.optimacros.com/',
	'wss://ws116.optimacros.com/ws',
	OM.params.token,
	'3e72d0057138616a1904c69848389ac0',
	{param1: 1, param2: 'abc'}
);
```
В результате в переменную `om` будет записана ссылка на интерфейс модели [`OM`](./API.md#om). В модели будут установлены переменные окружения `param1` и `param2`.

&nbsp;

### Асинхронная операция соединения <a name="connect-async"></a>

```js
async OM.connectAsync(https: string, wss: string, token: string, modelId: string, env?: Object, ignoreSslErrors?: boolean): Promise<OM | undefined>;
```
Выполняет асинхронную операцию соединения с моделью. Описание параметров соответствует методу [`OM.connect()`](#model-connect). Возвращает ссылку на объект [`Promise`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Promise). Чтобы получить соединение с моделью, необходимо дождаться, когда `Promise` завершится. 

При создании соединения с помощью `connectAsync()` все синхронные методы всех интерфейсов API отключаются и выдают ошибку, их асинхронные пары продолжают работать.

&nbsp;

### Закрытие соединения с моделью<a name="model-close"></a>

```js
close(): void
async closeAsync(): Promise<void>
```
Закрывает соединение с моделью, а также все открытые связанные с ней сетевые соединения: с базами данных, с FTP-серверами.

&nbsp;

## Запуск дочернего скрипта<a name="run-script"></a>

```js
OM.script(relativePathOrId: string, params: Object): EventPromise
```
Запускает скрипт `relativePathOrId` с [входными параметрами](#input-params) `params`. В качестве параметра `relativePathOrId` можно передать идентификатор скрипта, существующего в Application Manager (скрипт может находиться в другом приложении), или относительный путь к скрипту в текущем приложении. **Важно! Скрипт должен быть исполняемым.** Список исполняемых скриптов и их идентификаторы можно найти в модальном окне `Edit Application` на вкладке `Executable Scripts`.

Метод возвращает ссылку на объект класса `EventPromise`. Родительский скрипт может ждать результата выполнения дочернего скрипта или продолжить работу параллельно с дочерним скриптом.

### Класс EventPromise<a name="event-promise"></a>
```ts
class EventPromise extends EventEmitter {
	then(callback: (result: any) => void): this;
	catch(callback: (error: any) => void): this;
}
```
Комбинация возможностей обычного [`Promise`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Promise) с возможностью подписываться на результат или ожидать с помощью [`await`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/await) и [`EventEmitter`](https://nodejsdev.ru/doc/event-emitter/#eventemitter), генерирующего события из источника.

&nbsp;

## Вывод статусного сообщения<a name="status"></a>

```js
OM.status(...args: any[]): OM
```
Устанавливает статусное сообщение `args`. Если `args` задано в виде массива, то выводит элементы в заданном порядке, разделяя их пробелом. Имеет смысл во время длительной работы скриптов сообщать пользователю об этапах или процентах выполненных работ. Аналог метода [`setStatusMessage()`](https://github.com/optimacros/scripts_documentation/blob/main/API/common.md#request-manager.set-status-message) в Скриптах 1.0. ***Не реализовано, выводит подсвеченное зелёным цветом сообщение в терминале вывода.***

&nbsp;

## Веб-интерфейсы<a name="web-handlers"></a>

```js
web(eventName: string, callback: (request: OMWebRequest) => string | WebHandlerResponse): void;
```
Создает веб-хендлер для взаимодействия с другими приложениями. Подробное описание [читать тут](./webHandlers.md).

&nbsp;

[Оглавление](../README.md)