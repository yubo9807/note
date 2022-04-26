# function

## 原生函数

- Array() 不要求必须带 new 关键字，与 new Array() 效果一样

```js
var a = Array(3);
var b = [undefined, undefined, undefined];
var c = [];
c.length = 3;
console.log(a, b, c);
// chrome: --> a: [empty × 3]  b: [undefined, undefined, undefined]  c: [empty × 3]
// firefox: --> a: [undefined, undefined, undefined]  b: [undefined, undefined, undefined]  c: [undefined, undefined, undefined]
```

> Object() Function() RegExp() 尽量不要使用
> 在实际情况下没有必要使用 new Object() 创建对象，因为这样无法像常量形式那样一次设定多个属性，而必须逐一设定

## 作用域带来的影响

```js
function foo(){
    function bar(a){
        i = 3;  // 修改for循环所属作用域中的i
        console.log(a + i);
    }
    for(var i = 0; i < 10; i ++){
        // bar(i * 2);  // 作死操作，无限循环
    }
}
foo();
```

> “隐藏”作用域中的变量和函数所带来的的另一个好处，是可以规避同名标识符之间的冲突。冲突会导致变量的值被意外赋值。

## 立即函数表达式

```js
var obj1 = {
    a: 2
};
(function IIFE(global){  // IIFE() 把他们当作函数调用传递进去
    var a = 3;
    console.log(a);  //--> 3
    console.log(global.a);  //--> 2
})(obj1);


var obj2 = {
    a: 2
};
(function IIFE(def){
    def(obj2);
})(function def(global){
    var a = 3;
    console.log(a);  //--> 3
    console.log(global.a);  //--> 2
})
```

> 倒置代码的运行顺序，将需要运行的函数放在第二位。这种模式在UMD项目中被广泛使用，尽管这种模式略显冗长，但有些人它更容易理解。

## 作用域

```js
foo();  // TypeError
bar();  // ReferenceError
var foo = function bar(){}

// 代码提升后，会被理解为以下形式：
var foo;  // 变量 声明被提升
foo();  // 发生类型错误
bar();  // 函数名称作为函数体（作用域内）的本地变量
foo = function bar(){
    // 变量赋值被保留在原地
}
```

## 闭包

- 闭包的形式：

```js
function foo() {
    var a = 2;
    function baz(){
        console.log(a);  //--> 2
    }
    bar(baz);
}
function bar(fn){
    fn()
}
foo();

function wait(message){
    setTimeout(function timer(){
        console.log(message);
    }, 1000);
}
wait('helo');
```

> 有没有发现，函数内的定时器其实形成了闭包。wait() 执行1000毫秒后，它内部作用域并不会消失，timer函数依然保有wait() 作用域的闭包

## 模块化

```js
function coolModule(){
    var str = 'cool';
    var num = 1234;
    function outputStr(){
        console.log(str);
    }
    function outputNum(){
        console.log(num);
    }
    return {outputStr, outputNum};
}
var foo = coolModule();
foo.outputStr();  //--> cool

var foo = (function coolModule(){
    var str = 'cool';
    var num = 1234;
    function outputStr(){
        console.log(str);
    }
    function outputNum(){
        console.log(num);
    }
    return {outputStr, outputNum};
})();
foo.outputStr();  //--> cool
```
