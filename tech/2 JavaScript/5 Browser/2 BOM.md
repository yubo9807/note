# BOM

- BOM 浏览器对象模型：主要处理浏览器窗口（window）和框架（iframe），描述了与浏览器进行交互的方法和接口，可以对浏览器窗口进行访问和操作，不过通常浏览器特定的JavaScript扩展都被看做BOM的一部分

## Window

- innerWidth ：浏览器窗口宽度（可读不可写）
- innerHeight ：浏览器窗口高度
- pageXOffset ：横向滚动条偏移量（可读不可写）
- pageYOffset ：纵向滚动条偏移量
- screenX || screenLeft ：浏览器距离屏幕的左边距（可读不可写）
- screenY || screenTop ：浏览器距离平魔的上边距
- alert(); confirm(); prompt(); ：弹窗
- close(); ：关闭浏览器
- open('http://www.baidu.com', 'bozai', 'width=100,height=100'); ：打开新窗口
- scrollBy(0, 300) ：指定的像素值来滚动内容
- scrollTo(0, 300) ：把内容滚动到指定坐标

## Navigator 返回浏览器配置属性

- cookieEnabled; ：若启用 cookie 返回 true，否则返回 false
- onLine ：监测系统是否处于脱机模式（断网）
- userAgent ：返回客户机发送服务器的 user-agent 头部的值

## History 返回该浏览窗口的历史

- length ：浏览器历史记录列表中的 url 数量
- back() ：浏览器 history 列表中的前一个 url
- forward() ：浏览器 history 列表中的后一个 url
- go() ：浏览器 history 列表中的某个具体页面

## Location 返回窗口装载的 html 文档 url

- protocol ："http:" 协议
- host ："www.baidu.com" 域名
- pathname ："/s" 地址
- search ：? 参数
- hash ：# 锚点（单页面应用）
- assign('https://www.baidu.com') ：加载新的文档
- reload() ：拉取新页面 参数为true时刷新
- replace() ：页面替换

## Screen 返回当前浏览者屏幕对象（兼容性很差）

- availHeight(); ：窗口可使用的屏幕高度，单位像素
- availWidth(); ：窗口可使用的屏幕高度
- colorDrepth(); ：用户浏览器表示的颜色位数

## document  返回装载的 html 文档

- moveBy(); moveTo(); ：移动窗口（谷歌、火狐不兼容）
- resizeBy(); resizeTo(); ：重设窗口大小（谷歌、火狐不兼容）
- scrollBy(); scrollTo(); ：滚动窗口
- open(); ：打开新页面
- setInterval(); clearInterval(); ：设置、删除定时器
