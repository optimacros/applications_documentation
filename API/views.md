# Представления

### Интерфейс Multicubes<a name="multicubes"></a>
```ts
interface Multicubes {
	multicubesTab(): MulticubesTab;
	syncMulticube(): SyncMulticubeBuilder;
}
```
Интерфейс работы с мультикубами.

&nbsp;

```js
multicubesTab(): MulticubesTab
```
Возвращает ссылку на интерфейс [`MulticubesTab`](#multicubes-tab). В интерфейсе Optimacros аналогично открытию вкладки `Данные` -> `Мультикубы`.

&nbsp;

```js
syncMulticube(): SyncMulticubeBuilder
```
***Не реализовано.***

Возвращает интерфейс [`SyncMulticubeBuilder`](./sync.md#sync-multicube-builder) синхронизации мультикубов.

&nbsp;

### Интерфейс MulticubesTab<a name="multicubes-tab"></a>
```ts
interface MulticubesTab extends Tab {
	open(name: string): MulticubeTab;
   
	elementsCreator(): ElementsCreator;
	elementsDeleter(): ElementsDeleter;
}
```
Вкладка `Мультикубы`. Интерфейс наследуется от [`Tab`](#tab).

&nbsp;

```js
open(name: string): MulticubeTab
```
Возвращает ссылку на [`MulticubeTab`](#multicube-tab) куба `name`. Если такой мультикуб отсутствует, бросает исключение. В интерфейсе Optimacros аналогично открытию вкладки мультикуба `name`.

&nbsp;

```js
elementsCreator(): ElementsCreator
```

Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для создания мультикубов.

&nbsp;

```js
elementsDeleter(): ElementsDeleter
```

Возвращает ссылку на [`ElementsDeleter`](./elementsManipulator.md#elements-deleter) для удаления мультикубов.

### Интерфейс Tab<a name="tab"></a>

```ts
interface Tab {
	pivot(viewName?: string): Pivot;
}
```
Базовый интерфейс для вкладок.

&nbsp;

<a name="tab.pivot"></a>
```js
pivot(viewName?: string): Pivot
```
Возвращает ссылку на интерфейс [`Pivot`](#pivot) представления `viewName` текущего мультикуба. Если `viewName` не задано, используется представление по умолчанию. Эта функция — ***единственный*** способ получить доступ к представлению мультикуба в скриптах. Возможность программно задать строки, колонки и фильтры для создания представления мультикуба [*отсутствует*](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#pivot), поэтому для работы с нужным представлением через скрипт необходимо заранее создать и сохранить его вручную.

&nbsp;

### Интерфейс MulticubeTab<a name="multicube-tab"></a>
```ts
interface MulticubeTab extends Tab {
	cleanCellsData(cubesIdentifiers?: number[]): MulticubeTab;
	cubeCellSelector(identifier: string | number): CubeCellSelectorBuilder;
	cubeCellUpdater(identifier: string | number): CubeCellUpdaterBuilder;
	
	getCubeInfo(identifier: string | number): CubeInfo;
	async getCubeInfoAsync(identifier: string | number): Promise<CubeInfo>;
	
	cubesTab(): CubesTab;
	
	importer(): MulticubeImporter;
	storageImporter(): StorageImporter;
}
```
Вкладка мультикуба. Интерфейс наследуется от [`Tab`](#tab).

&nbsp;

```js
cleanCellsData(cubesIdentifiers?: number[]): MulticubeTab
```
***Не реализовано.***

Очищает всё содержимое кубов `cubesIdentifiers` или весь мультикуб при вызове без параметров. Возвращает `this`.

&nbsp;

```js
cubeCellSelector(identifier: string | number): CubeCellSelectorBuilder
```
***Не реализовано.***

Возвращает интерфейс [`CubeCellSelectorBuilder`](./cubeCell.md#cube-cell-selector-builder) выборки клеток для куба `identifier`.

&nbsp;

```js
cubeCellUpdater(identifier: string | number): CubeCellUpdaterBuilder
```
Возвращает интерфейс [`CubeCellUpdaterBuilder`](./cubeCell.md#cube-cell-updater-builder) обновления клеток куба с именем или идентификатором `identifier` по формуле.

&nbsp;

```js
getCubeInfo(identifier: string | number): CubeInfo
async getCubeInfoAsync(identifier: string | number): Promise<CubeInfo>
```
Возвращает интерфейс [`CubeInfo`](./cubeCell.md#cube-info) для получения информации о кубе `identifier`.

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

```js
cubesTab(): CubesTab
```
Возвращает интерфейс [`CubesTab`](#cubes-tab) доступа к режиму редактирования мультикуба.

&nbsp;

```js
importer(): MulticubeImporter
```
Возвращает интерфейс [`MulticubeImporter`](./exportImport.md#multicube-importer) для импорта данных в мультикуб.

&nbsp;

```js
storageImporter(): StorageImporter
```
Возвращает ссылку на интерфейс быстрого импорта [`StorageImporter`](./exportImport.md#storage-importer).

&nbsp;

### Интерфейс CubesTab<a name="cubes-tab"></a>
```ts
interface CubesTab extends Tab {
	elementsCreator(): ElementsCreator;
	elementsDeleter(): ElementsDeleter;
}
```
Интерфейс доступа к кубам мультикуба. В интерфейсе Optimacros аналогично открытию вкладки `Режим редактирования` мультикуба. Наследуется от интерфейса [`Tab`](#tab).

&nbsp;

```js
elementsCreator(): ElementsCreator
```
Возвращает ссылку на [`ElementsCreator`](./elementsManipulator.md#elements-creator) для добавления кубов.

&nbsp;

```js
elementsDeleter(): ElementsDeleter
```
***Не реализовано.***

Возвращает ссылку на [`ElementsDeleter`](./elementsManipulator.md#elements-deleter) для удаления кубов.

&nbsp;

### Интерфейс Pivot<a name="pivot"></a>
```ts
interface Pivot {
	create(): Grid;
	async createAsync(): Promise<Grid>;
	
	rowsFilter(data: string | string[] | number | number[]): Pivot;
	columnsFilter(data: string | string[] | number | number[]): Pivot;
	
	withoutValues(): Pivot;
	addDependentContext(identifier: number): Pivot;
}
```
Интерфейс представления (сводной таблицы) мутилькуба. Функции интерфейса настраивают будущее отображение таблицы и ***не*** запрашивают данные мультикуба.

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

```js
create(): Grid
async createAsync(): Promise<Grid>
```
Возвращает ссылку на [`Grid`](#grid) настроенного представления мультикуба.

&nbsp;

<a name="rows-filter"></a>
```js
rowsFilter(data: string | string[] | number | number[]): Pivot
```
Позволяет задать для отображения множество строк и скрыть остальные. Множество можно задать следующими способами:

`string` — название строки;

`string[]` — массив названий строк;

`number` — [`longId`](#long-id) строки;

`number[]` — массив [`longId`](#long-id) строк.

Возвращает `this`.

&nbsp;

```js
columnsFilter(data: string | string[] | number | number[]): Pivot
```
Аналог [`rowsFilter()`](#rows-filter) для столбцов.

&nbsp;

```js
withoutValues(): Pivot
```
Устанавливает признак загрузки с сервера данных о мультикубе без значений ячеек. В этом случае функции интерфейса [`Cell`](#cell) [`getValue()`](#cell.get-value), [`getNativeValue()`](#cell.get-native-value) и [`getContextValue()`](#get-context-value) будут возвращать `null`, однако функции [`Cell`](#cell).[`setValue()`](#cell.set-value), [`Cells`](#cells).[`setValue()`](#cells.set-value) и [`CellBuffer`](./common.md#cell-buffer).[`apply()`](#apply) не теряют свою магическую силу. Возвращает `this`.

Эта функция существенно ускоряет работу с мультикубами в тех случаях, когда нужно записать данные, но не читать их.

&nbsp;

<a name="add-dependent-context"></a>
```js
addDependentContext(identifier: number): Pivot
```
Добавляет в фильтр по строкам весь зависимый контекст переданного [`longId`](#long-id) `identifier`: материнские и дочерние элементы всех уровней.

Если эта функция многократно вызывается с аргументами, один из которых является потомком остальных (порядок вызовов не имеет значения), то это считается уточнением запроса, и результат будет равносилен однократному вызову с этим аргументом.

Если для полученного [`Grid`](#grid) установлен фильтр [`GridPageSelector`](#grid-page-selector) (или несколько), а `identifier` — это [`longId`](#long-id) элемента измерения одного из этих фильтров, то в соответствующем фильтре будет программно установлен этот элемент.

Возвращает `this`.

&nbsp;

### Интерфейс Grid<a name="grid"></a>
```ts
interface Grid {
	range(rowStart?: number, rowCount?: number, columnStart?: number, columnCount?: number): GridRange;

	rowCount(): number;
	columnCount(): number;
	cellCount(): number;

	getDefinitionInfo(): GridDefinitionInfo;
	exporter(): Exporter;
	storageExporter(): StorageExporter;
}
```
Интерфейс таблицы.

&nbsp;

<a name="range"></a>
```js
range(rowStart?: number, rowCount?: number, columnStart?: number, columnCount?: number): GridRange
```
Возвращает интерфейс [`GridRange`](#grid-range), представляющий прямоугольный диапазон ячеек.

Аргументы `rowStart` и `columnStart` задают начальные номера строки и столбца соответственно. Значения по умолчанию: `0`.
Аргументы `rowCount` и `columnCount` задают количество строк и столбцов соответственно. Особое значение этих аргументов `-1` означает захват всех строк/столбцов до конца таблицы. Значения по умолчанию: `-1`.

Пример: `grid.range(0, -1, 0, -1)` означает захват всех ячеек таблицы.

&nbsp;

```js
rowCount(): number
```
Возвращает количество строк в таблице.

&nbsp;

```js
columnCount(): number
```
Возвращает количество колонок в таблице.

&nbsp;

```js
cellCount(): number
```
Возвращает количество ячеек в таблице. Эквивалентно `rowCount() * columnCount()`.

&nbsp;

```js
getDefinitionInfo(): GridDefinitionInfo
```
Возвращает ссылку на интерфейс [`GridDefinitionInfo`](#grid-definition-info).

&nbsp;

```js
exporter(): Exporter
```
Возвращает ссылку на интерфейс [`Exporter`](./exportImport.md#exporter) базового экспорта таблицы.

&nbsp;

```js
storageExporter(): StorageExporter
```
Возвращает ссылку на интерфейс [`StorageExporter`](./exportImport.md#storage-exporter) быстрого экспорта таблицы.

&nbsp;

### Интерфейс GridDefinitionInfo<a name="grid-definition-info"></a>
```ts
interface GridDefinitionInfo {
	getPageSelectors(): GridPageSelector[];
	getRowDimensions(): GridDimension[];
	getColumnDimensions(): GridDimension[];
}
```
Интерфейс, предоставляющий метаданные о таблице [`Grid`](#grid).

&nbsp;

```js
getPageSelectors(): GridPageSelector[]
```
Возвращает массив интерфейсов [`GridPageSelector`](#grid-page-selector), которые представляют метаданные о фильтрах таблицы.

&nbsp;

<a name="grid-definition-info.get-row-dimensions"></a>
```js
getRowDimensions(): GridDimension[]
```
Возвращает массив интерфейсов [`GridDimension`](#grid-dimension), которые представляют метаданные о строках таблицы.

&nbsp;

<a name="grid-definition-info.get-column-dimensions"></a>
```js
getColumnDimensions(): GridDimension[]
```
Возвращает массив интерфейсов [`GridDimension`](#grid-dimension), которые представляют метаданные о столбцах таблицы.

&nbsp;

### Интерфейс GridDimension<a name="grid-dimension"></a>
```ts
interface GridDimension {
	getDimensionEntity(): EntityInfo;
	async getDimensionEntityAsync(): Promise<EntityInfo>;
}
```
Интерфейс предоставляет данные об измерении мультикуба.

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

```js
getDimensionEntity(): EntityInfo
async getDimensionEntityAsync(): Promise<EntityInfo>
```
Возвращает ссылку на сущность [`EntityInfo`](#entity-info) измерения мультикуба.

&nbsp;

### Интерфейс GridPageSelector<a name="grid-page-selector"></a>
```ts
interface GridPageSelector extends GridDimension {
	getSelectedEntity(): EntityInfo;
}
```
Интерфейс предоставляет данные о фильтре мультикуба. (Ранее фильтры назывались `Page`). Интерфейс наследуется от [`GridDimension`](#grid-dimension). Программно задать значение фильтра позволяет функция [`Pivot`](#pivot).[`addDependentContext()`](#add-dependent-context).

&nbsp;

```js
getSelectedEntity(): EntityInfo
```
Возвращает ссылку на [`EntityInfo`](#entity-info) выбранного элемента фильтра.

&nbsp;

### Интерфейс GridRange<a name="grid-range"></a>
```ts
interface GridRange {
	rowStart(): number;
	rowCount(): number;

	columnStart(): number;
	columnCount(): number;

	cellCount(): number;

	generator(size?: number): GridRangeChunk[];
}
```
Интерфейс, представляющий прямоугольный диапазон ячеек в таблице [`Grid`](#grid).

&nbsp;

```js
rowStart(): number
```
Возвращает номер первой строки.

&nbsp;

```js
rowCount(): number
```
Возвращает количество строк.

&nbsp;

```js
columnStart(): number
```
Возвращает номер первого столбца.

&nbsp;

<a name="grid-range.column-count"></a>
```js
columnCount(): number
```
Возвращает количество столбцов.

&nbsp;

```js
cellCount(): number
```
Возвращает количество ячеек. Эквивалентно `rowCount() * columnCount()`.

&nbsp;

<a name="generator"></a>
```js
generator(size?: number): GridRangeChunk[]
```
Возвращает генератор, при каждом обращении возвращающий интерфейс [`GridRangeChunk`](#grid-range-chunk) размером *не более* `size` ячеек, позволяющий обрабатывать `GridRange` покусочно.

Каждый возвращаемый [`GridRangeChunk`](#grid-range-chunk) содержит целое количество строк, т. е. все колонки `GridRange`, а количество строк в нём определяется по формуле `size / columnCount()`. Здесь используется целочисленное деление. Например, если в таблице `7` столбцов, а параметр `size` равен `100`, то генератор вернёт [`GridRangeChunk`](#grid-range-chunk) из `100 / 7 = 14` строк, в котором будет `7 * 14 = 98` ячеек.

Значение аргумента `size` ограничено снизу значением `500` и сверху значением `5000`, поэтому в скриптах 1.0 [`невозможно`](../appendix/constraints.md#generator) работать с `GridRange` с б*О*льшим количеством столбцов. Значение по умолчанию: `500`.

Типичный пример использования:

```js
let rowIndex = 0;

for (const chunk of range.generator(1000)) {
    chunk.rows().all().forEach(labelGroup => {
        const rowLabels = [];
        labelGroup.all().forEach(label => {
            rowLabels.push(label.label());
        });

        console.log(`Row index ${rowIndex} (${rowLabels.join(', ')})\n`);
        rowIndex++;
    });
}
```

&nbsp;

### Интерфейс GridRangeChunk<a name="grid-range-chunk"></a>
```ts
interface GridRangeChunk {
	cells(): Cells;
	async cellsAsync(): Promise<Cells>;
	
	rows(): Labels;
	async rowsAsync(): Promise<Labels>;
	
	columns(): Labels;
	async columnsAsync(): Promise<Labels>;
	
	rawData(): ChunkRawData;
	async rawDataAsync(): Promise<ChunkRawData>;
}
```
Интерфейс для обработки куска [`GridRange`](#grid-range).

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

```js
cells(): Cells
async cellsAsync(): Promise<Cells>
```
Возвращает ссылку на набор ячеек [`Cells`](#cells) текущего куска.

&nbsp;

```js
rows(): Labels
async rowsAsync(): Promise<Labels>
```
Возвращает интерфейс [`Labels`](#labels), представляющий заголовки строк.

&nbsp;

```js
columns(): Labels
async columnsAsync(): Promise<Labels>
```
Возвращает интерфейс [`Labels`](#labels), представляющий заголовки столбцов.

&nbsp;

```js
rawData(): ChunkRawData
async rawDataAsync(): Promise<ChunkRawData>
```
Возвращает интерфейс [`ChunkRawData`](#chunk-raw-data) для быстрого чтения текущего куска данных.


### Интерфейс ChunkRawData<a name="chunk-raw-data"></a>
```ts
type RawHeaderData = {
  label: string | number | null;
  id: string | number | null;
  longId: number;
  parentLongId: number;
  name?: string | number | null;
  code?: string | number | null;
};

type RawHeaderKey = 'label' | 'id' | 'longId';

type RawRow = Record<string | number, string | number | null>;

type RowFullItem = {
  headers: RawHeaderData[];
  values: RawRow;
};

interface ChunkRawData {
	columnsHeaders(): RawHeaderData[][];
	rowsHeaders(): RawHeaderData[][];
	
	getColumnKey(): RawHeaderKey;
	getRowKey(): RawHeaderKey;
	
	setColumnKey(value: RawHeaderKey): ChunkRawData;
	setRowKey(value: RawHeaderKey): ChunkRawData;
	
	getRawValues(): (string | number | null)[][];
	getRowsAsArray(): RawRow[];
	getRowsAsObject(): Record<string | number, RawRow>;
	getRowsAsItems(): RowFullItem[];
}
```
Интерфейс быстрого чтения данных куска [`GridRangeChunk`](#grid-range-chunk). ***Не*** позволяет записывать данные.

&nbsp;

```js
columnsHeaders(): RawHeaderData[][]
```
Возвращает описание заголовков столбцов в виде массива, каждым элементом которого является массив объектов заголовков очередного столбца.

&nbsp;

```js
rowsHeaders(): RawHeaderData[][]
```
Возвращает описание заголовков строк в виде массива, каждым элементом которого является массив объектов заголовков очередной строки.

&nbsp;

```js
getColumnKey(): RawHeaderKey
```
Возвращает текущее значение ключа для формирования заголовка ячейки при получении строки в виде объекта, что используется в функциях [`getRowsAsArray()`](#chunk-raw-data.get-rows-as-array), [`getRowsAsObject()`](#chunk-raw-data.get-rows-as-object) и [`getRowsAsItems()`](#chunk-raw-data.get-rows-as-items). Допустимые значения: `'label'`, `'id'`, `'longId'`. Значение по умолчанию: `'label'`.

&nbsp;

```js
getRowKey(): RawHeaderKey
```
Аналог `getColumnKey()` для строк.

&nbsp;

```js
setColumnKey(value: RawHeaderKey): ChunkRawData
```
Устанавливает значение ключа для столбцов. См. описание `getColumnKey()`. Возвращает `this`.

&nbsp;

```js
setRowKey(value: RawHeaderKey): ChunkRawData
```
Устанавливает значение ключа для строк. См. описание `getColumnKey()`. Возвращает `this`.

&nbsp;

```js
getRawValues(): (string | number | null)[][]
```
Возвращает сырое содержимое куска [`GridRangeChunk`](#grid-range-chunk). Каждый внутренний массив соответствует одной строке и содержит значения ячеек этой строки.

&nbsp;

<a name="chunk-raw-data.get-rows-as-array"></a>
```js
getRowsAsArray(): RawRow[]
```
Возвращает содержимое куска [`GridRangeChunk`](#grid-range-chunk) в виде массива объектов, где каждый элемент является объектом, представляющим строку, где ключом является установленное поле заголовка столбца. Если заголовков несколько, они объединяются в строку с разделителем `'.'`.

&nbsp;

<a name="chunk-raw-data.get-rows-as-object"></a>
```js
getRowsAsObject(): Record<string | number, RawRow>
```
Возвращает содержимое куска [`GridRangeChunk`](#grid-range-chunk) в виде объекта, где ключом является установленное поле заголовка строки (если заголовков несколько, они объединяются в строку с разделителем `'.'`), а значением — такой же объект строки, какой возращает [`getRowsAsArray()`](#chunk-raw-data.get-rows-as-array).

&nbsp;

<a name="chunk-raw-data.get-rows-as-items"></a>
```js
getRowsAsItems(): RowFullItem[]
```
Возвращает содержимое куска [`GridRangeChunk`](#grid-range-chunk) в виде массива объектов, где в свойстве `headers` содержится массив заголовков строки, а в свойстве `values` — такой же объект строки, какой возращает [`getRowsAsArray()`](#chunk-raw-data.get-rows-as-array).

&nbsp;

### Интерфейс EntityInfo (Label)<a name="entity-info"></a> <a name="label"></a>
```ts
interface Label {
	longId(): number;
	name(): string | null;
	code(): string | null;
	alias(): string | null;
	label(): string | null;
	parentLongId(): number;
}

interface EntityInfo = Label;
```
Интерфейс сущности. Как правило, представляет собой один из заголовков строки или столбца.

&nbsp;

<a name="long-id"></a>
```js
longId(): number
```
Возвращает внутренний идентификатор сущности в системе, уникальный в пределах модели.

&nbsp;

<a name="label.name"></a>
```js
name(): string
```
Возвращает имя сущности.

&nbsp;

```js
code(): string
```
Возвращает код сущности. В Optimacros всего две сущности могут иметь код: элементы справочников и кубы.

&nbsp;

<a name="alias"></a>
```js
alias(): string | null
```
Возвращает отображаемое имя.

Если `this` является сущностью элемента справочника, в настройках которого задано некоторое свойство в качестве отображаемого имени (опция `Отображение`), и для этой сущности задано значение этого свойства, то возвращает значение этого свойства.

Иначе возвращает `null`.

&nbsp;

```js
label(): string | null
```
То же, что и [`alias()`](#alias). Если отображаемое имя не задано, возвращает [`name()`](#label.name).

&nbsp;

```js
parentLongId(): number
```
Если сущность является элементом, у которого есть родительский элемент, то возвращает [`longId`](#long-id) сущности родителя.

Если родительской сущности нет, возвращает `-1`.

&nbsp;

### Интерфейс Labels<a name="labels"></a>
```ts
interface Labels {
	start(): number;
	count(): number;
	
	all(): (LabelsGroup | undefined)[];
	async allAsync(): Promise<(LabelsGroup | undefined)[]>;
	
	get(index: number): LabelsGroup | null;
	async getAsync(index: number): Promise<LabelsGroup | undefined>;
	
	chunkInstance(): GridRangeChunk;
	findLabelByLongId(longId: number): Label | null;
}
```
Интерфейс, представляющий набор интерфейсов [`LabelsGroup`](#labels-group), то есть набор заголовков строк/столбцов с их возможно многоуровневой структурой. Как правило, его можно получить функциями интерфейса [`GridRangeChunk`](#grid-range-chunk).

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

```js
start(): number
```
Возвращает номер первой строки/столбца текущего [`GridRangeChunk`](#grid-range-chunk) в таблице [`Grid`](#grid).

&nbsp;

```js
count(): number
```
Возвращает количество строк/столбцов в наборе.

Если `this` относится к строкам, то это значение, которое было посчитано в функции [`GridRange`](#grid-range).[`generator(size)`](#generator) на основе аргумента `size`.

Если `this` относится к столбцам, то это в точности значение аргумента `columnCount` функции [`Grid`](#grid).[`range(rowStart, rowCount, columnStart, columnCount)`](#range).

&nbsp;

```js
all(): (LabelsGroup | undefined)[]
async allAsync(): Promise<(LabelsGroup | undefined)[]>
```
Возвращает массив интерфейсов [`LabelsGroup`](#labels-group) заголовков каждой строки/столбца.

&nbsp;

```js
get(index: number): LabelsGroup | null
async getAsync(index: number): Promise<LabelsGroup | undefined>
```
Аналог `all()[index]`.

&nbsp;

```js
chunkInstance(): GridRangeChunk
```
Возвращает обратную ссылку на [`GridRangeChunk`](#grid-range-chunk), из которого был получен `this`.

&nbsp;

```js
findLabelByLongId(longId: number): Label | null
```
Возвращает интерфейс [`Label`](#label) по его [`longId`](#long-id), если он присутствует в `this`, иначе — `null`.

&nbsp;

### Интерфейс LabelsGroup<a name="labels-group"></a>
```ts
interface LabelsGroup {
	all(): Label[];
	first(): Label;
	cells(): Cells;
}
```
Интерфейс, представляющий многоуровневый набор заголовков конкретной строки или столбца.

&nbsp;

```js
all(): Label[]
```
Возвращает массив конкретных заголовков [`Label`](#label).

&nbsp;

```js
first(): Label
```
Аналог `all()[0]`.

&nbsp;

```js
cells(): Cells
```
Возвращает интерфейс [`Cells`](#cells), предоставляющий доступ к ячейкам данной строки или столбца.

В случае плоской таблицы [`возвращает`](https://github.com/optimacros/scripts_documentation/blob/main/appendix/constraints.md#flat-table) `null`.

&nbsp;

### Интерфейс Cell<a name="cell"></a>
```ts
interface Cell {
	setValue(value: number | string | boolean | null);
	getValue(): number | string | boolean | null;
	getNativeValue(): number | string | boolean | null;
	getTextValue(): number | string | null;
	getContextValue(): string | null;
	definitions(): number[];
	
	columns(): LabelsGroup | undefined;
	async columnsAsync(): Promise<LabelsGroup | undefined>;
	
	rows(): LabelsGroup | undefined;
	async rowsAsync(): Promise<LabelsGroup | undefined>;
	
	dropDown(): Labels;
	getFormatType(): string;
	isEditable(): boolean;
}
```
Интерфейс, представляющий клетку таблицы.

Работа асинхронных функций описана [`здесь`](./webHandlers.md#async).

&nbsp;

<a name="cell.set-value"></a>
```js
setValue(value: number | string | boolean | null)
```
Устанавливает значение клетки. Отрабатывает в момент вызова и мгновенно приводит к пересчёту зависимых клеток. Поэтому ***не*** рекомендуется к использованию в больших мультикубах.

&nbsp;

<a name="cell.get-value"></a>
```js
getValue(): number | string | boolean | null
```
Возвращает значение клетки, которое видит пользователь.

&nbsp;

<a name="cell.get-native-value"></a>
```js
getNativeValue(): number | string | boolean | null
```
Возвращает самородное значение клетки, зависящее от формата. Если клетка имеет формат справочника, то возвращается [`longId`](#long-id). 

В противном случае возвращает то же, что и [`getValue()`](#cell.get-value).

&nbsp;

<a name="cell.get-text-value"></a>
```js
getTextValue(): number | string | null;
```
Возвращает значение клетки, которое видит пользователь. Работает только для клеток формата `Справочник` и `Дата`, в остальных случаях возвращает `null`.

&nbsp;

<a name="get-context-value"></a>
```js
getContextValue(): string | null
```
Если ячейка имеет формат справочника, в настройках которого задано некоторое свойство `prop` в качестве отображаемого имени (опция `Отображение`), и для этой ячейки задано значение этого свойства, то возвращает строку, состоящую из имени, двойной вертикальной черты и значения свойства `prop`, например, `'#5||Берлин'`.

В противном случае возвращает `null`.

&nbsp;

```js
definitions(): number[]
```
То же, что и [`CubeCell.definitions()`](./cubeCell.md#cube-cell.definitions).

&nbsp;

```js
columns(): LabelsGroup | undefined
async columnsAsync(): Promise<LabelsGroup | undefined>
```
Возвращает многоуровневый набор заголовков [`LabelsGroup`](#labels-group) конкретного столбца.

&nbsp;

```js
rows(): LabelsGroup | undefined
async rowsAsync(): Promise<LabelsGroup | undefined>
```
Возвращает многоуровневый набор заголовков [`LabelsGroup`](#labels-group) конкретной строки.

&nbsp;

```js
dropDown(): Labels
```
***Не реализовано.***

Возвращает набор заголовков строк [`Labels`](#labels) выпадающего списка, который в интерфейсе пользователя Optimacros можно получить кликом по треугольнику внутри ячейки. Эта функция считается неэффективной, так как выгружает справочник целиком. Лучше зайти в нужный справочник и итерироваться по нему.

&nbsp;

```js
getFormatType(): string
```
***Не реализовано.***

Возвращает строку с форматом клетки. Возможные значения: `'NUMBER'`, `'BOOLEAN'`, 
`'ENTITY'`, `'TIME_ENTITY'`, `'LINE_ITEM_SUBSET'`, `'VERSION'`, `'TEXT'`, `'DATE'`, `'NONE'`.

&nbsp;

```js
isEditable(): boolean
```
Возвращает признак возможности редактирования ячейки пользователем.

&nbsp;

### Интерфейс Cells<a name="cells"></a>
```ts
interface Cells {
	all(): Cell[];
	first(): Cell;
	setValue(value: number | string | null);
	count(): number;
	chunkInstance(): GridRangeChunk;
	getByIndexes(indexes: number[]): Cells | null;
}
```
Интерфейс, представляющий (как правило, прямоугольный) набор клеток таблицы.

&nbsp;

```js
all(): Cell[]
```
Возвращает одномерный массив всех клеток [`Cell`](#cell).

&nbsp;

```js
first(): Cell
```
Аналог `all()[0]`.

&nbsp;

<a name="cells.set-value"></a>
```js
setValue(value: number | string | null)
```
***Не реализовано.***

Устанавливает одно и то же значение для всех клеток. Отрабатывает в момент вызова и мгновенно приводит к пересчёту зависимых от них клеток. Поэтому ***не*** рекомендуется к использованию в больших мультикубах.

&nbsp;

```js
count(): number
```
Возвращает количество клеток в наборе.

&nbsp;

<a name="chunk-instance"></a>
```js
chunkInstance(): GridRangeChunk
```
Возвращает обратную ссылку на [`GridRangeChunk`](#grid-range-chunk), из которого был получен `this`.

&nbsp;

```js
getByIndexes(indexes: number[]): Cells | null
```
Производит выборку из одномерного представления клеток объекта `this` по индексам `indexes` и возвращает новый объект [`Cells`](#cells). В этом случае функция [`chunkInstance()`](#chunk-instance) для нового объекта будет возвращать ссылку на тот же самый объект [`GridRangeChunk`](#grid-range-chunk), что и для `this`. Это *единственный* способ создать непрямоугольный объект [`Cells`](#cells).

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)