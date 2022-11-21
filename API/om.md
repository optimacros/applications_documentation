# Интерфесы модели OM

1. [Интерфейс Common](common.md)
1. [Окружение](env.md)
1. [Представления](views.md)
	1. [Измерения](dimensions.md)
	1. [Манипуляция элементами](elementsManipulator.md)
	1. [Низкоуровневый доступ к клеткам и кубам](cubeCell.md)
	1. [Синхронизация мультикубов и справочников](sync.md)
1. [Экспорт и импорт](exportImport.md)
1. [Файловые системы](fs.md)
1. [Файлы CSV](csv.md)
1. [Оптимизационные запросы](optimization.md)
1. [Коннекторы](connectors.md)
	1. [Реляционные БД](relationalDB.md)
	1. [MongoDB](mongoDB.md)
	1. [HTTP](http.md)
	1. [WinAgent](winAgent.md)
1. [Уведомление пользователя](notifications.md)
1. [Цепочки скриптов](scriptChains.md)

### Интерфейс OM<a name="OM"></a>
```ts
interface OM {
	readonly common: Common;
	readonly environment: Environment;
	readonly multicubes: Multicubes;
	readonly times: Times;
	readonly versions: Versions;
	readonly lists: Lists;
	readonly filesystems: Filesystems;
	readonly optimization: Optimization;
	readonly connectors: Connectors;
	readonly notifications: Notifications.Manager;
}
```
Интерфейс `OM` являет собой набор интерфейсов, предоставляющих API доступа к модели.

&nbsp;

```js
readonly common: Common
```
Ссылка на интерфейс [`Common`](./common.md#Common).

&nbsp;

```js
readonly environment: Environment
```
Ссылка на интерфейс [`Environment`](./env.md#Environment).

&nbsp;

```js
readonly multicubes: Multicubes
```
Ссылка на интерфейс [`Multicubes`](./views.md#Multicubes).

&nbsp;

```js
readonly times: Times
```
Ссылка на интерфейс [`Times`](./dimensions.md#Times).

&nbsp;

```js
readonly versions: Versions
```
Ссылка на интерфейс [`Versions`](./dimensions.md#Versions).

&nbsp;

```js
readonly lists: Lists
```
Ссылка на интерфейс [`Lists`](./dimensions.md#Lists).

&nbsp;

```js
readonly filesystems: Filesystems
```
Ссылка на интерфейс [`Filesystems`](./fs.md#Filesystems).

&nbsp;

```js
readonly optimization: Optimization
```
Ссылка на интерфейс [`Optimization`](./optimization.md#Optimization).

&nbsp;

```js
readonly connectors: Connectors
```
Ссылка на интерфейс [`Connectors`](./connectors.md#Connectors).

&nbsp;

```js
readonly notifications: Notifications.Manager
```
Ссылка на интерфейс [`Notifications.Manager`](./notifications.md#Manager).

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
