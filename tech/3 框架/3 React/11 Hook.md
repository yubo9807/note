# Hook

> 所有 Hook 不能写在 if | for 中

## State Hook

- State Hook 是一个在函数组件中使用的函数（useState），用于在函数组建中使用状态

```jsx
import React, {useState} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    // useState() 返回一个数组，arr[0] 初始值，arr[1] 设置值
    let [num, setNum] = useState(0);
    setNum = 0;  // 两次数据完全相等（Object.is 进行比较），不会导致重新渲染
    return (<>{setNum}</>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

> 一个函数组件中可以有多个状态，这种做法非常有利于横向切分关注点

## Effect Hook

```jsx
import React, {useState, useEffect} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    let [num, setNum] = useState(0);
    useEffect(() => {  // 副作用操作
        document.title = num;
        let timer = setInterval(() => {
            console.log(num + 1);
        }, 1000);

        // 返回函数，永远执行在 useEffect 的最开始（在数据初始化时不会执行）
        return () => {
            clearInterval(timer);
            timer = null;
        }
    }, [num])  // 第二个参数会与原先数据进行比较，一致则不会运行 useEffect
    return (<h1 onClick={() => {
        setNum(num + 1);
    }}>{num}</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

> 副作用函数的运行时间在真实 UI 渲染完之后，是异步操作，不会阻塞页面

## LayoutEffect Hook

- useLayoutEffect 完成了 DOM 渲染，但还没呈现页面

```jsx
import React, {useState, useLayoutEffect} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    const [num,] = useState(10);
    useLayoutEffect(() => {
        console.log(num);
    })
    return (<h1>hello</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## Context Hook

```jsx
import React, {useContext} from 'react';
import ReactDOM from 'react-dom';

const ctx = React.createContext('hello');

function Comp () {
    const value = useContext(ctx);
    return (<h1>{value}</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## Callback Hook

```jsx
import React, {useState, useCallback} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    const [num, setNum] = useState(10);
    const handleClick = useCallback(() => {
        setNum(num + 1);
    }, [num])
    return (<h1 onClick={handleClick}>{num}</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## Memo Hook

```jsx
import React, {useState, useMemo} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    const [, setN] = useState(0);
    const [range,] = useState({min: 0, max: 100});
    const list = useMemo(() => {
        const arr = [];
        for (let i = 0; i < range.max; i++) {
            console.log(i)
            arr.push(<li key={i}>{i}</li>);
        }
        return arr;
    }, [range])  // 监控 range 状态
    return (<ul onClick={() => {
        setN(10);  // 改变了 setN 的值，不会导致 range 重新渲染，达到性能上的优化
    }}>
        {list}
    </ul>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## Ref Hook

```jsx
import React, {useRef, useEffect} from 'react';
import ReactDOM from 'react-dom';

function Comp () {
    const demo = useRef();
    useEffect(() => {
        console.log(demo.current);
    })
    return (<h1 ref={demo}>hello</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## ImperativeHandle Hook

```jsx
import React, {useRef, useImperativeHandle, useEffect} from 'react';
import ReactDOM from 'react-dom';

const TestSomComp = React.forwardRef(SonComp);

function Comp () {
    const demo = useRef();

    return (<>
        <h1 onClick={() => {
            demo.current.method();
        }}>hello</h1>
        <TestSomComp ref={demo}/>
    </>)
}

function SonComp (props, ref) {
    useImperativeHandle(ref, () => {
        return {
            method () {
                console.log(123456)
            }
        }
    }, [])
    return <h2>word</h2>
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```

## DebugValue Hook

```jsx
import React, {useState, useDebugValue} from 'react';
import ReactDOM from 'react-dom';

// 自定义 Hook
function useTest () {
    const [num,] = useState(10);
    useDebugValue(num);  // 方便调试，展示关键信息
    return num;
}

function Comp () {
    useTest();
    return (<h1>hello</h1>)
}

ReactDOM.render(<Comp />, document.getElementById('root'));
```
