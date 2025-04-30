# Интерфейс Utils

## Интерфейс Utils<a name="utils"></a>
```ts
interface Utils {
	postgreSQL: PostgreSQLConnector;
}
```
Интерфейс, группирующий интерфейсы, работающие вне воркспейса.

&nbsp;

```js
postgreSQL: PostgreSQLConnector;
```
Ссылка на интерфейс [`PostgreSQLConnector`](#postgre-sql-connector).

&nbsp;

### Интерфейс PostgreSQLConnector<a name="postgre-sql-connector"></a>
```ts
interface PostgreSQLConnector {
	setUser(value: string): this;
	setPassword(value: string): this;
	setHost(value: string): this;
	setPort(value: number): this;
	setDatabase(value: string): this;

	async connectAsync(config?: Object): Promise<boolean>;
	async disconnectAsync(): Promise<void>;
	async queryAsync(text: string, params: unknown[]): Promise<unknown>;
	async transactionAsync<T>(async callback: (client: PoolClient) => T): Promise<T | null>;
}
```
Интерфейс для соединения с PostgreSQL. Является низкоуровневой обёрткой над официальным клиентом [`node-postgres`](https://node-postgres.com/).

&nbsp;

```js
setUser(value: string): this;
```
Устанавливает имя пользователя. Возвращает `this`.

&nbsp;

```js
setPassword(value: string): this;
```
Устанавливает пароль пользователя. Возвращает `this`.

&nbsp;

```js
setHost(value: string): this;
```
Устанавливает имя хоста. Возвращает `this`.

&nbsp;

```js
setPort(value: number): this;
```
Устанавливает номер порта. Возвращает `this`.

&nbsp;

```js
setDatabase(value: string): this;
```
Устанавливает имя БД. Возвращает `this`.

&nbsp;

```js
async connectAsync(config?: Object): Promise<boolean>;
```
Устанавливает соединение с БД. Указать настройки соединения можно либо поочерёдным вызовом функций `set...()`, либо передачей объекта `config`, поля которого описаны в [документации](https://node-postgres.com/apis/client) `node-postgres`. Если будут использованы оба способа, данные объекта `config` перезапишут данные, переданные через функции `set...()`. Возвращает признак успешного соединения или бросает исключение с текстом ошибки.

&nbsp;

```js
async disconnectAsync(): Promise<void>;
```
Разрывает соединение с БД.

&nbsp;

```js
async queryAsync(text: string, params: unknown[]): Promise<unknown>;
```
Выполняет запрос к БД. Тело запроса содержится в параметре `text`, оно может быть параметризовано с помощью `params`. Если запрос успешный, возвращает JSON с тремя ключами: `rows`, `fields`, `rowCount`, которые описаны в [документации](https://node-postgres.com/apis/result) `node-postgres`. Если запрос безуспешный, бросает исключение с текстом ошибки.

&nbsp;

```js
async transactionAsync<T>(async callback: (client: PoolClient) => T): Promise<T | null>;
```
Выполняет [транзакцию](https://habr.com/ru/articles/537594/). Принимает в качестве аргумента функцию-колбек `callback` с единственным аргументом `client`, который после запуска `callback` будет содержать объект-аналог `this` с единственной функцией `query()`, почти полностью совпадающей с функцией `queryAsync()`. Единственное отличие заключается в том, что в результирующем JSON функции `PoolClient.query()` окажутся все поля из [документации](https://node-postgres.com/apis/result) и, возможно, служебная информация. Пример использования:

```js
const createCities = `
	CREATE TABLE IF NOT EXISTS "cities" (
		"id" SERIAL,
		"name" VARCHAR(100) NOT NULL,
		"population" INTEGER NOT NULL,
		PRIMARY KEY ("id")
	);`
;

const cities = [['Москва', 8000], ['Ханты-Мансийск', 120], ['Лондон', 10000], ['Выдропужск', 1]];

const res = await sqlClient.transactionAsync(async (client) => {
	await client.query(createCities);
	
	for (const city of cities) {
		await client.query('INSERT INTO cities(name, population) VALUES ($1, $2)', city);
	}
	
	return await client.query('SELECT * FROM cities WHERE name = ($1)', [cities[2][0]]);
});
```

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
