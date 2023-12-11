# Файлы CSV

### Интерфейс CsvWriter<a name="csv-writer"></a>
```ts
interface CsvWriter {
	params(): CSVParams;
	writeRow(row: string[]): CsvWriter;
	writeRows(rows: string[][]): CsvWriter;
	save(name: string, charset?: string): string;
}
```
Интерфейс для записи в новый файл формата [`CSV`](https://ru.wikipedia.org/wiki/CSV). Запись ведётся во временный буфер, и лишь функция [`save()`](#csv-writer.save) сохраняет файл в памяти. Редактировать существующий файл невозможно, вместо этого нужно читать из одного файла и писать в другой.

&nbsp;

```js
params(): CSVParams
```
Возвращает ссылку на интерфейс [`CSVParams`](./exportImport.md#csv-params), предоставляющий доступ к настройкам CSV.

&nbsp;

```js
writeRow(row: string[]): CsvWriter
```
Записывает массив полей `row` в очередную строку файла. Возвращает `this`.

&nbsp;

```js
writeRows(rows: string[][]): CsvWriter
```
Записывает двойной массив полей `rows` в очередные несколько строк файла. Возвращает `this`.

&nbsp;

<a name="csv-writer.save"></a>
```js
save(name: string, charset?: string): string
```
Сохраняет файл в [`рабочей директории скрипта`](../appendix/glossary.md#script-dir) под именем `'{name}.csv'` в кодировке `charset` (допустимые значения: `'UTF-8'`, `'WINDOWS-1251'`, значение по умолчанию: `'UTF-8'`). Возвращает имя файла с расширением: `'{name}.csv'`.

&nbsp;

### Интерфейс CsvReader<a name="csv-reader"></a>

```ts
interface CsvReader {
	params(): CSVParams;
	changeFileCharset(charset: string): CsvReader;
	generator(): string[][];
}
```
Интерфейс для чтения файла формата [`CSV`](https://ru.wikipedia.org/wiki/CSV).

&nbsp;

```js
params(): CSVParams
```
Возвращает ссылку на интерфейс [`CSVParams`](./exportImport.md#csv-params), предоставляющий доступ к настройкам CSV.

&nbsp;

```js
changeFileCharset(charset: string): CsvReader
```
Устанавливает кодировку файла. Допустимые значения: `'UTF-8'`, `'WINDOWS-1251'`, значение по умолчанию: `'UTF-8'`. Возвращает `this`.

&nbsp;

```js
generator(): string[][]
```
Возвращает генератор, при каждом обращении читающий одну строку файла CSV и возвращающий её в виде `string[]`.

&nbsp;

### Интерфейс BaseConverter<a name="base-converter"></a>

***Не реализовано.***

```ts
interface BaseConverter {
	setSource(path: string): this;
	convert(): string;
}
```
Базовый интерфейс преобразования файлов.

&nbsp;

```js
setSource(path: string): this
```
Устанавливает имя исходного файла. Возвращает `this`.

&nbsp;

```js
convert(): string
```
Конвертирует файл. Возвращает имя преобразованного файла.

&nbsp;

### Интерфейс ExcelToCsvConverter<a name="excel-to-csv-converter"></a>

***Не реализовано.***

```ts
interface ExcelToCsvConverter extends BaseConverter {
	setSheetIdentifier(identifier: string | number): ExcelToCsvConverter;
}
```
Интерфейс преобразования файлов Excel в CSV. Наследуется от [`BaseConverter`](#base-converter).

&nbsp;

```js
setSheetIdentifier(identifier: string | number): ExcelToCsvConverter
```
Устанавливает идентификатор или имя листа. Возвращает `this`.

&nbsp;

### Интерфейс ConverterManager<a name="converter-manager"></a>

***Не реализовано.***

```ts
interface ConverterManager {
	excelToCsv(): ExcelToCsvConverter;
}
```
Менеджер конвертеров.

&nbsp;

```js
excelToCsv(): ExcelToCsvConverter
```
Возвращает ссылку на интерфейс [`ExcelToCsvConverter`](#excel-to-csv-converter) преобразования файлов Excel в CSV.

&nbsp;

### Интерфейс FilesDataManager<a name="files-data-manager"></a>
```ts
interface FilesDataManager {
	csvWriter(): CsvWriter;
	csvReader(path: PathObj): CsvReader;
	converterManager(): ConverterManager;
}
```
Интерфейс, который группирует интерфейсы для работы с файлами в [`рабочей директории скрипта`](../appendix/glossary.md#script-dir).

&nbsp;


```js
csvWriter(): CsvWriter
```
Возвращает ссылку на [`CsvWriter`](#csv-writer).

&nbsp;

```js
csvReader(path: PathObj): CsvReader
```
***Не реализовано.***

Возвращает ссылку на [`CsvReader`](#csv-reader) для чтения файла `path` в формате [`PathObj`](./fs.md#path-obj).

&nbsp;

```js
converterManager(): ConverterManager
```
***Не реализовано.***

Возвращает ссылку на [`ConverterManager`](#converter-manager).

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)