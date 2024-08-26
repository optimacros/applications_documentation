# Карта модели

### Тип ModelItem<a name="model-item"></a>
```ts
type ModelItem {
	longId: number;
	id: string | null;
	label: string | null;
	code: string | null;
	parentLongId: number;
}
```
Основной обобщённый тип единичного элемента модели, аналог [`Label`](./views.md#label).

&nbsp;

### Тип ModelItems<a name="model-items"></a>
```ts
type ModelItems {
  items: ModelItem[];
  count: number;
  nestingCount: number;
}
```
Коллекция элементов одного типа:
* `items` — массив элементов;
* `count` — количество элементов массива;
* `nestingCount` — пока что не используется.

&nbsp;

### Тип ModelCollection<a name="model-collection"></a>
```ts
type ModelCollection = Record<number, ModelItem[]>;
```
Коллекция элементов модели в виде объекта. Ключом являются [`longId`](./views.md#long-id) родительского объекта, а значением — массив элементов [`ModelItem`](#model-item), связанных с соответствующим элементом-родителем.

&nbsp;

### Интерфейс MulticubesMap<a name="multicubes-map"></a>
```ts
interface MulticubesMap {
	multicubes(): ModelItems;
	cubes(): ModelItems;
	cubeSubsets(): ModelItems;
	viewsOfMulticubes(): ModelCollection;
	cubesOfMulticubes(): ModelCollection;
	getCubeFormula(longId: number): string;
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных с мультикубами.

&nbsp;

```ts
multicubes(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех мультикубов.

&nbsp;

```js
cubes(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех кубов.

&nbsp;

```js
cubeSubsets(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех сабсетов кубов. 

&nbsp;

```js
viewsOfMulticubes(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) с представлениями всех мультикубов. Ключом является [`longId`](./views.md#long-id) мультикуба, а значением — массив его представлений.

&nbsp;

```js
cubesOfMulticubes(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) с кубами всех мультикубов. Ключом является [`longId`](./views.md#long-id) мультикуба, а значением — массив его кубов.

&nbsp;

```js
getCubeFormula(longId: number): string;
```
Возвращает строку с формулой куба, [`longId`](./views.md#long-id) которого передан в параметре. Если для куба не задана формула, возвращает пустую строку.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	multicubes: multicubes().items,
	cubes: cubes().items,
	cubeSubsets: cubeSubsets().items,
	viewsOfMulticubes: viewsOfMulticubes(),
	cubesOfMulticubes: cubesOfMulticubes()
}.
```

&nbsp;

### Интерфейс ListsMap<a name="lists-map"></a>
```ts
interface ListsMap {
	lists(): ModelItems;
	properties(): ModelItems;
	subsets(): ModelItems;
	viewsOfLists(): ModelCollection;
	propertiesOfLists(): ModelCollection;
	subsetsOfLists(): ModelCollection;
	subsetToParentListMap(): Object;
	getPropertyFormula(longId: longId): string;
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных со справочниками.

&nbsp;

```js
lists(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех справочников.

&nbsp;

```js
properties(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех свойств справочников.

&nbsp;

```js
subsets(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех выборок справочников.

&nbsp;

```js
viewsOfLists(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) с представлениями всех справочников. Ключом является [`longId`](./views.md#long-id) справочника, а значением — массив его представлений.

&nbsp;

```js
propertiesOfLists(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) со свойствами всех справочников. Ключом является [`longId`](./views.md#long-id) справочника, а значением — массив его свойств.

&nbsp;

```js
subsetsOfLists(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) с выборками всех справочников. Ключом является [`longId`](./views.md#long-id) справочника, а значением — массив его выборок.

&nbsp;

```js
subsetToParentListMap(): Object;
```
Возвращает объект, где ключом является [`longId`](./views.md#long-id) выборки справочника, а значением — соответствующий справочник.

&nbsp;

```js
getPropertyFormula(longId: number): string;
```
Возвращает строку с формулой свойства, [`longId`](./views.md#long-id) которого передан в параметре. Если для свойства не задана формула, возвращает пустую строку.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	lists: lists().items,
	properties: properties().items,
	subsets: subsets().items,
	viewsOfLists: viewsOfLists(),
	propertiesOfLists: propertiesOfLists(),
	subsetsOfLists: subsetsOfLists(),
	subsetToParentListMap: subsetToParentListMap()
}.
```

&nbsp;

### Интерфейс TimesMap<a name="times-map"></a>
```ts
interface TimesMap {
	labels(): string[];
	properties(): ModelCollection;
	subsets(): ModelCollection;
	periods(): ModelItem[];
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных с системными измерениями времени.

&nbsp;

```js
labels(): string[];
```
Возвращает имена измерений из перечисленных [`здесь`](./dimensions.md#times.time-period-tab), которые заданы в модели.

&nbsp;

```js
properties(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) со свойствами всех временных измерений. Ключом является [`longId`](./views.md#long-id) временного измерения, а значением — массив его свойств.

&nbsp;

```js
subsets(): ModelCollection;
```
Возвращает объект [`ModelCollection`](#model-collection) с выборками всех временных измерений. Ключом является [`longId`](./views.md#long-id) временного измерения, а значением — массив его выборок.

&nbsp;

```js
periods(): ModelItem[];
```
Возвращает массив временных периодов. Элементы массива отличаются от указанного в сигнатуре типа [`ModelItem`](#model-item) тем, что в них отсутствует поле `code`.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	labels: labels(),
	properties: properties(),
	subsets: subsets(),
	periods: periods()
}.
```

&nbsp;

### Интерфейс VersionsMap<a name="versions-map"></a>
```ts
interface VersionsMap {
	versions(): ModelItems;
	subsets(): ModelItems;
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных с системным измерением версий.

&nbsp;

```js
versions(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех версий модели.

&nbsp;

```js
subsets(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех выборок версий модели.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	versions: versions().items,
	subsets: subsets().items
}.
```

&nbsp;

### Интерфейс FoldersMap<a name="folders-map"></a>
```ts
interface FoldersMap {
	folders(): ModelItems;
	files(): ModelItems;
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных с файлами и папками модели.

&nbsp;

```js
folders(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех папок модели.

&nbsp;

```js
files(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех файлов модели.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	folders: folders().items,
	files: files().items
}.
```

&nbsp;

### Интерфейс ActionsMap<a name="actions-map"></a>
```ts
interface ActionsMap {
	actions(): ModelItems;
	toJSON(): Object;
}
```
Интерфейс, агрегирующий получение данных объектов, связанных со скриптами модели.

&nbsp;

```js
actions(): ModelItems;
```
Возвращает объект [`ModelItems`](#model-items) с массивом всех скриптов модели.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект вида
```js
{
	actions: actions().items
}.
```

&nbsp;

### Интерфейс ModelMap<a name="model-map"></a>
```ts
interface ModelMap {
	multicubesMap(): MulticubesMap;
	async multicubesMapAsync(): Promise<MulticubesMap>;
	
	listsMap(): ListsMap;
	async listsMapAsync(): Promise<ListsMap>;
	
	timesMap(): TimesMap;
	async timesMapAsync(): Promise<TimesMap>;
	
	versionsMap(): VersionsMap;
	async versionsMapAsync(): Promise<VersionsMap>;
	
	foldersMap(): FoldersMap;
	async foldersMapAsync(): Promise<FoldersMap>;
	
	actionsMap(): ActionsMap;
	async actionsMapAsync(): Promise<ActionsMap>;
	
	toJSON(): Object;
	async toJSONAsync(): Promise<Object>;
}
```
Интерфейс получения связных данных о компонентах модели.

&nbsp;

```js
multicubesMap(): MulticubesMap;
async multicubesMapAsync(): Promise<MulticubesMap>;
```
Возвращает интерфейс [`MulticubesMap`](#multicubes-map).

&nbsp;

```js
listsMap(): ListsMap;
async listsMapAsync(): Promise<ListsMap>;
```
Возвращает интерфейс [`ListsMap`](#lists-map).

&nbsp;

```js
timesMap(): TimesMap;
async timesMapAsync(): Promise<TimesMap>;
```
Возвращает интерфейс [`TimesMap`](#times-map).

&nbsp;

```js
versionsMap(): VersionsMap;
async versionsMapAsync(): Promise<VersionsMap>;
```
Возвращает интерфейс [`VersionsMap`](#versions-map).

&nbsp;

```js
foldersMap(): FoldersMap;
async foldersMapAsync(): Promise<FoldersMap>;
```
Возвращает интерфейс [`FoldersMap`](#folders-map).

&nbsp;

```js
actionsMap(): ActionsMap;
async actionsMapAsync(): Promise<ActionsMap>;
```
Возвращает интерфейс [`ActionsMap`](#actions-map).

&nbsp;

```js
toJSON(): Object;
async toJSONAsync(): Promise<Object>;
```
Возвращает объект вида
```js
{
	multicubesMap: multicubesMap().toJSON(),
	listsMap:      listsMap().toJSON(),
	timesMap:      timesMap().toJSON(),
	versionsMap:   versionsMap().toJSON(),
	foldersMap:    foldersMap().toJSON(),
	actionsMap:    actionsMap().toJSON()
}.
```


​	
&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
