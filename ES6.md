#块级作用域
###let取代var
ES6提出了两个新的声明变量的命令：let和const。其中，let完全可以取代var，因为两者语义相同，而且let没有副作用。
```js
'use strict';

if (true) {
  let x = 'hello';
}

for (let i = 0; i < 10; i++) {
  console.log(i);
}
```
上面代码如果用var替代let，实际上就声明了一个全局变量，这显然不是本意。变量应该只在其声明的代码块内有效，var命令做不到这一点。
var命令存在变量提升效用，let命令没有这个问题。
```js
'use strict';

if(true) {
  console.log(x); // ReferenceError
  let x = 'hello';
}
```
###全局常量和线程安全
在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。这符合函数式编程思想，有利于将来的分布式运算。
```js
// bad
var a = 1, b = 2, c = 3;

// good
const a = 1;
const b = 2;
const c = 3;

// best
const [a, b, c] = [1, 2, 3];
```
const声明常量还有两个好处，一是阅读代码的人立刻会意识到不应该修改这个值，二是防止了无意间修改变量值所导致的错误。

所有的函数都应该设置为常量。

长远来看，JavaScript可能会有多线程的实现（比如Intel的River Trail那一类的项目），这时let表示的变量，只应出现在单线程运行的代码中，不能是多线程共享的，这样有利于保证线程安全。
