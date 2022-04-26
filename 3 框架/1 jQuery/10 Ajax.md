## AJAX

```js
$.ajax({
    url: 'https://open.duyiedu.com/jq/person',
    type: 'GET',  // 请求方式
    async: true,  // 是否异步
    // dataType: 'jsonp',  // 跨域
    data: {},  // 参数，信息
    success: function (res) {  // 请求后的处理函数
        $.each(res.data, function (index, ele) {
            console.log(ele);
        })
    },
    error: function (e) {  // 错误信息
        console.log(e.status, e.statusText);
    },
    complete: function () {},  // 无论成功与否都会执行
    context: $('.wrapper'),  // 改变函数上下文
    timeout: 1000,  // 规定多长时间结束
})
```

```js
function deal (res) {
    console.log(res);
}
$.ajax({
    url: 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',
    type: 'GET',
    data: {
        wd: 'lol',
        cb: 'deal'
    },
    dataType: 'jsonp',
})
```
