# Вкладка скриптов

### Тип ModelScriptItem<a name="model-script-item"></a>
```ts
type ModelScriptItem = {
	name: string;
	longId: number;
	Macros: string;
	Folder: string | null;
	Scheduler: string;
	'Lock Mode': 'Unique' | 'Shared' | 'Custom';
	'Memory Limit, MB': number;
	'Time Limit, sec': number;
	'Custom Offset': number;
	Comments: string | null;
};
```
Тип объекта скрипта, возвращаемый MiddleWork.

&nbsp;

### Тип RunScriptResult<a name="run-script-result"></a>
```ts
type RunScriptResult {
	output: string;
	success?: boolean;
	files: string[];
}
```
Тип, возвращаемый после выполнения скрипта. Поле `output` содержит вывод скрипта, поле `success` — признак успешного выполнения, `files` – массив хэшей файлов, которые скрипт отдаст пользователю на скачивание в браузере.

&nbsp;

### Интерфейс ScriptsTab<a name="scripts-tab"></a>
```ts
interface ScriptsTab {
	scriptNames(): string[];
	
	items(): ModelScriptItem[];
	async itemsAsync(): Promise<ModelScriptItem[]>;

	openScript(scriptName: string): Script | null;
	async openScriptAsync(scriptName: string): Promise<Script | null>;

	addScript(scriptName: string, position?: string): this;
	async addScriptAsync(scriptName: string, position?: string): Promise<this>;
	
	deleteScript(scriptName: string): ScriptsTab;
	async deleteScriptAsync(scriptName: string): Promise<ScriptsTab>;
	
	runScript(scriptName: string): RunScriptResult;
	async runScriptAsync(scriptName: string): Promise<RunScriptResult>;
	
	toJSON(): Object;
}
```
Вкладка `Скрипты`. Вопреки названию интерфейс **не** наследуется от [`Tab`](./views.md#tab) и **не** реализует функцию [`pivot()`](./views.md#tab.pivot). В интерфейсе Optimacros аналогично открытию вкладки `Макросы` -> `Скрипты`.

&nbsp;

```js
scriptNames(): string[];
```
Возвращает имена всех скриптов модели. Не требует дополнительных запросов к MiddleWork.

&nbsp;

```js
items(): ModelScriptItem[];
async itemsAsync(): Promise<ModelScriptItem[]>;
```
Возвращает массив скриптов модели в виде типа [`ModelScriptItem`](#model-script-item).

&nbsp;

```js
openScript(scriptName: string): Script | null;
async openScriptAsync(scriptName: string): Promise<Script | null>;
```
Возвращает интерфейс [`Script`](#script) для скрипта `scriptName`. Если скрипта с таким именем нет в модели, возвращает `null`.

&nbsp;

```js
addScript(scriptName: string, position?: string): this;
async addScriptAsync(scriptName: string, position?: string): Promise<this>;
```
Создаёт новый скрипт с именем `scriptName`. Аргумент `position` определяет позицию скрипта в таблице скриптов. Он может принимать значения `"Start"` и `"End"`. Значение по умолчанию: `"End"`. Возвращает `this`.

&nbsp;

```js
deleteScript(scriptName: string): this;
async deleteScriptAsync(scriptName: string): Promise<this>;
```
Удаляет скрипт `scriptName`. Возвращает `this`.

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

### Интерфейс Script<a name="script"></a>
```ts
interface Script {
	name(): string;
	longId(): number;
	isModified(): boolean;
	
	getMacros(): string;
	setMacros(macros: string): this;
	
	getFolder(): string | null;
	setFolder(folder: string | null): this;
	
	getScheduler(): string;
	setScheduler(scheduler: string): this;
	
	getLockMode(): string;
	setLockMode(lockMode: string): this;
	
	getMemoryLimit(): number;
	setMemoryLimit(memoryLimit: number): this;
	
	getTimeLimit(): number;
	setTimeLimit(timeLimit: number): this;
	
	getCustomOffset(): number;
	setCustomOffset(customOffset: number): this;
	
	getComments(): string | null;
	setComments(comments: string | null): this;
	
	save(): boolean;
	async saveAsync(): Promise<boolean>;
	
	run(): RunScriptResult;
	async runAsync(): Promise<RunScriptResult>;
	
	toJSON(): ModelScriptItem;
}
```
Интерфейс скрипта как объекта модели Optimacros во вкладке `Скрипты`.

&nbsp;

```js
name(): string;
```
Возвращает имя скрипта.

&nbsp;

```js
longId(): number;
```
Возвращает [`longId`](./views.md#long-id) скрипта.

&nbsp;
```js
isModified(): boolean;
```
Возвращает признак того, что данные скрипта были изменены по сравнению с предыдущим сохранением или чтением из модели.

&nbsp;

```js
getMacros(): string;
```
Возвращает значение столбца `Macros`.

&nbsp;

```js
setMacros(macros: string): this;
```
Готовит для записи значение столбца `Macros` — код скрипта. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getFolder(): string | null;
```
Возвращает значение столбца `Folder`.

&nbsp;

```js
setFolder(folder: string | null): this;
```
Готовит для записи значение столбца `Folder` — папка, в которой находится скрипт. Если скрипт отображается в папке `Other contents` (`Прочее содержимое`), это значит, что он фактически не находится ни в какой папке, и это соответствует значению `null`. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getScheduler(): string;
```
Возвращает значение столбца `Scheduler`.

&nbsp;

```js
setScheduler(string): this;
```
Готовит для записи значение столбца `Scheduler` — режим планировщика. Это должна быть строка в формате [`cron`](https://ru.wikipedia.org/wiki/cron). Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getLockMode(): string;
```
Возвращает значение столбца `Lock Mode`.

&nbsp;

```js
setLockMode(lockMode: string): this;
```
Готовит для записи значение столбца `Lock Mode` — режим блокировки скрипта. Возможные значения: `'Unique'`, `'Shared'`, `'Custom'`. Подробнее о режимах блокировки — в [документации](https://github.com/optimacros/scripts_documentation/blob/main/advancedFeatues/modelLock.md) на скрипты модели. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getMemoryLimit(): number;
```
Возвращает значение столбца `Memory Limit, MB`.

&nbsp;

```js
setMemoryLimit(memoryLimit: number): this;
```
Готовит для записи значение столбца `Memory Limit, MB` — лимит памяти скрипта. Подробнее о лимитах — в [документации](https://github.com/optimacros/scripts_documentation/blob/main/advancedFeatues/limits.md) на скрипты модели. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getTimeLimit(): number;
```
Возвращает значение столбца `Time Limit, sec`.

&nbsp;

```js
setTimeLimit(timeLimit: number): this;
```
Готовит для записи значение столбца `Time Limit, sec` — лимит времени исполнения скрипта. Подробнее о лимитах — в [документации](https://github.com/optimacros/scripts_documentation/blob/main/advancedFeatues/limits.md) на скрипты модели. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getCustomOffset(): number;
```
Возвращает значение столбца `Custom Offset`.

&nbsp;

```js
setCustomOffset(customOffset: number): this;
```
Готовит для записи значение столбца `Custom Offset` — количество пробелов перед именем скрипта в первом столбце. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

```js
getComments(): string | null;
```
Возвращает значение столбца `Comments`. В случае отсутствия комментария возвращает не пустую строку, а `null`.

&nbsp;

```js
setComments(comments: string | null): this;
```
Готовит для записи значение столбца `Comments`. Фактическую запись в модель производит функция [`save()/saveAsync()`](#script.save). Возвращает `this`.

&nbsp;

<a name="script.save"></a>
```js
save(): boolean;
async saveAsync(): Promise<boolean>;
```
Сохраняет скрипт в модели с текущими параметрами. Возвращает признак успешной записи.

&nbsp;

```js
run(): RunScriptResult;
async runAsync(): Promise<RunScriptResult>;
```
Запускает скрипт. Возвращает объект типа [`RunScriptResult`](#run-script-result).

&nbsp;

```js
toJSON(): ModelScriptItem;
```
Возвращает данные скрипта в виде объекта [`ModelScriptItem`](#model-script-item).

&nbsp;

### Тип FileBase64Info <a name="file-base64-info"></a>
```ts
type FileBase64Info {
	name: string;
	content: string;
}
```
Объект, содержащий информацию о файле: поле `name` – его имя, поле `content` — содержимое, зашифрованное по схеме [`base64`](https://ru.wikipedia.org/wiki/Base64).

&nbsp;

### Интерфейс FilesContent <a name="files-content"></a>
```ts
interface FilesContent {
	getFiles(...files: string[]): FileBase64Info[];
	getFilesAsync(...files: string[]): Promise<FileBase64Info[]>;
}
```
Интерфейс для получения файлов из скриптов модели.

&nbsp;

```js
getFiles(...files: string[]): FileBase64Info[];
getFilesAsync(...files: string[]): Promise<FileBase64Info[]>;
```
Принимает список хэшей файлов, которые могут быть получены в скрипте, как правило, функцией скриптов 1.0 `Filesystem`.[`makeGlobalFile()`](https://github.com/optimacros/scripts_documentation/blob/main/API/fs.md#filesystem.make-global-file). Возвращает массив объектов [`FileBase64Info`](#file-base64-info) с информацией об этих файлах.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
