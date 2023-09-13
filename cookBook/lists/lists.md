# Операции со списками

## Создание элементов списка

### Использование numeric elementsCreator

```js
const appendNumericItems = (om, listName, count) => {
    const list = om.lists.listsTab().open(listName);
    const creator = list.elementsCreator().numeric().setPositionEnd().setCount(count);
    
    return creator.create();
}
```

### Использование named elementsCreator

```js
const appendNamedItems = (om, listName, elementNames) => {
    const list = om.lists.listsTab().open(listName);
    const creator = list.elementsCreator().named().setPositionEnd().setElementNames(elementNames);
    
    return creator.create();
}
```

**Важно!** Имена элементов списка должны быть уникальными, причем, как для самого списка, так и для properties. Поэтому перед добавлением именованных элементов следует сравнить массив добавляемых элементов и массив имен элементов в списке. 

## Поиск элемента списка

Для операций с элементами списка необходимо знать их `longId`. Получить значение `longId` можно при создании элементов списка или как?

### Поиск элемента списка по имени

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

### Поиск элемента списка по индексу

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

Следует учитывать, что нумерация элементов списка начинается с 0. Для получения первого элемента списка при вызове функции `getListItemByIndex` аргумент `index` равен 0, для второго элемента - 1 и т.д.

## Удаление элементов списка

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