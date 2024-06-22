## export 

```js
//export  abc.js
export var a = 1;

var b = 2
export { b }

var c = 3
export { c as d }

export function f() {}

function g() {}
export { g }

// import 
import { a,  d } from 'abc.js'

import { b as bName } from 'abc.js'

```
##### export 语句输出的接口，与其对应的值是动态绑定的关系，通过该接口可以取到模块内部实时的值。

```js
export var name = 'jack';
setTimeout(() => { name = 'jance' }, 1000)

```

#### export 与 import 都必须在模块的顶层，不能出现在块级作用域中。

```js

// 报错
if(a === 1) {
  export default '123'
}

```

#### import 不能使用表达式和变量

```js
//报错
import { 'f' + 'oo' } from 'module'

//报错
let mod = 'module'
import { foo } from mod;

```

#### 整体模块加载

```js
// circle.js
export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}

// other js
import * as circle from 'circle.js'
console.log("圆面积：" + circle.area(4))
console.log("圆周长：" + circle.circumference(4))

// 报错 整体模块加载的对象，可以静态分析，不允许运行时改变
circle.area = function () {}

```

#### export default 

```js
// e-d.js
export default function boo () {
  console.log('export default')
}

// 或者
function boo() {
  console.log('boo')
}

export default boo

import boo from 'e-d.js'

```

#### export 与 import 复合写法
```js
export { foo, bar } from 'my_module';

// 可以简单理解为
import { foo, bar } from 'my_module';
export { foo, bar };
```

#### import()

##### import() 运行时执行，import() 返回 Promise 对象

```js
async function start() {
  const values = await import('./beforeStart.js')
}

if(flag) {
  import('./moduleA.js').then(() => {})
} else {
  import('./moduleB.js').then(() => {})
}

```

#### import.meta.url 、import.meta.scriptElement
#### import.meta.scriptElement是浏览器特有的元属性，返回加载模块的那个<script>元素，相当于document.currentScript属性。

```js 
console.log(import.meta.url) // 返回本地路径，比如 file:///home/my/foo.js

// HTML 代码为
// <script type="module" src="my-module.js" data-foo="abc"></script>

// my-module.js 内部执行下面的代码
import.meta.scriptElement.dataset.foo
// "abc"

```





