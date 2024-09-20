## Удаление дубликатов

##### Коллекция

```js
const array = [1, 1, 2, 3, 5, 1, 6, 2, 5, 6, 7, 2];
const unique = [...new Set(array)];
```



##### Фильтр

```js
const array = [1, 1, 2, 3, 5, 1, 6, 2, 5, 6, 7, 2];

let unique = array.filter((item, index) => {
  return array.indexOf(item) === index;
});
```



##### Цикл

```js
const array = [1, 1, 2, 3, 5, 1, 6, 2, 5, 6, 7, 2];

function unique(array) {
  let _array = [];
  for (let index = 0; index < array.length; index++) {
    const element = array[index];
    const found = _array.indexOf(element);
      
    if (found === -1) {
      _array.push(element);
    }
  }
  return _array;
}
```



##### Reduce

```js
const array = [1, 1, 2, 3, 5, 1, 6, 2, 5, 6, 7, 2];

const unique = array.reduce((result, item) => {
    return result.includes(item) ? result : [... result, item];
}, []);
```





