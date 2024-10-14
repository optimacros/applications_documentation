# Прямой доступ к данным

## Интерфейс RawData<a name="raw-data"></a>
```ts
interface RawData {
	reader(): RawDataReader;
	async readerAsync(): Promise<RawDataReader>;
	
	writer(): RawDataWriter;
	async writerAsync(): Promise<RawDataWriter>;
}
```
Интерфейс прямого доступа к данным таблицы [`Grid`](./views.md#grid) или её диапазона – [`GridRange`](./views.md#grid-range) или [`GridRangeChunk`](./views.md#grid-range-chunk).

&nbsp;

```js
reader(): RawDataReader;
async readerAsync(): Promise<RawDataReader>;
```
Возвращает интерфейс [`RawDataReader`](#raw-data-reader) прямого чтения данных таблицы.

&nbsp;

```js
writer(): RawDataWriter;
async writerAsync(): Promise<RawDataWriter>;
```
Возвращает интерфейс [`RawDataWriter`](#raw-data-writer) прямой записи данных в таблицу.

&nbsp;

### Интерфейс RawDataReader<a name="raw-data-reader"></a>
```ts
interface RawDataReader {
	columns(): RawDataHeader;
	rows(): RawDataHeader;

	getColumnKey(): RawHeaderKey;
	getRowKey(): RawHeaderKey;
	
	setColumnKey(value: RawHeaderKey): this;
	setRowKey(value: RawHeaderKey): this;

	getMode(): string;
	setModeText(): this;
	setModeNativeValue(): this;

	getRawTexts(): (number | string | null)[][];
	getRawNativeValues(): (number | string | null)[][];

	getRowsAsArray(): RawRow[];
	getRowsAsObject(): Record<string, RawRow>;
	getRowsAsItems(): RowFullItem[];

	firstEmptyRowIndex(): number;

	refresh(): this;
	async refreshAsync(): Promise<this>;
}
```
Интерфейс прямого доступа к данным на чтение. Варианты представления данных довольно разнообразны, и для осознания получаемых результатов нужно понимать, что они зависят от [ключа столбцов](#raw-data-reader.get-column-key), [ключа строк](#raw-data-reader.get-row-key)  и [режима представления ячеек](#raw-data-reader.get-mode).

&nbsp;

```js
columns(): RawDataHeader;
```
Возвращает интерфейс [`RawDataHeader`](#raw-data-header) заголовков столбцов.

&nbsp;

```js
rows(): RawDataHeader;
```
Возвращает интерфейс [`RawDataHeader`](#raw-data-header) заголовков строк.

&nbsp;

<a name="raw-data-reader.get-column-key"></a>
```js
getColumnKey(): RawHeaderKey;
```
Возвращает [`ключ`](#raw-header-key) для формирования заголовка ячейки при получении строки в виде объекта, что используется в функциях [`getRowsAsArray()`](#raw-data-reader.get-rows-as-array), [`getRowsAsObject()`](#raw-data-reader.get-rows-as-object) и [`getRowsAsItems()`](#raw-data-reader.get-rows-as-items). Значение по умолчанию: `'label'`.

&nbsp;

<a name="raw-data-reader.get-row-key"></a>
```js
getRowKey(): RawHeaderKey;
```
Аналог [`getColumnKey()`](#raw-data-reader.get-column-key) для строк.

&nbsp;

```js
setColumnKey(value: RawHeaderKey): this;
```
Устанавливает значение ключа для столбцов. См. описание [`getColumnKey()`](#raw-data-reader.get-column-key). Возвращает `this`.

&nbsp;

```js
setRowKey(value: RawHeaderKey): this;
```
Устанавливает значение ключа для строк. См. описание [`getColumnKey()`](#raw-data-reader.get-column-key). Возвращает `this`.

&nbsp;

<a name="raw-data-reader.get-mode"></a>
```js
getMode(): string;
```
Возвращает режим представления ячеек, используемый функциями [`getRowsAsArray()`](#raw-data-reader.get-rows-as-array), [`getRowsAsObject()`](#raw-data-reader.get-rows-as-object) и [`getRowsAsItems()`](#raw-data-reader.get-rows-as-items). Допустимые значения: `'Text'`, `'NativeValue'`. В зависимости от этого режима представления ячеек будут соответствовать тому, что возвращают функции: [`Сell.getTextValue()`](./views.md#cell.get-text-value), [`Сell.getNativeValue()`](./views.md#cell.get-native-value). Значение по умолчанию: `'Text'`.

&nbsp;

```js
setModeText(): this;
```
Устанавливает значение режима представления ячеек в `'Text'`. Возвращает `this`.

&nbsp;

```js
setModeNativeValue(): this;
```
Устанавливает значение режима представления ячеек в `'NativeValue'`. Возвращает `this`.

&nbsp;

```js
getRawTexts(): (string | null)[][];
```
Возвращает содержимое таблицы в виде двумерного массива. Каждый внутренний массив соответствует одной строке и содержит *текст* ячеек этой строки. От значения [режима представления](#raw-data-reader.get-mode) поведение функции не зависит.

&nbsp;

```js
getRawNativeValues(): (string | number | null)[][];
```
Возвращает содержимое таблицы в виде двумерного массива. Каждый внутренний массив соответствует одной строке и содержит [*самородные значения*](./views.md#cell.get-native-value) ячеек этой строки. От значения [режима представления](#raw-data-reader.get-mode) поведение функции не зависит.

&nbsp;

<a name="raw-data-reader.get-rows-as-array"></a>
```js
getRowsAsArray(): RawRow[];
```
Возвращает содержимое таблицы в виде массива объектов [`RawRow`](#raw-row), где каждый элемент представляет строку таблицы.

&nbsp;

<a name="raw-data-reader.get-rows-as-object"></a>
```js
getRowsAsObject(): Record<string, RawRow>;
```
Возвращает содержимое таблицы в виде объекта, где [ключом](#raw-data-reader.get-row-key) является установленное поле заголовка строки (если заголовков несколько, они объединяются в строку с разделителем `'.'`), а значением — такой же объект строки [`RawRow`](#raw-row), какой возращает [`getRowsAsArray()`](#raw-data-reader.get-rows-as-array).

&nbsp;

<a name="raw-data-reader.get-rows-as-items"></a>
```js
getRowsAsItems(): RowFullItem[];
```
Возвращает содержимое таблицы в виде массива объектов [`RowFullItem`](#row-full-item).

&nbsp;

```js
firstEmptyRowIndex(): number;
```
Возвращает номер номер первой пустой строки таблицы. Если пустых строк нет, возвращает `-1`.

&nbsp;

<a name="raw-data-reader.refresh"></a>
```js
refresh(): this;
async refreshAsync(): Promise<this>;
```
Обновляет **заголовки** и **данные** таблицы. Если инициализирован соответствующий [`RawDataWriter`](#raw-data-writer), вызывает его функцию [`refresh()`](#raw-data-writer.refresh). Возвращает `this`.

&nbsp;

### Интерфейс RawDataWriter<a name="raw-data-writer"></a>
```ts
interface RawDataWriter {
	columns(): GridDataHeader;
	rows(): GridDataHeader;

	set(rowIds: number[], columnIds: number[], value: string | number | bool | null): this;

	apply(): this;
	async applyAsync(): Promise<this>;

	refresh(): this;
	async refreshAsync(): Promise<this>;
}
```
Интерфейс прямого доступа к данным на запись.

&nbsp;

```js
columns(): RawDataHeader;
```
Возвращает интерфейс [`RawDataHeader`](#raw-data-header) заголовков столбцов.

&nbsp;

```js
rows(): RawDataHeader;
```
Возвращает интерфейс [`RawDataHeader`](#raw-data-header) заголовков строк.

&nbsp;

<a name="raw-data-writer.set"></a>
```js
set(rowIds: number[], columnIds: number[], value: string | number | bool | null): this;
```
Устанавливает значение `value` для будущей записи в ячейку по адресу, определяемому через набор заголовков строки `rowIds` и столбца `columnIds`. Функция работает по принципу [`CellBuffer`](./common.md#cell-buffer) и **не** записывает данные в ячейку — это делает функция [`apply()`](#raw-data-writer.apply). Возвращает `this`.

&nbsp;

<a name="raw-data-writer.apply"></a>
```js
apply(): this;
async applyAsync(): Promise<this>;
```
Применяет все изменения, заданные функцией [`set()`](#raw-data-writer.set). Возвращает `this`.

&nbsp;

<a name="raw-data-writer.refresh"></a>

```js
refresh(): this;
async refreshAsync(): Promise<this>;
```
Обновляет **только заголовки** таблицы. Если инициализирован соответствующий [`RawDataReader`](#raw-data-reader), вызывает его функцию [`refresh()`](#raw-data-reader.refresh). Возвращает `this`.

&nbsp;

### Интерфейс RawDataHeader<a name="raw-data-header"></a>
```ts
interface RawDataHeader {
	count(): number;
	
	gluedHeaderIdentifiers(field: string, delim?: string): string[];

	dimensions(): HeaderDimension[];
	elementNamesByDimension(): Record<string, string[]>;

	getHeaderByIndex(index: number): RawHeaderData[] | null;
	getGluedHeaderIdentifiersByIndex(index: number, field: string, delim?: string): string | null;
	
	getLongIdsByIndex(index: number): number[] | null;
	getLongIdsByLabels(labels: string[]): number[] | null;
	
	areHeaderLongIdsValid(longIds: number[]): boolean;
}
```
Интерфейс заголовков строк или столбцов таблицы.

&nbsp;

```js
count(): number;
```
Возвращает количество заголовков – количество строк/столбцов.

&nbsp;

```js
gluedHeaderIdentifiers(field: string, delim?: string): string[];
```
Возвращает массив идентификаторов заголовков, сформированных по полю, указанному в аргументе `field`, который может принимать значение названия одного из полей [`RawHeaderData`](#raw-header-data). Если у заголовка несколько измерений, то заголовки объединяются с помощью разделителя, указанного в аргументе `delim` (по умолчанию: `'.'`). В случае некорретного значения `field` выбрасывает исключение.

**Баг!** В текущей реализации исключение не выбрасывается.

&nbsp;

```js
dimensions(): HeaderDimension[];
```
Возвращает данные измерений заголовков в виде массива объектов [`HeaderDimension`](#header-dimension).

&nbsp;

```js
elementNamesByDimension(): Record<string, string[]>;
```
Возвращает допустимые уникальные имена для каждого измерения в виде объекта, где ключами являются имена измерений.

&nbsp;

```js
getHeaderByIndex(index: number): RawHeaderData[] | null;
```
Возвращает заголовок в виде массива [`RawHeaderData`](#raw-header-data) со всеми измерениями, или `null`, если индекс некорректный.

&nbsp;

```js
getGluedHeaderIdentifiersByIndex(index: number, field: string, delim?: string): string | null;
```
То же, что и `gluedHeaderIdentifiers(field, delim)[index]`.

**Баг!** В текущей реализации позволяет не указывать или указывать некорректное поле `field`.

&nbsp;

```js
getLongIdsByIndex(index: number): number[] | null;
```
Возвращает заголовок по индексу `index` в виде массива [`longId`](./views.md#long-id) всех измерений, или `null`, если индекс некорректный.

&nbsp;

```js
getLongIdsByLabels(labels: string[]): number[] | null;
```
Возвращает заголовок в виде массива [`longId`](./views.md#long-id) по переданным полям `label` (из объекта [`RawHeaderData`](#raw-header-data)) каждого измерения, или `null`, если заголовок не найден.

&nbsp;

```js
areHeaderLongIdsValid(longIds: number[]): boolean;
```
Проверяет, является ли переданный массив `longIds` корректным определителем одного из заголовков таблицы.

&nbsp;

## Вспомогательные типы

### Тип RawHeaderData<a name="raw-header-data"></a>
```ts
type RawHeaderData = {
	label: string | null;
	id: string | null;
	longId: number;
	parentLongId: number;
	name?: string | null;
	code?: string | null;
};
```
Объект, представляющий заголовок строки или столбца таблицы.

&nbsp;

```js
label: string | null;
```
Отображаемое название.

&nbsp;

```js
id: string | null;
```
Неизвестно что.

&nbsp;

```js
longId: number;
```
[`Long id`](./views.md#long-id) заголовка.

&nbsp;

```js
parentLongId: number;
```
[`Long id`](./views.md#long-id) родительского элемента заголовка. Если его нет, здесь будет значение `-1`.

&nbsp;

```js
name?: string | null;
```
Имя заголовка. Если измерением на заголовке является справочник, это поле `'Item Name'`.

&nbsp;

```js
code?: string | null;
```
Код заголовка – поле `'code'`.

&nbsp;

### Тип HeaderDimension<a name="header-dimension"></a>
```ts
type HeaderDimension = {
	name: string;
	longId: number;
};
```
Объект, представляющий заголовок строки или столбца таблицы.

&nbsp;

```js
label: string | null;
```
Отображаемое название.

&nbsp;

```js
id: string | null;
```
То же, что и `label`.

&nbsp;

### Тип RawHeaderKey<a name="raw-header-key"></a>
```ts
type RawHeaderKey = 'label' | 'id' | 'longId';
```
Тип ключа заголовков строки или столбца таблицы. Каждый допустимый элемент типа является названием одного из полей объекта [`RawHeaderData`](#raw-header-data).

&nbsp;

### Тип RawRow<a name="raw-row"></a>
```ts
type RawRow = Record<string, string | number | null>;
```
Объект, соответствующий строке таблицы. [Ключом](#raw-data-reader.get-column-key) является установленное поле заголовка столбца. Если заголовков несколько, они объединяются в строку с разделителем `'.'`. Значением является значение ячейки, которое зависит от [режима представления](#raw-data-reader.get-mode).

&nbsp;

### Тип RowFullItem<a name="row-full-item"></a>
```ts
type RowFullItem = {
	headers: RawHeaderData[];
	values: RawRow;
};
```
Объект, представляющий строку таблицы вместе с заголовками.

&nbsp;

```js
headers: RawHeaderData[];
```
Массив заголовков строки [`RawHeaderData`](#raw-header-data).

&nbsp;

```js
values: RawRow;
```
Значения строки в виде объекта [`RawRow`](#raw-row).

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
