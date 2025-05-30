# nodemon

> 安装：`npm i -D nodemon 执行：npx nodemon index.js`

##### nodemon.json 配置

```json
{
    "watch": ["*.js", "*json"],  // 只监控
    "ignore": ["pack.json", "nodemon.json", "node_medules"],  // 忽略
    "env": {  // 环境变量
        "NODE_ENV": "developmen"
    }
}
```

> `nodemon --exec tsc`
