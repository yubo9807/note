## callbacks

> 异步编程离不开回调机制  setInterval、ajax、事件

```js
function a (x, y) {
    console.log('a', x, y);
}
function b (x, y) {
    console.log('b', x, y);
}
function c (x, y) {
    console.log('c', x, y);
}
var cb = $.Callbacks('memory');  // once 只执行一次  
                                  // memory 执行后面所添加的回调
                                  // unique 去重
                                  // stopOnFalse 碰到 return false 停止
cb.add(a, b);  // 添加新的回调到回调列表
cb.fire('10', 20);  // 返回绑定它的那个回调对象
cb.add(c);
```

### 回调机制的好处：

1. js是单线程的->异步编程可以优化体验，防止页面阻塞
2. 运动函数 animate 当你满足某个状态，接下来要去做另一件事
