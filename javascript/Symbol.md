## Symbol

```js
let a = Symbol('a')
let b = Symbol.for('boo')
Symbol.keyFor(b)

const obj = {}
obj[a] = 'abc'

Object.getOwnPropertySymbols(obj) // 获取对象的所有 Symbol 属性名

//Symbol.hasInstance
class MyClass {
  [Symbol.hasInstance](foo) {
    return foo instanceof Array;
  }
}

[1, 2, 3] instanceof new MyClass()

//Symbol.isConcatSpreadable
let concatObj = {length: 2, 0: 'c', 1: 'd'}; 
['a', 'b'].concat(concatObj, 'e') // ['a', 'b', obj, 'e'] 类数组的默认 isConcatSpreadable 为false

obj[Symbol.isConcatSpreadable] = true;
['a', 'b'].concat(concatObj, 'e') // ['a', 'b', 'c', 'd', 'e'] 

//Symbol.species
class MyArray extends Array {
  static get [Symbol.species]() { return Array; }
}

const myarray = new MyArray();
const barray = myarray.map(x => x);

barray instanceof MyArray // false
barray instanceof Array // true

//Symbol.match
let matchReg = /123/g
let matchStr = '123456'
matchStr.match(regexp)
// 等同于
matchReg[Symbol.match](matchStr)

//Symbol.replace
let replaceStr = '123456'
let replaceValue = '123'
replaceStr.replace(replaceValue, 'abc')
// 等同于
replaceValue[Symbol.replace](replaceStr, 'abc')

// Symbol.search
let searchReg = /123/g
let searchStr = '123456'
searchStr.search(searchReg)
//等价于
searchReg[Symbol.search](searchStr)

//Symbol.split
let splitStr = '123456'
let separator = '123'
slpitStr.split(separator, 1)
separator[Symbol.split](splitStr, 1)

// Symbol.iterator
const iterObj = {}
iterObj[Symbol.iterator] = function* () {
  yield 1;
  yield 2;
  yield 3;
}









```