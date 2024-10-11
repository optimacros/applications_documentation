# Интерфейсы воркспейса

## Интерфейс Workspace<a name="workspace"></a>
```ts
interface Workspace {
	files(): WorkspaceFiles;
}
```
Интерфейс функций воркспейса, не связанных непосредственно с какой-то моделью.

&nbsp;

```js
files(): WorkspaceFiles;
```
Возвращает ссылку на интерфейс [`WorkspaceFiles`](#workspace-files).

&nbsp;

### Интерфейс WorkspaceFiles<a name="workspace-files"></a>
```ts
interface WorkspaceFiles {
	getFiles(hashes: string[]): FileBase64Info[];
	async getFilesAsync(hashes: string[]): Promise<FileBase64Info[]>;
}
```
Интерфейс получения файлов из скриптов модели.

&nbsp;

```js
getFiles(hashes: string[]): FileBase64Info[];
async getFilesAsync(hashes: string[]): Promise<FileBase64Info[]>;
```
Принимает список хэшей файлов, которые могут быть получены в скрипте, как правило, функцией скриптов 1.0 `Filesystem`.[`makeGlobalFile()`](https://github.com/optimacros/scripts_documentation/blob/main/API/fs.md#filesystem.make-global-file). Передать хэши из скрипта в приложение можно после выполнения скрипта через объект [`RunScriptResult`](./scriptsTab.md#run-script-result). Возвращает массив объектов [`FileBase64Info`](#file-base64-info) с информацией об этих файлах.

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

[API Reference](API.md)

[Оглавление](../README.md)