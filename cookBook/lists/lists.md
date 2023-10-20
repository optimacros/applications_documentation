# Операции со справочниками

Все примеры подразумевают, что аргумент `om` — это объект, полученный при **[синхронном](../../API/API.md#model-connect)** соединении с моделью.

## Создание элементов справочника

### Интерфейс [`numericElementsCreator`](../../API/elementsManipulator.md#numeric-elements-creator)


```js
const appendNumericItems = (om, listName, count) => {
    const list = om.lists.listsTab().open(listName);
    const creator = list.elementsCreator().numeric().setPositionEnd().setCount(count);
    
    return creator.create();
}
```

### Интерфейс [`namedElementsCreator`](../../API/elementsManipulator.md#named-elements-creator)

```js
const appendNamedItems = (om, listName, elementNames) => {
    const list = om.lists.listsTab().open(listName);
    const creator = list.elementsCreator().named().setPositionEnd().setElementNames(elementNames);
    
    return creator.create();
}
```

**Важно!** Имена элементов справочника должны быть уникальными **и** не совпадать с названиями его свойств.

## Поиск элемента справочника

Для операций с элементами справочника необходимо знать их `longId`. Получить значение `longId` можно при создании элементов справочника или при вызове метода [`longId()`](../../API/views.md#long-id) для элемента справочника.

### По имени

```js
const getListItemByName = (om, listName, elementName) => {
    const list = om.lists.listsTab().open(listName);
    const grid = list.pivot().rowsFilter(elementName).withoutValues().create();
    const chunks = grid.range().generator();
    if (chunks.length) {
        return chunks[0].rows().get(0).first().longId();
    }
    
    return null;
}
```

### По номеру

```js
const getListItemByIndex = (om, listName, index) => {
    const list = om.lists.listsTab().open(listName);
    const grid = list.pivot().withoutValues().create();
    if (index <= grid.rowCount()) {
        const chunks = grid.range(index, 1, 0, 1).generator();
        if (chunks.length) {
            return chunks[0].rows().get(0).first().longId();
        } 
    }
    
    return null;
}
```

Следует учитывать, что нумерация элементов справочника начинается с `0`. Для получения первого элемента справочника при вызове функции `getListItemByIndex()` аргумент `index` равен `0`, для второго элемента — `1` и т. д.

## Удаление элементов справочника

```js
const deleteListElements = (om, listName, indexes) => {
    const list = om.lists.listsTab().open(listName);
    const deleter = list.elementsDeleter();
    indexes.forEach((index) => {
        deleter.appendIdentifier(index);
    });

    return deleter.delete();
}
```