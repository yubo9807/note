## AJAX

```js
var xhr = null;
if (window.XMLHttpRequest) {
    xhr = new XMLHttpRequest();
} else {
    xhr = new ActiveXObject("Microsoft.XMLHttp");  // IE6
}
console.log(xhr.readyState);  //--> 0 创建
xhr.open("get", "https://open.duyiedu.com/jq/person");  // 建立连接
// 如果open第三个参数传true，或者不传，为异步模式。如果传false，为同步模式。
console.log(xhr.readyState);  //--> 1
xhr.onreadystatechange = function () {
    console.log(xhr.readyState);  //--> 2 3 4
    //readyState == 4 接收
    //status == 200  网络请求，结果都会有一个状态码。来表示这个请求是否正常
    /* http状态码
        2**表示成功
        3**表示重定向，地址迁移
        4**表示客户端错误，404页面没找到。
        5**表示服务端错误
    */
    if (xhr.readyState == 4 && xhr.status == 200) {
        var data = JSON.parse(xhr.responseText);
        console.log(data);
    }
}
xhr.send(); // 发送
```

> 在计算机的世界里，异步与同步和现实世界中是相反的。
> 在计算机的世界里，同步表示串行。异步表示同时进行。可以理解为同线程和异线程。
