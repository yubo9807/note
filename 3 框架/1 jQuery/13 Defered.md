## $.Deferred() 延迟

```js
var df = $.Deferred();
// done 成功   fail 失败    progress 正在进行
// resolve     reject       notify

function creatScore () {
    var df = $.Deferred();
    setInterval(() => {
        var score = Math.random() * 100;
        if (score > 70) {
            df.resolve('congradulation');
        } else if (score < 50) {
            df.reject('get out');
        } else {
            df.notify('go on');
        }
    }, 1000);
    return df.promise();
}
var df = creatScore();
// // 注册成功的回调函数
// df.done((ms) => console.log('oh Yeah!!!', ms));
// // 注册失败的回调函数
// df.fail((ms) => console.log('oh No...', ms));
// // 注册进行时的函数
// df.progress((ms) => console.log('waiting~~~', ms));

// then 简化写法
df.then(() => {  // done
    console.log('oh Yeah!!!');
    return 'ok';
}, () => {  // fail
    console.log('oh No...');
    return 'no';
}, () => {  // progress
    console.log('waiting~~~');
    return 'go on';
}).then((param) => {  // 再次调用 then 指向就不是 df 了
    console.log('泡妞', param)
}, (param) => {
    console.log(param, '脸');
}, (param) => {
    console.log(param, '加油');
});
```
