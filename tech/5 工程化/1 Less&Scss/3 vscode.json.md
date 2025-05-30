# VSCode less，scss 文件配置

##### .vscode/settings.json

```json
{    
    // less 指定 css 文件保存位置
    "less.compile": {
        "out": "${workspaceRoot}\\css\\",  // 自定义css输出文件路径
    },
    
    // scss 指定 css 文件保存位置
    "easysass.formats": [
        {
            "extension": ".css",
            "format": "expanded",  // 不压缩
            // "format": "compressed",  // 压缩
        }
    ],
    "easysass.targetDir": "./css/"  // 自定义css输出文件路径
}
```
