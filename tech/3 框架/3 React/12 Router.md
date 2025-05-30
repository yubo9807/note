# React Router

> npm run i -D react-router-dom

- HashRouter ： hash 模式
- BrowserRouter ： H5历史模式

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Me = () => 'me';
const Home = () => 'home';
const About = () => 'about';
const NotFound = () => 404;
const Diary = () => 'diary';

function App () {
    return (<Router>
        {/* 看下面那条匹配符合条件 */}
        <Switch>
            <Route path='/' component={Home} exact />
            <Route path='/about' component={About} exact sensitive />
            <Route path='/about/me' component={Me} />
            <Route path='/diary/*' component={Diary} />
            <Route component={NotFound} />
        </Switch>
    </Router>);
    // exact 精确匹配
    // sensitive 区分大小写
}

ReactDOM.render(<App />, document.getElementById('root'));
```

## 路由信息

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route } from 'react-router-dom';

const About = () => 'about';
function Home (props) {
    return (<>
        <span>home</span>&nbsp;
        <span onClick={() => {
            props.history.push('/about');  // 添加路由
            // props.history.replace('/about');  // 替换路由
        }}>about</span>
    </>);
};

function App () {
    return (<Router>
        <Route path='/' component={Home} exact />
        <Route path='/about' component={About} />
    </Router>)
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### 参数解析

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import qs from 'querystring';

function App () {
    const query = qs.parse('a=111&b=222');
    console.log(query);  //-->  {a: "111", b: "222"}
    return (<>hello</>)
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### match 路径匹配

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route } from 'react-router-dom';

function Home (props) {
    console.log(props.match);
    return 'home';
}
function App (props) {
    return (<Router>
        <Route path='/home/:year(\d+)-:month(\d+)-:day(\d+)' component={Home} />
    </Router>)
}

ReactDOM.render(<App />, document.getElementById('root'));
/* {
    访问路径： http://192.168.1.80:3000/home/2020-10-20

    isExact: true
    params: {year: "2020", month: "10", day: "20"}
    path: "/home/year(\d+)-:month(\d+)-:day(\d+)"  // 路径规则
    url: "/home/2020/10/20"
} */
```

## Link 无刷新跳转的 a 标签

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

function Home () {
    return (<Link to={{
        pathname: '/about',
        search: 'a=111',
        hash: 'h',
    }} innerRef={node => {
        console.log(node);
    }}>about</Link>);
}

function App () {
    return (<Router>
        <Route path='/' component={Home} />
    </Router>)
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### NavLink 继承于 Link

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, NavLink } from 'react-router-dom';

function Home () {
    return (<NavLink to='/home' activeStyle={{color: 'red'}} activeClassName='active'>home</NavLink>);
}

function App () {
    return (<Router>
        <Route path='/home' component={Home} />
    </Router>)
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### Redirect 重定向

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Redirect } from 'react-router-dom';

const NotFound = () => (<Redirect to='/home' />);
const Home = () => 'home';

function App () {
    return (<Router>
        <Route path='/home' component={Home} exact />
        <Route component={NotFound} />
    </Router>)
}

ReactDOM.render(<App />, document.getElementById('root'));
```
