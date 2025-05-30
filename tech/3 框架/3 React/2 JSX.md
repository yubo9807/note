# JSX

- 本质是一个 JS 对象，会被 babel 编译，最终被转换为 createElement（可以对 jsx 语法进行解析）；
- 每个 JSX 表达式有且只有一个根节点 React.Fragment；

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const a = 123, b = 234, nums = [1, 2, 3, 4, 5];
const list = nums.map((val, i) => (<li key={i}>{val}</li>));  // key 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。
const className = 'demo', bgColor = 'yellow';
const str = '<button onclick="alert(0)">点击</button>';

const html = (<>
    <h1>一级标题</h1>
    <p>{a} + {b} = {a + b}</p>
    {/* 注释 */}
    <p>{undefined} {false} {true} {null}</p>
    <ul>{list}</ul>
    <span className={className} style={{color: 'red', background: bgColor}}>text</span>
    <p>{"{""}"}</p>
    {/* { 不能通过转义字符转义 */}
    <p>{str}</p>
    {/* 防注入攻击：div.innerText 写入 */}
    <p dangerouslySetInnerHTML={{__html: str}}></p>
    {/* 字符串编译，React 设置层层障碍，告诉我们这样做是危险的 */}
</>);

ReactDOM.render(html, document.getElementById('root'));
```

> undefined、null、Boolean 值不展示；
> Object 对象无法放置。

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

let num = 0;

render();
setInterval(() => {
    num += 1;
    render();  // 更改数据之后只能重新渲染
}, 1000);

function render () {
    const html = (<p>{num}</p>);
    ReactDOM.render(html, document.getElementById('root'));
}
```

> React 会将前后渲染的 DOM 进行比对，对未修改的 DOM 并不会采取删除操作
