# ORM

[GitHub Sequelize 中文文档](https://github.com/demopark/sequelize-docs-Zh-CN)

> npm install --save sequelize
> npm install --save mysql2

```js
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize('user', 'root', '229237', {
    host: 'localhost',
    dialect: 'mysql',  // 数据库类型
});

// 测试连接
(async function () {
    try {
        await sequelize.authenticate();
        console.log('Connection has been established successfully.');
    } catch (error) {
        console.error('Unable to connect to the database:', error);
    }
}());
```
