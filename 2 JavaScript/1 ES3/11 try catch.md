# try catch

```js
try {
    // 在 try 里面的发生错误，不会执行错误后的 try 里面的代码
    console.log('a');  //--> a
    console.log(b);  //--> ReferenceError:b is not defined
    console.log(c);
    console.log('d');
} catch (e) { // error  error.message, error.name --> error
    // 捕捉错误信息
    console.log(e.name + ":" + e.message);
}
console.log('f');  //--> f
```

## Error.name 的六种值对应的信息

- EvalError： eval() 的使用与定义不一致
- RangeError： 数值越界
- ReferenceError： 非法或不能识别的引用数值
- SyntaxError： 发生语法解析错误
- TypeError： 操作数类型错误
- URIError： URI 处理函数使用不当
