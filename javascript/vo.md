## 变量对象 (Variable object  VO)
 什么是变量对象，变量对象是与执行上下文相关的数据作用域，存储了上下文中定义的变量和函数声明。 
   

##### 全局上下文变量对象
  全局对象是预定义对象，通过全局对象可以访问所有其他所有预定义的对象、函数和属性；
  所有非限定的变量和函数名都会作为全局对象的属性；
  在顶层 js 中声明的所有变量都将成为全局对象的属性；
```js
console.log(this)
this instanceof Object
Math.random()
this.Math.random()
var num = 1
this.num
this.window.num

```
##### 函数上下文活动对象
  1. 进入执行上下文
    变量对象包括：函数所有的形参、函数声明、变量声明

  2. 执行代码
    会顺序执行代码，根据代码，修改变量对象的值

  
```js
function person(age) {
  let name 
  function b() {}
  const sayName = function() {}
  name = 'nike'
}

person(1)

// 进入阶段 AO
AO = {
  arguments: {
    0: 1,
    length: 1
  },
  age: 1,
  name: undefined,
  b: reference to function b() {},
  sayName: undefined
}

// 执行阶段 AO

AO = {
  arguments: {
    0: 1,
    length: 1
  },
  age: 1,
  name: 'nike',
  b: reference to function b() {},
  sayName: reference to FunctionExpression "sayName"
}

```