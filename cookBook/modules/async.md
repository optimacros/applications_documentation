# Синхронный и асинхронный код в приложениях

Код приложений АМ может завпускаться либо синхронно (при запуске из Редактора АМ), либо асинхронно (через вебхендлеры).

<!-- #TODO: ## Добавить информацию или ссылку на описание задач АМ -->

Выполнение асинхронных фукций напрямую из Редактора АМ штатными способом невозможно. Следующий код выполнится только частично, потому, что функция `testFetch` запускается синхронно и не ожидает завершения выполнения `fetch`:

```js
const testFetch = async () => {
    console.log('Start fetch')
    await fetch('https://optimacros.com/')
        .then(() => { console.log('Fetch done!') })
        .catch(() => { console.log('Fetch error!') });
}

testFetch();
```

```shell
[00.359] Start fetch
```

Чтобы в Редакторе АМ запустить функцию асинхронно (например, при отладке функций для вебхендлеров), можно использовать `module.exports`, поскольку экспорт модуля выполняется асинхронно:

```js
const testFetch = async () => {
    console.log('Start fetch')
    await fetch('https://optimacros.com/')
        .then(() => { console.log('Fetch done!') })
        .catch(() => { console.log('Fetch error!') });
}

module.exports = testFetch();
```

```shell
[00.409] Start fetch
[01.957] Fetch done!
```

Следует учитывать, что внутри асинхронной функции для вызова других асинхронных функций нужно использовать `await`, иначе задача закроется до завершения выполнения функции.

Асинхронный вызов работает только для присваивания `module.exports` значения асинхронной функции напрямую, но не работает, если использовать асинхронные функции внутри объекта:

```js
const testFetch = async () => {
    console.log('Start fetch')
    await fetch('https://optimacros.com/')
        .then(() => { console.log('Fetch done!') })
        .catch(() => { console.log('Fetch error!') });
}

module.exports = {
    f: testFetch(),
}
```

```shell
[00.380] Start fetch
[00.387] {"f":{}}
```

Если нужно проверить работу сразу нескольких асинхронных функций, то можно использовать `Promise.then`:

```js
const testFetch = async () => {
    console.log('Start fetch')
    await fetch('https://optimacros.com/')
        .then(() => { console.log('Fetch done!') })
        .catch(() => { console.log('Fetch error!') });
}

const testAnotherFetch = async () => {
    console.log('Start another fetch')
    await fetch('https://optimacros.com/')
        .then(() => { console.log('Another fetch done!') })
        .catch(() => { console.log('Another fetch error!') });
}

module.exports = testFetch().then(async () => { await testAnotherFetch() });
```

```shell
[00.380] Start fetch
[01.567] Fetch done!
[01.567] Start another fetch
[02.561] Another fetch done!
```