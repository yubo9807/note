## $.when()

```js
$.when(creatScore1(), creatScore2(), creatScore3(),)
    .then(function () {  // 全部成功执行
        console.log('yach');
    }, function () {  // 有一个失败就执行
        console.log('no');
    });    

function creatScore1 () {
    var df = $.Deferred();
    setInterval(() => {
        var score = Math.random() * 100;
        score > 70 ? df.resolve() : df.reject();
    }, 1000);
    return df.promise();
}
function creatScore2 () {
    var df = $.Deferred();
    setInterval(() => {
        var score = Math.random() * 100;
        score > 60 ? df.resolve() : df.reject();
    }, 1000);
    return df.promise();
}
function creatScore3 () {
    var df = $.Deferred();
    setInterval(() => {
        var score = Math.random() * 100;
        score > 30 ? df.resolve() : df.reject();
    }, 1000);
    return df.promise();
}
```