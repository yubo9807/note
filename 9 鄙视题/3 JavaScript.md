# JavaScript

## 什么是类数组

## 作用域在什么条件下产生

- ES6 之前：作用域因函数而产生，在函数**声明时**产生；
- ES6：增加了 `{}` `let` `const` 语法

## 原型及原型链的作用

## async 和 defer 区别
- 都是异步加载
- 不同：
    - async 只支持加载外部脚本，defer 可以执行内部脚本；
    - async 会在请求空闲的时候进行加载，defer 在页面解析完毕后进行加载；
    - async 是 W3C 规范，defer 仅支持 IE。
## typeof 返回值

```js
object   function   number   boolean   string   undefined   symbol   bigint
```

## JavaScript 中的数字在计算机内存中占多少个 Byte ？

1. JavaScript 中只有一种数字类型：双精度浮点数 64位
2. 8位 == 1Byte
3. 64 / 8 = 8Byte


## 没有声明的变量为什么会造成内存泄露

- 全局可看做 window，所以在全局 var 的变量直接放在 window 上，window 上的变量不会被回收，所以占内存，即内存泄露；
- 但 function 里的 var 即局部作用域在函数执行完毕时会被销毁，所以不会造成内存泄露；
- 闭包因为有东西指向这个局部作用的 var，所以不会被垃圾回收机制回收机制销毁。

## 事件传播的三个阶段

> Capturing > Target > Bubbling

## 所有对象都有原型

> false  基本对象除外 `String().prototype === undefined`

## 闭包

```js
var f = (
    function f () {
	    return "1";
    },
    function g () {
	    return 2;
    }
)();  // (f1, f2)(); 执行括号执行最后一个函数
console.log(typeof f);  //--> number
```

- 使用场景：递归、私有化变量（立即执行函数）、函数累加器、缓存

## 闭包，typeof，类型转换

```js
var x = 1;
if (function f () {}) {  // 这里的括号被当做运算符，将函数体变为表达式
    x += typeof f;  // typeof fn 不会报错
}
console.log(x);  //--> 1undefined  1 + undefined 隐式类型转换
```

## this 指向

1. 谁调用指向谁；
2. 由 call 调用绑定到指定对象；
3. 由上下文对象调用，调用到哪个上下文对象；
4. 严格模式下指向 undefined，宽松模式下指向绑定的对象。

## 改变 this 指向的几种方式

#### call、apply、bind

- 作用：改变 this 指向
- 不同：
    - call、apply：直接调用
    - bind：需要通过返回函数来接收

#### 箭头函数

- 可以理解为在外部保存 self = this（箭头函数作用域在声明时创建）

## 实现 bind 函数

```js
Function.prototype.newBind = function (target) {
    let self = this;
    let args = [].slice.call(arguments, 1);
    let temp = function () {};
    let f = function () {
        let _arg = [].slice.call(arguments, 0);
        return self.apply( this instanceof temp ? this : (target || window), args.concat(_arg) );
    }
    temp.prototype = self.prototype;
    f.prototype = new temp();
    return f;
}
```

## 实现一个 new

```js
function _new (fn, ...arg) {
    const obj = Object.create(fn.prototype);
    const ret = fn.apply(obj, arg);
    return ret instanceof Object ? ret : obj;
}
```

## 事件循环机制

- 首先会开启任务队列，将异步任务分发到宏队列与微队列当中；
    - 宏队列：DOM 操作、AJAX、H5 history 操作、定时器
    - 微队列：Promise、Process.nextTick（node 异步事件）、MutationObserver（H5 监听 DOM 节点变化）
- 执行方式：先进后出，后进先出（栈）；
- 将自身任务放入到执行队列，在看微队列任务，最后看宏队列任务。

> 开启异步模式：回调函数、事件、定时器、AJAX、发布/订阅（设计模式）、Promise、Generater、async

## 说说对原型与原型链的理解

- 原型：提取公有属性，方便调用，减少内存消耗；
- 原型链：通过 __proto__ 不断的向上查询属性或方法，终点为 null，返回 undefined。

## 继承方式有哪些？

1. 原型链：
    - 过多的继承了没用的属性；
2. 借用构造函数：
    - 不能继承借用构造函数的原型，每次构造函数都要多走一个函数；
3. 共享原型（复制）：
    - 不能随意的改动自己的原型；
4. 圣杯模式：

```js
const inherit = (function () {
    let F = function () {};
    return function (Target, Origin) {
        F.prototype Origin.prototype;
        Target.prototype = new F();
        Target.prototype.constuctor = Target;  // 防止指向紊乱
        Target.prototype.uber = Origin.prototype;  // 寻找自己的超类
    }
}());
```

## 正则回溯问题

- 在正则中有一种贪婪模式，即：
    - /ab{1,3}c/
    - /ab{1,}c/
    - n+
    - n*
    - n?
- 解决方式：将贪婪模式改为懒惰模式
    - /ab{1,3}?c/
    - /ab{1,}?c/
    - n+?
    - n*?
    - n??

> 回溯问题会记录备选状态多次，出现大量计算

## offsetWidth clientWidth scrollWidth 的区别

- offsetWidth = content + padding + border
- clientWidth = content + padding
- scrollWidth = content + padding + scrollbar + 隐藏不可见内容 width

## 将数组扁平化并排序

```js
const arr = [ [1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
arr.toString().split(",").sort((a, b)=> a - b);
//--> ["1", "2", "2", "3", "4", "5", "5", "6", "7", "8", "9", "10", "11", "12", "12", "13", "14"]
```

## 实现一个 sleep 函数，比如 sleep(1000) 意味着等待1000毫秒，可从 Promise、Generator、Async/Await 等角度实现

- Promise

```js
const sleep = time => new Promise(resolve => setTimeout(resolve,time));
sleep(1000).then(() => console.log(1));
```

- Generator

```js
function* sleepGenerator(time) {
    yield new Promise(function (resolve, reject) {
        setTimeout(resolve, time);
    })
}
sleepGenerator(1000).next().value.then(() => console.log(1));
```

- async

```js
function sleep(time) {
    return new Promise(resolve => setTimeout(resolve, time))
}
async function output () {
    let out = await sleep(1000);
    console.log(1);
    return out;
}
output();
```

## 浏览器的垃圾回收机制

- 我们写的 String、Number 等，浏览器会将他们做标记，对于没用的变量收回占用空间

1. 标记清除：
    - 在一个作用域中，从代码执行到结束，浏览器会将其中的变量进行回收，进行内存清除，后续这些变量将访问不到；

```js
function test () {
    var a = 111, b = 222;
    return a + b;
}
// 用完即删，渣男形象
```

2. 引用计数：
    - 针对 引用类型，在没有引用后，将其进行回收

```js
function test () {

    var a = {};  // a 的引用次数为 0
    
    var b = a;  // a 的引用次数加 1

    var c = a;  // a 的引用次数再加 1

    b = {};  // a 的引用次数减 1

    // 最终 a 的引用次数不为 0 ，所以无法进行垃圾回收，造成内存泄露（内存不释放）
}
```

## 执行上下文

- 某个函数或全局代码的执行环境，该环境中包含执行代码的所有信息

## sessionStorage，localStorage，cookie 的区别

- 都会在客户端进行保存；
- cookie 会在请求时发送给服务器，服务器可进行修改；cookie 的父路径不能访问子路径，子路径可访问父路径；
- 有效期：
    - cookie 可设置过期时间；
    - sessionStorage 浏览器关闭即删除；
    - localStorage 长期有效，知道用户删除；
- localStorage 的修改会导致其他文档窗口的 updata 事件；
- 浏览器最多支持 300 个 cookie，浏览器不同单个服务器存放 cookie 条数也不同（最少的支持 20 条），cookie 大小不能超过 4k 左右（浏览器支持大小不同），localStorage 和  sessionStorage 大小支持 5M。

## 常见 JavaScript 错误类型

1. SyntaxError（语法错误）：
    - var 1a;
2. Uncaught ReferenceError（引用错误）：
    - 未声明即引用；
3. RangeError（范围错误）：
    - [].length = -5；
4. TypeError（类型错误）：
    - var obj = {}; obj();
5. URIError（URL 错误）：
    - 函数参数出现问题。