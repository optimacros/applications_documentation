# Карта модели

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
	
	toJSON(): Record<string, ToJson>;
	async toJSONAsync(): Promise<Record<string, ToJson>>;
}
```
Интерфейс получения связных данных о компонентах модели.

&nbsp;


&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
