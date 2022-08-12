# Измерения

### Интерфейс Lists<a name="Lists"></a>
```ts
interface Lists {
	listsTab(): ListsTab;
	syncList(): SyncListBuilder;
}
```
Интерфейс работы со справочниками.

&nbsp;

```js
listsTab(): ListsTab
```
Возвращает ссылку на интерфейс [`ListsTab`](#ListsTab). В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Справочники`.

&nbsp;

```js
syncList(): SyncListBuilder
```
```ts
`Не реализовано`
```
Возвращает интерфейс [`SyncListBuilder`](./sync.md#SyncListBuilder) синхронизации справочников.

&nbsp;

### Интерфейс ListsTab<a name="ListsTab"></a>
```ts
interface ListsTab extends Tab {
	open(name: string): ListTab;
}
```
Интерфейс для получения ссылки на [`ListTab`](#ListTab). Интерфейс наследуется от [`Tab`](./views.md#Tab). Несмотря на это, функция `open()` **не реализована**.

&nbsp;

```js
open(name: string): ListTab
```
Возвращает ссылку на [`ListTab`](#ListTab) справочника `name`. В интерфейсе Optimacros аналогично открытию вкладки справочника `name`.

&nbsp;

### Интерфейс ListTab<a name="ListTab"></a>
```ts
interface ListTab extends Tab {
	subsetTab(): ListSubsetsTab;
	propertiesTab(): ListPropertiesTab;
	accessModelTab(): ListAccessModelTab;
	importer(): ListImporter;
}
```
Вкладка справочника. Интерфейс наследуется от [`Tab`](./views.md#Tab).

&nbsp;

```js
subsetTab(): ListSubsetsTab
```
Возвращает интерфейс [`ListSubsetsTab`](#ListChildTab) доступа к вкладке выборок справочника.

&nbsp;
```js
propertiesTab(): ListPropertiesTab
```
Возвращает интерфейс [`ListPropertiesTab`](#ListChildTab) доступа к вкладке свойств справочника.

&nbsp;
```js
accessModelTab(): ListAccessModelTab
```
Возвращает интерфейс [`ListAccessModelTab`](#ListAccessModelTab) доступа к вкладке разграничения прав доступа по элементам справочника (МДП).

&nbsp;

```js
importer(): ListImporter
```
Возвращает интерфейс [`ListImporter`](#ListImporter) для импорта данных в справочник.

&nbsp;

### Интерфейс ListSubsetsTab, ListPropertiesTab (ListChildTab)<a name="ListChildTab"></a>
```ts
interface ListChildTab extends Tab {
	listTab(): ListTab;
}

interface ListSubsetsTab = ListChildTab;
interface ListPropertiesTab = ListChildTab;
```
Интерфейс доступа к дочерним вкладкам справочника. Интерфейс наследуется от [`Tab`](./views.md#Tab).

&nbsp;

```js
listTab(): ListTab
```
Возвращает интерфейс [`ListTab`](#ListTab) вкладки того справочника, чья дочерняя вкладка представляет собой `this`.

&nbsp;

### Интерфейс ListAccessModelTab<a name="ListAccessModelTab"></a>
```ts
interface ListAccessModelTab extends ListChildTab {
	isEnabled(): boolean;
}
```
Интерфейс доступа к вкладке `МДП` справочника. Интерфейс наследуется от [`ListChildTab`](#ListChildTab).

&nbsp;

```js
isEnabled(): boolean
```
Возвращает признак того, что доступ по МДП включен и вкладка доступна.

&nbsp;

### Интерфейс ListImporter<a name="ListImporter"></a>
```ts
interface ListImporter extends Importer {
	setFilePath(path: string): ListImporter;
	setObligatoryListCodes(obligatoryListCodes: boolean): ListImporter;
	getObligatoryListCodes(): boolean;
	setImportToChildListOnly(importToChildListOnly: boolean): ListImporter;
	getImportToChildListOnly(): boolean;
	setUpdatedPropertiesOnParentLevels(updatedPropertiesOnParentLevels: boolean): ListImporter;
	getUpdatedPropertiesOnParentLevels(): boolean;
}
```
Интерфейс импорта в справочник. Интерфейс наследуется от [`Importer`](./exportImport.md#Importer).

&nbsp;

```js
setFilePath(path: string): ListImporter
```
Устанавливает имя импортируемого файла. Возвращает `this`.

&nbsp;

```js
setObligatoryListCodes(obligatoryListCodes: boolean): ListImporter
```
Устанавливает режим обязательных кодов: если столбец `Code` у элемента пустой, то несуществуещие элементы не будут создаваться, но уже существующие тем не менее будут обновлены. Значение по умолчанию: `false`. Возвращает `this`.

&nbsp;

```js
getObligatoryListCodes(): boolean
```
Возвращает признак режима обязательных кодов.

&nbsp;

```js
setImportToChildListOnly(importToChildListOnly: boolean): ListImporter
```
Устанавливает режим обновления свойств `Parent` и `Code` для элементов только текущего справочника. Если аргумент `importToChildListOnly === false`, эти свойства будут обновляться также и у родительских справочников любого уровня. Значение по умолчанию: `false`. Возвращает `this`.

&nbsp;

```js
getImportToChildListOnly(): boolean
```
Возвращает признак режима обновления свойств `Parent` и `Code` для элементов только текущего справочника.

&nbsp;

```js
setUpdatedPropertiesOnParentLevels(updatedPropertiesOnParentLevels: boolean): ListImporter
```
Устанавливает режим обновления собственных свойств для элементов родительских справочников. Значение по умолчанию: `true`. Возвращает `this`.

&nbsp;

```js
getUpdatedPropertiesOnParentLevels(): boolean
```
Возвращает признак режима обновления собственных свойств для элементов родительских справочников.

&nbsp;

### Интерфейс Versions<a name="Versions"></a>
```ts
interface Versions {
	versionsTab(): VersionsTab
}
```
Интерфейс для получения ссылки на [`VersionsTab`](#VersionsTab).

&nbsp;

```js
versionsTab(): VersionsTab
```
Возвращает ссылку на вкладку [`VersionsTab`](#VersionsTab) настроек версий. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Версии`.

&nbsp;

### Интерфейс VersionsTab<a name="VersionsTab"></a>
```ts
interface VersionsTab extends Tab {
	copyVersion(from: string, to: string): Object;
}
```
Вкладка `Версии`. Интерфейс наследуется от [`Tab`](./views.md#Tab). Для работы не требует открытия.

&nbsp;

```js
copyVersion(from: string, to: string): Object
```
Копирует срез по версии `from` в срез по версии `to` во всех мультикубах модели, которые имеют измерение версий, включающее обе эти версии. Возвращает объект вида `{"success": true}`.

&nbsp;

### Интерфейс Times<a name="Times"></a>
```ts
interface Times {
	optionsTab(): TimeOptionsTab;
	timePeriodTab(identifier: string | number): TimePeriodTab;
}
```
Интерфейс для получения доступа к вкладкам измерения `Время`.

&nbsp;

```js
optionsTab(): TimeOptionsTab
```
Возвращает ссылку на вкладку [`TimeOptionsTab`](#TimeOptionsTab) настроек времени. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время`.

&nbsp;

```js
timePeriodTab(identifier: string | number): TimePeriodTab
```
Возвращает ссылку на вкладку [`TimePeriodTab`](#TimePeriodTab) периодов времени. В интерфейсе Optimacros аналогично открытию вкладки `Время` -> `Период времени`. Период времени передается параметром `identifier` в формате идентификатора вкладки или строки: `Days`, `Weeks`, `Periods`, `Months`, `Quarters`, `Half Years`, `Years`.

&nbsp;

### Интерфейс TimeOptionsTab<a name="TimeOptionsTab"></a>
```ts
interface TimeOptionsTab extends Tab{
	resetForm(): Object;
	applyForm(): Object;
}
```
Вкладка `Время`. Интерфейс наследуется от [`Tab`](./views.md#Tab). Для работы не требует открытия. Является [`плоской таблицей`](../appendix/constraints.md#flatTable). Кроме того, является формой, аналогичной форме HTML: после изменения значений ячейки/ячеек требуется ещё вызвать функцию `applyForm()` для применения новых данных к модели.

&nbsp;

```js
resetForm(): Object
```
Сбрасывает все изменения данных во вкладке. Возвращает объект вида `{"success": true}`.

&nbsp;

```js
applyForm(): Object
```
Применяет все изменения данных. Возвращает объект вида `{"success": true}`.

&nbsp;

### Интерфейс TimePeriodTab<a name="TimePeriodTab"></a>
```ts
interface TimePeriodTab extends Tab{
	subsetsTab(): TimePeriodSubsetTab;
}
```
Вкладка периодов времени. Интерфейс наследуется от [`Tab`](./views.md#Tab). Для работы не требует открытия.

&nbsp;

```js
subsetsTab(): TimePeriodSubsetTab
```
Возвращает ссылку на вкладку [`TimePeriodSubsetTab`](#TimePeriodSubsetTab) сабсетов времени.

&nbsp;

### Интерфейс TimePeriodSubsetTab<a name="TimePeriodSubsetTab"></a>
```ts
interface TimePeriodSubsetTab extends Tab{
}
```
Вкладка сабсетов времени. Интерфейс наследуется от [`Tab`](./views.md#Tab). Для работы не требует открытия.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
