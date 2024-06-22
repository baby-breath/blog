## Array 创建静态数组的 from() 和 of() 方法

##### Array.from() 可以将什么对象转为数组？

``` js
  const arr = ['a', 'b', 'c', 'd']
  const s = new Set([1, 2, 3, 4]);
  const m = new Map([[1, 'one'], [2, 'two']])
  
  Array.from('hello'); // 字符串拆成单字符数组，['h', 'e', 'l', 'l', 'o']
  Array.from(arr)  // 相当于浅拷贝 ['a', 'b', 'c', 'd']
  Array.from(s)    // [1, 2, 3, 4]
  Array.from(m)    // [[1, 'one'], [2, 'two']]

  const obj = {
    0: 'a',
    1: 'b',
    2: 'c',
    3: 'd',
    length: 4
  }

  Array.from(obj)  // ['a', 'b', 'c', 'd']

  //arguments 对象转化成数组
  function foo() {
    return Array.from(arguments) 
  }

  // 可遍历（iterable）的对象
  const iter = {
    *[Symbol.iterator]() {
      yield 1;
      yield 2;
      yield 3;
    }
  }
  Array.from(iter)

  // NodeList 对象
  let pList = document.querySelectorAll('p');
  Array.from(pList).filter(p => {
    return p.textContent.length > 100;
  });

```
Array.from() 用于将类似数组的对象和可遍历（iterator）的对象转为真正的数组。


##### Array.from() 可以接收几个参数
```js

Array.from([1, 2, 3], function(item) {
  return item * 2
})

Array.from([1, 2, 3], function(item) {
  return item * 2 + this.baseValue
}, { baseValue: 10 })

```
Array 可以接收 3 个参数，第一个是类数组对象，第二个是可选的映射函数参数，第三个是用于指定映射函数中this的值，但是这个 this 的值在箭头函数中不适用。


##### Array.of() 把一组参数值转化成数组
```js
Array.of(1, 2, 3, 4)

Array.of(3)

// 模拟实现 Array.of() 
function ArrayOf(){
  return [].slice.call(arguments);
}


```


##### 小思考
- 类似数组的对象有何特征？
本质特征只有一点，即必须有length属性

- Array.from() 相当于ES5 的哪个方法？
```js
  const obj = {
    0: 'a',
    1: 'b',
    2: 'c',
    3: 'd',
    length: 4
  }
  // ES6
  let array1 = Array.from(obj)
  // ES5
  let array2 = [].slice.call(obj)

```







