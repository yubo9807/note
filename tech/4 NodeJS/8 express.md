# express

`npm i express`

```js
const express = require("express");

const app = new express();

app.use(express.static("./dist"));

app.get('*', (req, res) => {  // 请求方式：get、post、delete……
    console.log(req);

    res.send('hello');  // 响应，内部会自动调用 .end()

    res.status(302).header('location', 'https://baidu.com').end();  // 临时重定向
    res.redirect('https://baidu.com');  // 永久重定向

    res.end();  // 结束，断开连接
})

app.listen(3000, () => {
    console.log('服务已启动...');
});
```

## 中间件

```js
app.get('/home', 
    (req, res, next) => {
        res.status(200);  // 响应码
        next(new Error('err'));  // 传入错误参数
    },
    (err, req, res, next) => {
        res.send('服务器发生了错误');
        console.log(err);
        next();  // 交给后续函数处理
    },
    (req, res) => {
        console.log('handler3');
    },
)
```

### 常用中间件

```js
const express = require("express");
const path = require("path");

const app = new express();

// 静态资源映射
// 当请求时，会根据请求路径，从指定的目录中寻找是否存在该文件（如果存在，直接响应文件内容，不再移交给后续中间件）
app.use(express.static(path.resolve(__dirname, "./dist")));

// 解析 application/x-www-from-urlencodeed 格式的请求体
app.use(express.urlencodeed({ extended: true }));

// 解析 application/json 格式的请求体
app.use(express.json());

app.listen(3000);
```

## 路由

```js
const express = require("express");
const path = require("path");

const app = new express();
const studentRouter = express.Router();

studentRouter.get('/', (req, res) => {
    res.send('获取');
});
studentRouter.get('/:id', (req, res) => {
    res.send('获取单条数据');
});
studentRouter.post('/', (req, res) => {
    res.send('添加');
});
studentRouter.delete('/:id', (req, res) => {
    res.send('删除');
});
studentRouter.put('/:id', (req, res) => {
    res.send('修改');
});

app.use('/api/student', studentRouter);

app.listen(3000);
```

[项目案例](https://github.com/belong-you/blog_1.x/tree/server) github

## 简单服务器

```js
const express = require("express");
const path = require('path')
const app = new express();
app.use(express.static("./dist"));

app.use('/', async (req, res) => {
    res.sendFile(path.join(__dirname, './dist/index.html'));
})

const port = 3000;
app.listen(port, () => {
    console.log(`服务已启动... http://localhost:${port}`)
});
```

