# TypeScript

## JS 开发中常见的一些问题

```js
function getUserName () {
    if (Math.random() < .5) return 'hello word';
    return 404;
}

let myname = getUsername();  // 使用不存在的函数
mynema = myname.split(' ')  // myname 类型不确定
               .fillter(it => it)
               .map(it => it[0].touppercase() + it.subStr(1))
               .json(' ');
```

> JS 语言本身的特点，决定了该语言无法适应大型的项目

- 弱类型：某个变量，可以随意更换类型
- 解释型：错误发生的时间在运行时

#### 为什么要用 TS ：缩减项目周期，提高开发效率，少范低级错误

## TS

[官方文档](https://www.typescriptlang.org/docs) 
[中文文档](https://www.tslang.cn/docs/home.html)

> 2012 微软 Anders Hejlsberg 负责开发（开源，拥抱 ES 标准）

- TypeScript 是 JS 的超集，是一个可选的、静态的类型系统
    - 类型系统：对代码中所有的标识符（变量、函数、参数、返回值）进行类型检查
    - 可选：随意选择
    - 静态：无论是浏览器还是 node 环境，都无法直接识别 .ts 文件（TS 不参与运行时的类型检查）

## 使用

- 安装： `npm i -g typescript`
- 编译： tsc（需要配置文件） | tsc index.ts（忽略配置文件）
- 生成配置文件： tsc --init

##### tsconfig.json

```json
{
    "compilerOptions": {
        "target": "es3",                       // 配置编译目标代码的版本标准
        "module": "commonjs",                  // 编译目标使用的模块化标准
        "lib": ["es2016"],                     // 类型检查标准
        "outDir": "./dist",                    // 编译后文件目录
        "moduleResolution": "node",            // 模块解析策略方式
        "strictNullChecks": true,              // 更加严格的空类型检查
        "removeComments": true,                // 移除注释
        "noImplicitUseStrict": true,           // 不使用严格模式
        "noEmitOnError": true,                 // 检查错误不执行编译
        "esModuleInterop": true,               // 启用 es 模块化交互非 es 模块导出
        "noEmitOnError": true,                 // 错误时不生成编译结果
        "strictPropertyInitialization": true,  // 更加严格的方式检查属性有无初始化
        "declaration": true,                   // 编译自动生成 .d.ts 文件
        "sourceMap": true,                     // 编译自动生成 .map 文件，用于调试
        "experimentalDecorators": true,        // 开启试验性质的装饰器功能
        "emitDecoratorMetadata": true,         // 源数据反射
        "experimentalDecorators": true,        // 装饰器开启
    },
    // "files": ["./src/index.js"],            // 编译指定文件
    "include": ["./src"], // 编译指定目录
}
```

> 没有不支持 node 环境，需要安装 npm i -D @types/node （@types 官方出品配置库）

### nodemon 监控文件变化

> nodemon --watch src -e ts --exec tsc  只监控 src 目录下的 .ts 文件

## 搭建 React + TypeScript 项目

- 安装 React ： `npm i -g create-react-app`
- 创建 React TS 项目 ： `create-react-app test --typescript`
