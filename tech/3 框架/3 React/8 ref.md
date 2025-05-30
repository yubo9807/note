# ref

1. ref 作用于内置对象的 html 组件，得到的将是真实的 dom 对象
2. ref 作用于类组件，得到的将是类的实例（ref 不能用于函数组件）

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class Comp extends Component {
    constructor (props) {
        super(props);
        this.txt = React.createRef();  // 创建一个 ref 对象
    }
    componentDidMount () {
        console.log(this.txt.current);  // 通过 ref 获取 dom
    }
    render () {
        return (<h1 ref={this.txt}>hello</h1>);
    }
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

> ref 不再推荐使用字符串赋值，将来可能会被移除
> 能够使用属性和状态进行控制，就不要使用 ref

### 函数式调用

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class Comp extends Component {
    constructor (props) {
        super(props);
        this.txt = React.createRef();
    }
    componentDidMount () {
        console.log(this.txt);
    }
    render () {
        return (<h1 ref={el => this.txt = el}>hello</h1>);
    }
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## ref 转发

- 组件名称并不能直接使用 ref，通过 React.forwardRef() 得到一个新的组件，将 ref 赋值到我们想要的元素上

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

function A (props, ref) {  // 转发后接收 ref 参数
    return <h1 ref={ref}>hello</h1>  // 自定义 ref 值
}
class Comp extends Component {
    constructor (props) {
        super(props);
        this.txt = React.createRef();
    }
    componentDidMount () {
        console.log(this.txt.current);
    }
    render () {
        return (<NewA ref={this.txt} />);
    }
}
const NewA = React.forwardRef(A);  // 转发给新对象

ReactDOM.render(<Comp />, document.getElementById('root'));
```

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

function A (props) {
    return <h1 ref={props.forwardRef}>hello</h1>
}
class Comp extends Component {
    constructor (props) {
        super(props);
        this.txt = React.createRef();
    }
    componentDidMount () {
        console.log(this.txt.current);
    }
    render () {
        return (<NewA ref={this.txt} />);
    }
}
const NewA = React.forwardRef((props, ref) => {  // 接收 ref 参数
    return <A {...props} forwardRef={ref} />
});

ReactDOM.render(<Comp />, document.getElementById('root'));
```
