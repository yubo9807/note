# Context 上下文

- 上下文：做某一些事情的环境

## React 中的上下文特点：

1. 当某个组件创建了上下文后，上下文中的数据会被所有后代组件共享
2. 如果某个组件依赖了上下文，会导致该组件不再纯粹（外部数据仅来源于属性 props）

> 简单理解为多层的嵌套函数，在外层函数定义了一个变量贡子函数调用

## 新版 Context

- 上下文是一个独立于组件的对象，该对象通过 React.createContext() 创建
- 返回的是一个包含两个属性的对象

1. Provider ： 生产者。一个组件，该组件会创建一个上下文
2. Comsumer ： 消费者。

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

const ctx = React.createContext();

class Comp extends Component {
    state = {
        name: 'bozai',
        age: 18,
        change: () => {
            this.setState({
                age: 10
            })
        }
    }
    render () {
        // ctx.Provider 约定谁来提供上下文
        return (<ctx.Provider value={this.state}>
            <SonComp />
        </ctx.Provider>);
    }
}
class SonComp extends Component {
    shouldComponentUpdate () {  // 父组件提供的上下文不会受子组件的影响
        return false;
    }
    render () {
        // ctx.Consumer 调用上下文
        return (<ctx.Consumer>
            {value => <h2>{value.age}
                <button onClick={() => value.change()}>change</button>
            </h2>}
        </ctx.Consumer>);
    }
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## 旧版 Context

```jsx
import React, {Component} from 'react';
import ReactDOM from 'react-dom';
import PropTypes from 'prop-types';

const types = {
    name: PropTypes.string,
    age: PropTypes.number
}

class Comp extends Component {
    static childContextTypes = types;  // 约束上下文中数据的类型

    getChildContext () {  // 得到上下文中的数据
        return {
            name: 'bozai',
            age: 18
        }
    }
    render () {
        return (<SonComp />);
    }
}

class SonComp extends Component {
    constructor (props, context) {
        super(props);
    }
    static contextTypes = types;  // 使用父组件上下文，必须传入静态属性 contextTypes
    render () {
        console.log(this.context);  //--> {name: "bozai", age: 18}
        return (<>hello {this.context.name}</>)
    }
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

### 子组件更改上下文数据

```js
import React, {Component} from 'react';
import ReactDOM from 'react-dom';
import PropTypes from 'prop-types';

const types = {
    name: PropTypes.string,
    age: PropTypes.number,
    change: PropTypes.func
}

class Comp extends Component {
    static childContextTypes = types;

    state = {
        name: 'bozai',
        age: 18
    }
    getChildContext () {
        const self = this;
        return {
            name: this.state.name,
            age: this.state.age,
            change (val) {
                self.setState({  // 利用 state 来改变数据
                    age: -- val
                })
            }
        }
    }
    render () {
        return (<SonComp />);
    }
}

class SonComp extends Component {
    constructor (props, context) {
        super(props);
    }
    static contextTypes = types;
    render () {
        return (<>
            <h1>{this.context.age}</h1>
            <button onClick={() => this.context.change(this.context.age)}>age --</button>
        </>)
    }
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

> 旧版 API 存在严重效率问题，并容易导致滥用
