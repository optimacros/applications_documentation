# Интерфейс Utils

## Интерфейс Utils<a name="utils"></a>
```ts
interface Utils {
	postgreSQL: PostgreSql;
}
```
Интерфейс, группирующий интерфейсы, работающие вне воркспейса.

&nbsp;

```js
postgreSQL: PostgreSql;
```
Ссылка на интерфейс [`PostgreSql`](#postgre-sql).

&nbsp;

## Интерфейс PostgreSql<a name="postgre-sql"></a>
```ts
interface PostgreSql {
  createConnector(): PostgreSqlConnector;
}
```
Интерфейс для взаимодействия с PostgreSQL.

&nbsp;

```js
createConnector(): PostgreSqlConnector;
```
Возвращает ссылку на интерфейс [`PostgreSqlConnector`](#postgre-sql-connector).

&nbsp;

### Интерфейс PostgreSqlConnector<a name="postgre-sql-connector"></a>
```ts
interface PostgreSqlConnector {
	setUser(value: string): this;
	setPassword(value: string): this;
	setHost(value: string): this;
	setPort(value: number): this;
	setDatabase(value: string): this;

	showFullQueryResponse(value: boolean): this;

	setTrace(value: boolean): void;
	getLog(): string;
	purgeLog(): void;

	async connectAsync(config?: Object): Promise<boolean>;
	async disconnectAsync(): Promise<void>;
	
	async queryAsync(text: string, params: unknown[], timeout?: number): Promise<QueryAsyncResponse | QueryResult>;
	async transactionAsync<T>(async callback: (client: PoolClient) => T, timeout?: number): Promise<T>;
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

<a name="postgre-sql-connector.show-full-query-response"></a>
```js
showFullQueryResponse(value: boolean): this;
```
Устанавливает флаг полного показа ответа на запрос к БД функцией [`queryAsync()`](#postgre-sql-connector.query-async). Значение по умолчанию: `false`. Возвращает `this`.

&nbsp;

```js
setTrace(value: boolean): void;
```
Устанавливает флаг ведения лога запросов. Значение по умолчанию: `true`. Возвращает `this`.

&nbsp;

```js
getLog(): string;
```
Возвращает текст лога запросов.

&nbsp;

```js
purgeLog(): void;
```
Очищает лог запросов.

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

<a name="postgre-sql-connector.query-async"></a>
```js
async queryAsync(text: string, params: unknown[], timeout?: number): Promise<QueryAsyncResponse | QueryResult>;
```
Выполняет запрос к БД. Тело запроса содержится в параметре `text`, оно может быть параметризовано с помощью `params`. Необязательный параметр `timeout` задаёт количество миллисекунд на выполнение запроса; значение `0` отключает таймаут. Значение по умолчанию: `0`. Если запрос успешный, то в зависимости от [`showFullQueryResponse()`](#postgre-sql-connector.show-full-query-response) возвращает [`QueryAsyncResponse`](#query-async-response) или [`QueryResult`](#query-result). Если запрос безуспешный, бросает исключение с текстом ошибки. 

&nbsp;

```js
async transactionAsync<T>(async callback: (client: PoolClient) => T, timeout?: number): Promise<T>;
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

### Интерфейс QueryResult<a name="query-result"></a>
Интерфейс результата запроса. Соответствует интерфейсу `pg.Result` и описан в [документации](https://node-postgres.com/apis/result) на `node-postgres`.

&nbsp;

### Интерфейс QueryAsyncResponse<a name="query-async-response"></a>
Интерфейс результата запроса. Соответствует интерфейсу [`QueryResult`](#query-result) без полей `'command'` и `'oid'`.


&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
