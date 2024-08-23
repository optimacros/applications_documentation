# Вкладка папок

### Тип TreeItem<a name="tree-item"></a>
```ts
type TreeItem = {
	name: string | null;
	longId: number;
	parentEntityLongId: number;
	subItems: TreeItem[];
};
```
Элемент древовидной структуры папок модели.

&nbsp;

### Тип ModelFolderItem<a name="model-folder-item"></a>
```ts
type ModelFolderItem = {
	name: string | null;
	longId: number;
	'Parent Folder': string | null;
	Comments: string | null;
};
```
Тип объекта папки.

&nbsp;

### Интерфейс FoldersTab<a name="folders-tab"></a>
```ts
interface FoldersTab {
	names(): string[];
	tree(): TreeItem;
	
	items(): ModelFolderItem[];
	async itemsAsync(): Promise<ModelFolderItem[]>;

	addFolder(folderName: string, position: string): boolean;
	async addFolderAsync(folderName: string, position: string): Promise<boolean>;
	
	deleteFolder(folderName: string): boolean;
	async deleteFolderAsync(folderName: string): Promise<boolean>;
	
	setParentFolder(folderName: string, parentName: StringOrNull): boolean;
	async setParentFolderAsync(folderName: string, parentName: StringOrNull): Promise<boolean>;
	
	toJSON(): Object;
}
```
Вкладка `Папки`. Вопреки названию интерфейс **не** наследуется от [`Tab`](./views.md#tab) и **не** реализует функцию [`pivot()`](./views.md#tab.pivot). В интерфейсе Optimacros аналогично открытию вкладки `Визуализация` -> `Папки`.

&nbsp;

```js
names(): string[];
```
Возвращает имена папок модели. Не требует дополнительных запросов к MiddleWork.

&nbsp;

```js
tree(): TreeItem;
```
Возвращает корень дерева структуры папок модели в виде типа [`TreeItem`](#tree-item).

&nbsp;

```js
items(): ModelFolderItem[];
async itemsAsync(): Promise<ModelFolderItem[]>;
```
Возвращает массив папок модели в виде типа [`ModelFolderItem`](#model-folder-item).

&nbsp;

```js
addFolder(folderName: string, position: string): boolean;
async addFolderAsync(folderName: string, position: string): Promise<boolean>;
```
Создаёт новую папку  с именем `folderName`. Аргумент `position` определяет её позицию в списке папок верхнего уровня. Допустимые значения: `'Start'` и `'End'`. Значение по умолчанию: `'End'`. Возвращает результат выполнения.

&nbsp;

```js
deleteFolder(folderName: string): boolean;
async deleteFolderAsync(folderName: string): Promise<boolean>;
```
Удаляет папку `folderName`. Возвращает результат выполнения.

&nbsp;

```js
setParentFolder(folderName: string, parentName: StringOrNull): boolean;
async setParentFolderAsync(folderName: string, parentName: StringOrNull): Promise<boolean>;
```
Устанавливает папку `parentName` в качестве родительской папки для `folderName`. Возвращает результат выполнения.

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект 
`{
	names: names(),
	tree:  tree()
}`.


&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
