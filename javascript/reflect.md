## Reflect 操作对象的新 API

 ###### Reflect 与 Proxy 一一对应，Proxy 对象的方法，都能在 Reflect对象上找到对应的方法。

``` js
  function Animal (type) {
    this.type = type
  } 
  let handler = {
    set(target, propKey, value, receiver) {
      return Reflect.set(target, propKey, value)
    },
    get(target, propKey) {
      return Reflect.get(target, propKey)
    },
    construct(target, args) {
      return Reflect.construct(Animal, [...args])
    },
    apply(target, thisBinding, args) {
      const nums = [1,13,24,12,222]
      return Reflect.apply(Math.min, Math, nums)
    },
    has(target, propKey) {
      return Reflect.has(target, propKey)
    },
    deleteProperty(target, propKey) {
      if (propKey[0] === '_') {
        throw new Error(`私有属性${propKey}不能删除`)
      } 
      Reflect.deleteProperty(target, propKey)
    },
    ownKeys(target) {
      var obj = {
        a: 1,
        b: 2,
        [Symbol.for('a')]: 3,
        [Symbol.for('b')]: 4,
      }
      return Reflect.ownKeys[obj]
    },
    getOwnPropertyDescriptor(target, propKey) {
      if (propKey[0] === '_') {
        return;
      }
      return Reflect.getOwnPropertyDescriptor(target,propKey);
    },
    defineProperty(target, propKey, propDesc) {
      if (propKey[0] === '_') {
        return false
      }
      return Reflect.defineProperty(target, propKey, propDesc)
    },
    getPrototypeOf(target) {
      return Reflect.getPrototypeOf(target)
    },
    setPrototypeOf(target, proto) {
      return Reflect.setPrototypeOf(target, proto)
    },
    preventExtensions(target) { // 让一个对象变为不可扩展
      Reflect.preventExtensions(target)
      return true
    },
    isExtensible(target) {
      Reflect.isExtensible(target)
    }
  }

  const p = new Proxy({
    foo: 1,
    bar: 2
  }, handler)


```

 ### so 为什么定义 Reflect 呢？
 1. 将对象 Object 上一些明显属于语言内部的方法，放到Reflect对象上；
 2. 修改这些方法的返回，使其更合理；
 3. 让 Object 的一些操作都变成函数行为（prop in obj）变成 Reflect.has(obj, prop)；
 4. 方便 Proxy 对象的 调用。
