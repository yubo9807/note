## 变量声明，禁止使用 var 声明变量
### var 存在的问题
1. 变量可被重新赋值；
2. 变量提升；
3. 作用域：for 循环输出 `i` = `i + 1`， 需通过闭包解决；
4. 挂载到 window 上，污染全局变量。

```javascript
if (Math.random() > .5) {
  var a = 111;
}
console.log(a);  // 进入判断：111，否则：undefined

function test () {
  var arr = [];
  for (var i = 0; i < 10; i ++) {
    arr[i] = () => console.log(i);
  }
  return arr;
}
var myArr = test();
for(var j = 0; j < 10; j ++){
  myArr[j]();  //--> 10 * 10  函数执行
}
```

## 赋值使用 void 0 代替 undefined
1. undefined 在 JS 中不属于关键字，是 window 上的一个只读属性

```javascript
(function () {
  const undefined = 1;
  const a = undefined;
  console.log(a);  //--> 1
}());
```

## 除直接调用的情况外，严谨将函数直接赋值
```javascript
const obj = {
  fn() {
    console.log(this);
  }
}

const f1 = obj.fn;
f1();  // 这里会导致 this 指向发生改变

function f2() {
  return obj.fn();
}
f2();
```

## 数组遍历，使用 ES5 后提出的一系列 API 代替 for 循环
1. 更好的性能提升；
2. 规避 `for` 循环遍历 稀疏数组 的问题。

```javascript
const arr = new Array(3);
console.log(arr);  //--> [empty × 3]

arr[1] = 0;
for (let i = 0; i < arr.length; i++){
  console.log(arr[i]);
}
//--> undefined 0 undefined
```

## 推荐参数添加默认值
```javascript
function fn(a = 1, b = 1) {}  // 参数添加默认值后函数内部自动变为严格模式
```

## 不建议使用 `?.`
```javascript
obj.a?.b  //-->

// babel 转换后：
var _a;(_a = obj.a) == null ? void 0 : _a.b;

// 我们不如写：
obj.a && obj.a.b;  // 又给项目节省了好几个 B 的空间
```

## 避免使用 delete
+ 推荐使用 `new Map().delete()` 或 解构`...` 的方式来代替 `delete`
+ 使用 delete 操作符并不会直接释放内存，而是说它会使得 V8（Javascript）引擎中的 hidden class 失效，将该 object 变为一个通用的 slow object，这就使得执行速度有了很明显的降低。

```javascript
const obj = { a: 111, b: 222 }

// 不推荐
// delete obj.a

// 推荐1
const { a, ...arge } = obj;  // 使用 arge

// 推荐2
const map = new Map(Object.entries(obj));
map.delete('a');
```

## 利用闭包解决内存忽上忽下的问题
```typescript
function createRemoveSpace() {
  const reg = /\s/g, space = '';
  return (str) => str.replace(reg, space);
}

const createSpace = createRemoveSpace();
createSpace();
createSpace = null;  // 进行垃圾回收
```

## 利用立即执行函数避免过多的 if-else 判断
```typescript
const getScrollPosition = (function() {
  if (window.pageXOffset !== void 0) {
    return (el) => ({
      x: el.pageXOffset,
      y: el.pageYOffset,
    }) : 
  } else {
    return (el) => ({
      x: el.scrollLeft,
      y: el.scrollTop,
    })
  }
}())
```

