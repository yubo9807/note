# babel 转换

```js
module.exports = {
    module: {
        rules: [
            {test:/\.js/, use: 'babel-loader'}
        ]
    }
}
```

#### .babelrc

```json
{
    "presets": [
        ["@babel/preset-env", {
            "useBuiltIns": "usage",
            "corejs": 3
        }]
    ],
    "plugins": [
        [
            "@babel/plugin-proposal-class-properties", {
                "loose": true,  // 宽松模式
            },
            // "babel-plugin-transform-remove-console",  // 去除console内容
            "@babel/plugin-transform-runtime",  // 提取公共函数
        ]
    ]
}
```

`npx babel src -d dist`

