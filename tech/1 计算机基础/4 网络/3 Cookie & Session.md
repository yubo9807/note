## Cookie

> Cookie是存在浏览器⾥的，不是存在某个⻚⾯上的。是可以⻓期存储的。Cookie即使是保存在浏览器⾥，也是存放在不同的域名下的。
> 缺点：复制浏览器⾥的cookie，可以在别的电脑上登录账号。XSS注⼊攻击。

1. 初始状态：没有登录
2. 访问百度的登录，输⼊⽤户名，密码。
3. 如果⽤户名和密码是正确的。百度的后端会向这个域名下，设置⼀个Cookie。写⼊⽤户
的基本信息（加密的）。
4. 以后每⼀次向百度发送请求，浏览器都会⾃动带上这些Cookie。
5. 服务端（后端）看到了带有ID的cookie，就可以解析这个加密的ID，来获取到这个⽤户
本身的ID。
6. 如果能获取到本身的ID，那么就证明这个⽤户已经登录过了。后端可以继续保留⽤户的信息。

### cookie 参数

- key :  键
- value ： 值
- domain ： 域，表示这个 cookie 是属于哪个网站的
- path ： 路径，表示这个 cookie 是属于网站的哪个基路径的
- secure ： 是否使用安全传输，false 请求协议为 http，true 请求协议为 https
- expire ： 过期时间，表示 cookie 什么时候过期（GMT 格式）
- max-age ： 多长时间后过期，单位 s，值设为 -1 删除该 cookie，过期
- httponly ： 设置 cookie 是否仅用于传输，不允许在客户端进行获取，可防止 XSS 攻击

> expire 和 max-age 都设置，会将两者就相加作为过期时间，如果都没有设置，则表示会话结束（关闭窗口）后过期

```js
// 服务器设置 cookie
res.header('set-cookie': 'token=1; domain=bozai.tech; path=/news; max-age=3600; httponly');

// 客户端设置 cookie
document.cookie = 'token=1; domain=bozai.tech; path=/news; max-age=3600';
```

## Session

- Session是存在服务器上的
1. 如果⽤户量⾮常⼤，上亿的⽤户。在⽤户量很⼤的情况下，服务器端很耗资源
2. 后端可能不⽌⼀台服务器，⽤户的登录信息，⼀般只存在⼀台服务器上
3. ⽤户的登录操作，在哪台机器上执⾏的，就⼀般存在哪台机器上
4. 需要通过反向代理。（轮询，IP哈希）
