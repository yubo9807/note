# setState

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyCopm extends React.Component {
    state = {
        num: 0
    }
    handelClick = () => {
        this.setState({
            num: this.state.num + 1
        })
        console.log(this.state.num);
    }

    render () {
        console.log('render');
        return (<>
            <p>{this.state.num}</p>
            <button onClick={this.handelClick}>加一</button>
        </>)
    }
}

ReactDOM.render(<MyCopm/>, document.getElementById('root'));
```

点击后输出结果：（setState “可能”是异步的）

```js
//--> 0
//--> render
```

> 如果改变状态的代码处于某个 HTML 元素的事件中，则其是异步的，否则是同步的

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyCopm extends React.Component {
    state = {
        num: 0
    }
    handelClick = () => {
        this.setState({
            num: this.state.num + 1
        }, () => {
            console.log(this.state.num);
        })
    }

    render () {
        console.log('render');
        return (<>
            <p>{this.state.num}</p>
            <button onClick={this.handelClick}>加一</button>
        </>)
    }
}

ReactDOM.render(<MyCopm/>, document.getElementById('root'));
```

输出结果：

```js
//--> render
//--> 1
```

## 同步多次调用 setState

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

class MyCopm extends React.Component {
    state = {
        num: 0
    }
    handelClick = () => {
        this.setState(cur => ({
            num: cur.num + 1
        }));
        this.setState(cur => ({
            num: cur.num + 1
        }));
        this.setState(cur => ({
            num: cur.num + 1
        }));
    }

    render () {
        return (<>
            <p>{this.state.num}</p>
            <button onClick={this.handelClick}>加一</button>
        </>)
    }
}

ReactDOM.render(<MyCopm/>, document.getElementById('root'));
```

> React 会对异步的 setState 进行优化，将多次的 setState 合并后再渲染
