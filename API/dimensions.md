# Измерения

### Интерфейс Lists<a name="lists"></a>
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
Возвращает ссылку на интерфейс [`ListsTab`](#lists-tab). В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Справочники`.

&nbsp;

```js
syncList(): SyncListBuilder
```
***Не реализовано.***

Возвращает интерфейс [`SyncListBuilder`](./sync.md#sync-list-builder) синхронизации справочников.

&nbsp;

### Интерфейс ListsTab<a name="lists-tab"></a>
```ts
interface ListsTab extends Tab {
	open(name: string): ListTab;
	elementsCreator(): ElementsCreator;
}
```
Вкладка `Справочники`. Интерфейс наследуется от [`Tab`](./views.md#tab).

&nbsp;

```js
open(name: string): ListTab
```
Возвращает ссылку на [`ListTab`](#list-tab) справочника `name`. Если такой справочник отсутствует, бросает исключение. В интерфейсе Optimacros аналогично открытию вкладки справочника `name`.

&nbsp;

```js
elementsCreator(): ElementsCreator
```

Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

### Интерфейс ListTab<a name="list-tab"></a>
```ts
interface ListTab extends Tab {
	subsetTab(): ListSubsetsTab;
	propertiesTab(): ListPropertiesTab;
	accessModelTab(): ListAccessModelTab;
	
	elementsCreator(): ElementsCreator;
	elementsDeleter(): ElementsDeleter;
	
	importer(): ListImporter;
}
```
Вкладка справочника. Интерфейс наследуется от [`Tab`](./views.md#tab).

&nbsp;

```js
subsetTab(): ListSubsetsTab
```
Возвращает ссылку на интерфейс [`ListSubsetsTab`](#list-child-tab) доступа к вкладке выборок справочника. В интерфейсе Optimacros аналогично открытию вкладки `Выборки` справочника `name`.

&nbsp;
```js
propertiesTab(): ListPropertiesTab
```
Возвращает ссылку на интерфейс [`ListPropertiesTab`](#list-child-tab) доступа к вкладке свойств справочника. В интерфейсе Optimacros аналогично открытию вкладки `Свойства` справочника `name`.

&nbsp;
```js
accessModelTab(): ListAccessModelTab
```
Возвращает ссылку на интерфейс [`ListAccessModelTab`](#list-access-model-tab) доступа к вкладке разграничения прав доступа по элементам справочника (МДП).

&nbsp;

```js
elementsCreator(): ElementsCreator
```

Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

```js
elementsDeleter(): ElementsDeleter
```
Возвращает ссылку на [`ElementsDeleter`](./elementsManipulator.md#elements-deleter) для удаления элементов.

&nbsp;

```js
importer(): ListImporter
```
Возвращает ссылку на интерфейс [`ListImporter`](./exportImport.md#list-importer) для импорта данных в справочник.

&nbsp;

### Интерфейс ListSubsetsTab, ListPropertiesTab (ListChildTab)<a name="list-child-tab"></a>
```ts
interface ListChildTab extends Tab {
	listTab(): ListTab;
	elementsCreator(): ElementsCreator;
}

interface ListSubsetsTab = ListChildTab;
interface ListPropertiesTab = ListChildTab;
```
Интерфейс доступа к дочерним вкладкам справочника. Интерфейс наследуется от [`Tab`](./views.md#tab).

&nbsp;

```js
listTab(): ListTab
```
Возвращает интерфейс [`ListTab`](#list-tab) вкладки того справочника, чья дочерняя вкладка представляет собой `this`.

&nbsp;

```js
elementsCreator(): ElementsCreator
```
Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

### Интерфейс ListAccessModelTab<a name="list-access-model-tab"></a>
```ts
interface ListAccessModelTab extends ListChildTab {
	isEnabled(): boolean;
}
```
Интерфейс доступа к вкладке `МДП` справочника. Интерфейс наследуется от [`ListChildTab`](#list-child-tab).

&nbsp;

```js
isEnabled(): boolean
```
Возвращает признак того, что доступ по МДП включен и вкладка доступна.

&nbsp;

### Интерфейс Versions<a name="versions"></a>
```ts
interface Versions {
	versionsTab(): VersionsTab;
	versionSubsetsTab(): VersionSubsetsTab;
}
```
Интерфейс для получения доступа к вкладкам измерения `Версии`.

&nbsp;

```js
versionsTab(): VersionsTab
```
Возвращает ссылку на вкладку [`VersionsTab`](#versions-tab) настроек версий. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Версии`.

&nbsp;

```js
versionSubsetsTab(): VersionSubsetsTab
```
Возвращает ссылку на вкладку [`VersionSubsetsTab`](#version-subsets-tab) выборок версий. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Версии` -> `Выборки`.

&nbsp;

### Интерфейс VersionsTab<a name="versions-tab"></a>
```ts
interface VersionsTab extends Tab {
	elementsCreator(): ElementsCreator;
	copyVersion(from: string, to: string): Object;
}
```
Вкладка `Версии`. Интерфейс наследуется от [`Tab`](./views.md#tab).

&nbsp;

```js
elementsCreator(): ElementsCreator
```
Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

```js
copyVersion(from: string, to: string): Object
```
***Не реализовано.***

Копирует срез по версии `from` в срез по версии `to` во всех мультикубах модели, которые имеют измерение версий, включающее обе эти версии. Возвращает объект вида `{"success": true}`.

&nbsp;

### Интерфейс VersionSubsetsTab<a name="version-subsets-tab"></a>
```ts
interface VersionSubsetsTab extends Tab {
	elementsCreator(): ElementsCreator;
}
```
Вкладка `Выборки` версий. Интерфейс наследуется от [`Tab`](./views.md#tab).

&nbsp;

```js
elementsCreator(): ElementsCreator
```
Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

### Интерфейс Times<a name="times"></a>
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
Возвращает ссылку на вкладку [`TimeOptionsTab`](#time-options-tab) настроек времени. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время`.

&nbsp;

```js
timePeriodTab(identifier: string | number): TimePeriodTab
```
Возвращает ссылку на вкладку [`TimePeriodTab`](#time-period-tab) измерения времени `identifier`. Доступны измерения `Days`, `Weeks`, `Periods`, `Months`, `Quarters`, `Half Years`, `Years`. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время` -> `identifier`.

&nbsp;

### Интерфейс TimeOptionsTab<a name="time-options-tab"></a>
```ts
interface TimeOptionsTab extends Tab {
	resetForm(): Object;
	applyForm(): Object;
}
```
Вкладка `Время`. Интерфейс наследуется от [`Tab`](./views.md#tab) Является [`плоской таблицей`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#flat-table). Кроме того, является формой, аналогичной форме HTML: после изменения значений ячейки/ячеек требуется ещё вызвать функцию `applyForm()` для применения новых данных к модели.

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

### Интерфейс TimePeriodTab<a name="time-period-tab"></a>
```ts
interface TimePeriodTab extends Tab {
	subsetsTab(): TimePeriodSubsetTab;
}
```
Вкладка выбранного измерения времени. Интерфейс наследуется от [`Tab`](./views.md#tab). В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время` -> `identifier`.

&nbsp;

```js
subsetsTab(): TimePeriodSubsetTab
```
Возвращает ссылку на вкладку [`TimePeriodSubsetTab`](#time-period-subset-tab) выборок выбранного измерения времени. В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время` -> `{выбранное измерение времени}` -> `Выборки`.

&nbsp;

### Интерфейс TimePeriodSubsetTab<a name="time-period-subset-tab"></a>
```ts
interface TimePeriodSubsetTab extends Tab {
	elementsCreator(): ElementsCreator;
}
```
Интерфейс доступа к вкладке `Выборки` выбранного измерения времени. Интерфейс наследуется от [`Tab`](./views.md#tab). В интерфейсе Optimacros аналогично открытию вкладки `Измерения` -> `Время` -> `{выбранное измерение времени}` -> `Выборки`.

&nbsp;

```js
elementsCreator(): ElementsCreator
```
***Не реализовано.***

Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления элементов.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
