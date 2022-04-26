# this

### this 绑定规则

- 1.由 new 调用？绑定到新创建的对象。
- 2.由 call 或 apply（或  bind ）调用？绑定到指定的对象。
- 3.由上下文对象调用？绑定到那个上下文对象。
- 4.默认：在严格模式下绑定到 undefined ，否则绑定到指定的对象。

> ES6 中的箭头函数并不会使用四条标准的绑定准则，而且是根据当前的词法作用域来决定 this ，具体来说，箭头函数会继承外层函数调用的 this 绑定（无论 this 绑定到什么）。这和之前代码中的 self = this 机制一样。

```js
var obj = {
    id: 'awesome',
    cool: function coolFn () {
        console.log(this.id);
    }
};
var id = 'not awesome';
obj.cool();  //--> awesome
setTimeout(obj.cool, 1000);  // this丢失  --> not awesome
// 定时器内部执行cool函数并且把this强制指向了window

// 通过箭头函数“继承”了 cool() 函数的this绑定
var obj = {
    count: 0,
    cool: function coolFn () {
        setTimeout(() => {
            this.count ++;
            console.log('awesome');
        }, 100)
    }
};
obj.cool();  //--> awesome
```
