## HTTP协议

- 请求：Request
    - 请求方式 路径 协议版本
    - 请求方式：GET POST HEAD PUT DELETE
        - GET可在url中展示，用于传输字段，POST用于传输大型文件
        - GET和POST请求一样危险
- 响应：Response
    - 响应头
    - 数据体
    - 协议版本 状态码 message
    - 属性：值

## GET和POST请求方式的区别

### 是基于什么前提的？

- 如果什么前提都没有，不使用任何规范，只考虑语法和理论上的HTTP协议。GET和POST几乎是没有区别的，只有名字不一样

### 如果是基于RFC规范的

1. 理论上：GET和POST具有相同语法的，但是有不同的语义。GET是用来获取数据的，POST是用来发送数据的，其他方面没有区别
2. 实现上：各种浏览器，就是这个规范的实现者
    - GET的数据在URL是可见的。POST请求不显示在url中
    - GET对长度是有限制的，POST长度是无限的
    - GET请求的数据可以收藏为书签，POST请求到的数据不可收藏为书签
    - GET请求后，后退、刷新无影响，POST数据会重新提交
    - 编码类型
        - GET编码类型：application/x-www-form-url，
        - post编码类型有很多种：encodeapplication/x-www-from-urlencoded  multipart/form-data
    - GET历史参数会被保留在浏览器里，POST不会
    - GET只允许ASCII，POST没有编码限制，允许发二进制
    - GET与POST相比，GET安全性较差，因为所发的数据是url的一部分
