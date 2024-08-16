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
	folderNames(): string[];
	folderTree(): TreeItem;
	
	items(): ModelFolderItem[];
	async itemsAsync(): Promise<ModelFolderItem[]>;

	# addScript(scriptName: string, position?: string): this;
	# async addScriptAsync(scriptName: string, position?: string): Promise<this>;
	
	deleteFolder(folderName: string): this;
	async deleteFolderAsync(folderName: string): Promise<this>;
	
	setFolderParent(folderName: string, parentName: StringOrNull): boolean;
	async setFolderParentAsync(folderName: string, parentName: StringOrNull): Promise<boolean>;
	
	toJSON(): Object;
}
```
Вкладка `Папки`. Вопреки названию интерфейс **не** наследуется от [`Tab`](./views.md#tab) и **не** реализует функцию [`pivot()`](./views.md#tab.pivot). В интерфейсе Optimacros аналогично открытию вкладки `Визуализация` -> `Папки`.

&nbsp;

```js
folderNames(): string[];
```
Возвращает имена папок модели. Не требует дополнительных запросов к MiddleWork.

&nbsp;

```js
folderTree(): TreeItem;
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
# addScript(scriptName: string, position?: string): this;
# async addScriptAsync(scriptName: string, position?: string): Promise<this>;
```
Создаёт новый скрипт с именем `scriptName`. Аргумент `position` определяет позицию скрипта в таблице скриптов. Он может принимать значения `"Start"` и `"End"`. Значение по умолчанию: `"End"`. Возвращает `this`.

&nbsp;

```js
deleteFolder(folderName: string): this;
async deleteFolderAsync(folderName: string): Promise<this>;
```
Удаляет папку `folderName`. Возвращает `this`.

&nbsp;

```js
runScript(scriptName: string): RunScriptResult;
async runScriptAsync(scriptName: string): Promise<RunScriptResult>;
```
Запускает скрипт. Возвращает объект типа [`RunScriptResult`](#run-script-result).

&nbsp;

```js
toJSON(): Object;
```
Возвращает объект `{ scripts: this.scriptNames() }`.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
