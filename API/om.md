# Интерфейс OM

1. [Интерфейс Common](common.md)
1. [Интерфейс System](system.md)
1. [Окружение](env.md)
1. [Представления](views.md)
	1. [Измерения](dimensions.md)
	1. [Манипуляция элементами](elementsManipulator.md)
	1. [Низкоуровневый доступ к клеткам и кубам](cubeCell.md)
	1. [Синхронизация мультикубов и справочников](sync.md)
	1. [Вкладка скриптов](scriptsTab.md)
	1. [Вкладка папок](foldersTab.md)
1. [Карта модели](modelMap.md)
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

### Интерфейс OM<a name="om"></a>
```ts
interface OM {
	readonly common: Common;
	readonly system: System;
	readonly environment: Environment;
	readonly multicubes: Multicubes;
	readonly times: Times;
	readonly versions: Versions;
	readonly lists: Lists;
	readonly filesystems: Filesystems;
	readonly optimization: Optimization;
	readonly connectors: Connectors;
	readonly notifications: Notifications.Manager;
	readonly workspace: Workspace;

	readonly isConnected: boolean;
	closeAsync(): Promise<void>;
}
```
Интерфейс `OM` являет собой набор интерфейсов, предоставляющих API доступа к модели и воркспейсу.

&nbsp;

```js
readonly common: Common;
```
Ссылка на интерфейс [`Common`](./common.md#common).

&nbsp;

```js
readonly system: System;
```
Ссылка на интерфейс [`System`](./system.md#system).

&nbsp;

```js
readonly environment: Environment;
```
Ссылка на интерфейс [`Environment`](./env.md#environment).

&nbsp;

```js
readonly multicubes: Multicubes;
```
Ссылка на интерфейс [`Multicubes`](./views.md#multicubes).

&nbsp;

```js
readonly times: Times;
```
Ссылка на интерфейс [`Times`](./dimensions.md#times).

&nbsp;

```js
readonly versions: Versions;
```
Ссылка на интерфейс [`Versions`](./dimensions.md#versions).

&nbsp;

```js
readonly lists: Lists;
```
Ссылка на интерфейс [`Lists`](./dimensions.md#lists).

&nbsp;

```js
readonly filesystems: Filesystems;
```
Ссылка на интерфейс [`Filesystems`](./fs.md#filesystems).

&nbsp;

```js
readonly optimization: Optimization;
```
Ссылка на интерфейс [`Optimization`](./optimization.md#optimization).

&nbsp;

```js
readonly connectors: Connectors;
```
Ссылка на интерфейс [`Connectors`](./connectors.md#connectors).

&nbsp;

```js
readonly notifications: Notifications.Manager;
```
Ссылка на интерфейс [`Notifications.Manager`](./notifications.md#manager).

&nbsp;

```js
readonly workspace: Workspace;
```
Ссылка на интерфейс [`Workspace`](./workspace.md#workspace).

&nbsp;

```js
readonly isConnected: boolean;
```
Признак установленного соединения с моделью.

&nbsp;

```js
closeAsync(): Promise<void>;
```
Закрывает соединение с моделью.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)