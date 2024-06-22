  ## Proxy ---这不就是设计模式中的代理模式吗

  ###### "proxy" 的字面意思是 “代理”，在这里表示由它来“代理”某些操作。Proxy对象用于创建一个对象，该对象可以拦截对另一个对象的操作，并提供自定义行为。
  
  ```js
  let proto = {}
  let handler = {
    set(target, propKey, value, receiver) {
      if (propKey[0] === '_') {
        throw new Error(`不能设置私有属性${propKey}`)
      }
      target[propKey] = value
      return true
    },
    get(target, propKey) {
      if (propKey in target) {
        return target[propKey]
      } else if( propKey === 'prototype' ){
        return Object.prototype
      } else {
        throw new Error(`${propKey} 属性不存在`)
      }
    },
    construct(target, args) {
      return {
        value: args[0],
        code: args[1]
      }
    },
    apply(target, thisBinding, args) {
      return args[0]
    },
    has(target, propKey) {
      if (propKey[0] === '_') {
        return false
      } 
      return propKey in target
    },
    deleteProperty(target, propKey) {
      if (propKey[0] === '_') {
        throw new Error(`私有属性${propKey}不能删除`)
      } 
      delete target[propKey]
    },
    ownKeys(target) {
      return ['a', 'b', 'c']
    },
    getOwnPropertyDescriptor(target, propKey) {
      if (propKey[0] === '_') {
        return;
      }
      return Object.getOwnPropertyDescriptor(target,propKey);
    },
    defineProperty(target, propKey, propDesc) {
      if (propKey[0] === '_') {
        return false
      }
      return true
    },
    getPrototypeOf(target) {
      return proto
    },
    setPrototypeOf(target, proto) {
      return true
    },
    preventExtensions(target) {
      Object.preventExtensions(target)
      return true
    },
    isExtensible(target) {
      return false
    }
  }

  let proxy = new Proxy({
    _prop: 'foo',
    prop: 'foo'
  }, handler)

  let fproxy = new Proxy(function(a, b) {
    return a + b
  }, handler)

  // set
  proxy._a = 1
  proxy.a = 2
  proxy.value  = 1

  // get
  proxy.prototype 
  ++proxy.value

  // construct
  new fproxy(1, 2)

  // apply
  fproxy(1, 2)

  // has
  '_prop' in proxy
  'prop' in proxy

  //deleteProperty
  delete proxy._prop
  proxy.count = 1
  delete proxy.count

  //ownKeys
  Object.keys(proxy)

  for (let key in proxy) {
    console.log(proxy[key])
  }

  // getOwnPropertyDescriptor
  Object.getOwnPropertyDescriptor(proxy, 'prop')

  // defineProperty
  proxy.foo = 'bar'

  // getPrototypeOf
  Object.getPrototypeOf(proxy) === proto

  // setPrototypeOf
  Object.setPrototypeOf(proxy, proto)

  //preventExtensions
  Object.preventExtensions(proxy)

  //isExtensible
  Object.isExtensible(proxy)

  ```

  
  ### so Proxy 可以干什么用呢？
  1. 数据验证：在访问或者修改数据时，验证数据的合理性；
  2. 缓存：在访问对象的属性时可以进行缓存，提高效率；
  3. 日志记录：在访问或者修改对象的属性时记录日志；
  4. 数据模拟：在访问对象的属性时模拟数据；
  5. 权限控制：在访问或者修改对象的属性时，进行权限控制，确保只有授权的用户可以访问和修改；
  其他欢迎补充 ...
  
  
  
  
  


