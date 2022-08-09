# Манипуляция элементами

### Интерфейс ElementsCreator<a name="ElementsCreator"></a>
```ts
`Не реализовано`
```

```ts
interface ElementsCreator {
	numeric(): NumericElementsCreator;
	named(): NamedElementsCreator;
}
```
Абстрактный интерфейс, предоставляющий конкретные интерфейсы с различными возможностями добавления элементов.

&nbsp;

```js
numeric(): NumericElementsCreator
```
Возращает ссылку на [`NumericElementsCreator`](#NumericElementsCreator).

&nbsp;

```js
named(): NamedElementsCreator
```
Возращает ссылку на [`NamedElementsCreator`](#NamedElementsCreator).

&nbsp;

### Интерфейс NumericElementsCreator<a name="NumericElementsCreator"></a>
```ts
`Не реализовано`
```

```ts
interface NumericElementsCreator {
	setCount(count: number): NumericElementsCreator;
	setPositionAfter(relativeLongId: number): NumericElementsCreator;
	setPositionBefore(relativeLongId: number): NumericElementsCreator;
	setPositionStart(): NumericElementsCreator;
	setPositionEnd(): NumericElementsCreator;
	setPositionChildOf(parentLongId: number): NumericElementsCreator;
	create(): number[];
}
```
Интерфейс позволяет добавить заданное количество элементов в заданную позицию таблицы. Аналог кнопки "Добавить элементы" в интерфейсе Optimacros. Перед созданием элементов необходимо указать их количество (нет значения по умолчанию) и позицию добавления (по умолчанию: в конец).

&nbsp;

```js
setCount(count: number): NumericElementsCreator
```
Устанавливает количество добавляемых элементов. Возвращает `this`.

&nbsp;

```js
setPositionAfter(relativeLongId: number): NumericElementsCreator
```
Устанавливает позицию добавления после [`relativeLongId`](./views.md#longId). Возвращает `this`.

&nbsp; 

```js
setPositionBefore(relativeLongId: number): NumericElementsCreator
```
Устанавливает позицию добавления до [`relativeLongId`](./views.md#longId). Возвращает `this`.

&nbsp;

```js
setPositionStart(): NumericElementsCreator
```
Устанавливает позицию добавления в начало. Возвращает `this`.

&nbsp;

<a name="NumericElementsCreator.setPositionEnd"></a>
```js
setPositionEnd(): NumericElementsCreator
```
Устанавливает позицию добавления в конец, это поведение по умолчанию. Этот вариант наиболее эффективный с точки зрения производительности. Возвращает `this`.

&nbsp;

<a name="NumericElementsCreator.setPositionChildOf"></a>
```js
setPositionChildOf(parentLongId: number): NumericElementsCreator
```
Устанавливает позицию добавления дочерней для [`parentLongId`](./views.md#longId). Возвращает `this`.

&nbsp;

```js
create(): number[]
```
Добавляет элементы и возвращает массив их [`longId`](./views.md#longId).

&nbsp;

### Интерфейс ElementsDeleter<a name="ElementsDeleter"></a>
```ts
interface ElementsDeleter {
	appendIdentifier(identifier: number): ElementsDeleter;
	delete(): ElementsDeleter;
}
```
Интерфейс позволяет удалить элементы таблицы. Аналог кнопки "Удалить" в интерфейсе Optimacros.

&nbsp;

```js
appendIdentifier(identifier: number): ElementsDeleter
```
Добавляет в буфер элемент, чей [`longId`](./views.md#longId) равен `identifier`. Возращает `this`.

&nbsp;

```js
delete(): ElementsDeleter
```
Фактически удаляет все элементы в буфере из таблицы. Возвращает `this`.

&nbsp;

### Интерфейс ElementsReorder<a name="ElementsReorder"></a>
```ts
`Не реализовано`
```

```ts
interface ElementsReorder {
	append(longId: number, relativeLongId?: number, position?: string): ElementsReorder;
	reorder(): ElementsReorder;
	count(): number;
	reverse(): ElementsReorder;
}
```
Интерфейс позволяет перетасовать элементы и доступен только для элементов справочников. Во время работы хранит очередь элементов, которые функцией [`reorder()`](#reorder) будут переданы на сервер для перепозиционирования в порядке этой очереди.

Аналог кнопки "Переместить" в интерфейсе Optimacros. Но в отличие от интерфейса пользователя, в скриптах 1.0 изменение позиции элемента возможно только в пределах элементов с тем же родительским элементом. Поэтому для постановки элемента в конкретную позицию среди элементов с другим родительским, нужно сначала сменить родителя. Именно так и организован интерфейс пользователя: в таком случае он отправляет на сервер две команды.

&nbsp;

```js
append(longId: number, relativeLongId?: number, position?: string): ElementsReorder
```
Добавляет в очередь данные о [`longId`](./views.md#longId) элемента, который впоследствии будет позиционирован относительно элемента `relativeLongId` (значение по умолчанию: `-1`). Возвращает `this`. Способ позиционирования задаёт аргумент `position` (регистр имеет значение):

`'Before'` — непосредственно перед `relativeLongId`;

`'After'` — сразу за `relativeLongId`;

`'Start'` — в начало (необходимо указать `relativeLongId === -1`);

`'End'` — в конец (необходимо указать `relativeLongId === -1`), это значение по умолчанию.

&nbsp;

<a name="reorder"></a>
```js
reorder(): ElementsReorder
```
Передаёт на сервер данные для фактического перемещения их в модели и очищает буфер. Возвращает `this`.

&nbsp;

```js
count(): number
```
Возвращает количество элементов в очереди.

&nbsp;

```js
reverse(): ElementsReorder
```
Переворачивает очередь. Возвращает `this`.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)