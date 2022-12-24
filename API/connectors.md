# Коннекторы

### Интерфейс Connectors<a name="connectors"></a>
```ts
interface Connectors {
	mysql(): SqlConnectorBuilder;
	postgresql(): SqlConnectorBuilder;
	sqlServer(): MicrosoftSqlConnectorBuilder;
	oracle(): OracleConnectorBuilder;
	mongodb(): Mongodb.ConnectorBuilder;
	http(): Http.HttpManager;
	winAgent(builtIn?: boolean): WinAgent.WinAgentBuilder;
}
```
Интерфейс, группирующий [`коннекторы`](../appendix/glossary.md#connector) к различным внешним системам.

&nbsp;

```js
mysql(): SqlConnectorBuilder
```
Возвращает коннектор [`SqlConnectorBuilder`](./relationalDB.md#sql-connector-builder) для подключения к базе данных [`MySQL`](https://ru.wikipedia.org/wiki/MySQL).

&nbsp;

```js
postgresql(): SqlConnectorBuilder
```
Возвращает коннектор [`SqlConnectorBuilder`](./relationalDB.md#sql-connector-builder) для подключения к базе данных [`PostgreSQL`](https://ru.wikipedia.org/wiki/PostgreSQL).

&nbsp;

```js
sqlServer(): MicrosoftSqlConnectorBuilder
```
Возвращает коннектор [`MicrosoftSqlConnectorBuilder`](./relationalDB.md#microsoft-sql-connector-builder) для подключения к базе данных [`Microsoft SQL Server`](https://ru.wikipedia.org/wiki/Microsoft_SQL_Server).

&nbsp;

```js
oracle(): OracleConnectorBuilder
```
Возвращает коннектор [`OracleConnectorBuilder`](./relationalDB.md#oracle-connector-builder) для подключения к базе данных [`Oracle`](https://ru.wikipedia.org/wiki/Oracle_Database).

&nbsp;

```js
mongodb(): Mongodb.ConnectorBuilder
```
Возвращает коннектор [`Mongodb.ConnectorBuilder`](./mongoDB.md#connector-builder) для подключения к базе данных [`MongoDB`](https://ru.wikipedia.org/wiki/MongoDB).

&nbsp;

```js
http(): Http.HttpManager
```
Возвращает коннектор [`Http.HttpManager`](./http.md#http-manager) соединения по протоколу HTTP.

&nbsp;

```js
winAgent(builtIn?: boolean): WinAgent.WinAgentBuilder
```
***Более не поддерживается в скриптах.***

Возвращает коннектор [`WinAgent.WinAgentBuilder`](./winAgent.md#win-agent-builder) для взаимодействия с [`WinAgent`](./winAgent.md). Параметр `builtIn` указывает использовать встроенную конфигурацию воркспейса. Значение по умолчанию: `false`.

&nbsp;

[API Reference](API.md)

[Оглавление](../README.md)
