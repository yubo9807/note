# koa

## koa 与 express 的区别

- 更轻量
- 更合理的对象结构
- 更友好的支持中间件（洋葱式，获取上个中间件内容）

```js
const koa = require('koa');
const app = new koa();
const http = require('http');
const server = http.createServer(app.callback());

app.use(async (ctx, next) => {
    ctx.request.utl;
    ctx.state.user = {name: 'bozai'};  // .state 中是专门用来存东西的
    ctx.response.body = {a: 1, b: 2};
    await next();  // koa 支持等待 next 函数
    
	// 等待所有中间件完成后执行
    const body = ctx.response.body;
    ctx.response.body = {
        code: 200,
        msg: '',
        code: body
    }
})

server.listen(5008, () => {
    console.log('服务已启动...');
})
```

> ctx.request 和 ctx.response 上的属性可直接通过 ctx. 来获取

### cookie

```js
ctx.cookies.set(name, value, [options]);  // 设置 cookie
ctx.cookies.get(name);  // 获取 cookie
```

#### cookie 加密

```js
app.keys = ['pwd1', 'pwd2'];  // 旋转加密，保存至多台服务器，防止中招
ctx.cookies.set(name, value, {signed: true});  // cookie 加密
ctx.cookies.get(name, {signed: true});  // cookie 解密
```

### error

```js
app.use(async (ctx, next) => {
    ctx.throw(403, '客户端错误信息', '服务端错误信息');  // 触发错误
    next();
})

app.on('error', err => {  // 监听错误事件
    console.log('error:::::', err);
})
```

### 自定义事件

```js
app.use(async (ctx, next) => {
    app.emit('custom', 123);
})

app.on('custom', (data) => {
    console.log(data);
})
```

## 静态资源中间件

##### .index.js

```js
const koa = require('koa');
const path = require('path');
const app = new koa();
const koaStatic = require('./koaStatic.js');

app.use(koaStatic(path.resolve(__dirname, 'public')));

app.listen(5008, () => {
    console.log('服务器已启动...');
});
```

##### .koaStatic.js

```js
const fs = require("fs");
const path = require("path");
const mime = require("mime");

// 用于获取文件路径
async function getFileName(urlPath, root) {
    const subPath = urlPath.substr(1);
    const filename = path.resolve(root, subPath);
    try {
        const stat = await fs.promises.stat(filename);
        if (stat.isDirectory()) {
            // 是目录
            const newUrlPath = path.join(urlPath, "index.html");
            return await getFileName(newUrlPath, root);
        } else {
            return filename;
        }
    } catch {
        return null;
    }
}

module.exports = function (root) {
    return async function (ctx, next) {
        if (ctx.method !== "GET") {
            await next();
            return;
        }
        const filename = await getFileName(ctx.path, root);
        if (!filename) {
            // 文件不存在
            await next();
            return;
        }
        // 得到文件内容
        ctx.body = fs.createReadStream(filename);
        ctx.type = mime.getType(filename);
    };
};
```

## 常用中间件

- @koa/router  ： 官方中间件。借鉴了`koa-router` 用于处理路由的中间件，用法类似 `express.Router` 
- koa-bodyparser  ： 解析请求体的中间件，支持 x-www-form-urlencoded, application/json 格式的请求体
- koa-views  ： 渲染模板引擎的中间件，一般用于传统的服务端渲染
- koa-static  ： 用于搭建静态资源服务器的中间件
- koa-static-cache  ： 实现了http缓存的静态资源中间件
- koa-session  ： session中间件
- koa-jwt  ： 支持jwt的中间件
- koa-compress ： 支持gzip动态压缩的中间件
- koa-logger  ： 日志记录中间件
- @koa/cors  ： 官方中间件。支持CORS跨域的中间件
- @koa/multer  ： 官方中间件，借鉴了 `koa-multer` 用户处理文件上传的中间件
- koa-connect  ： 将express或connect中间件转换为koa中间件
- http-proxy-middleware ： 代理中间件
- connect-history-api-fallback ： 单页应用支持
- koa-convert  ： 用于将旧版本的koa中间件转换为koa2中间件

[项目案例](https://github.com/belong-you/chatRoom_vue3/tree/server) github