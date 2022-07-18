## HTML 中 data- 属性的作用是什么，如何使用？

- 作用：自定义属性
- 使用：

```html
<div id="demo" data-author="david">hello</div>
<script>
    var demo = document.getElementById('demo');
    var str = demo.dataset.author;
    console.log(str);  //--> david
</script>
```

## 关于 preload 特性

- 提前加载资源，缓存资源（用到时从缓存中拿）；
- 资源加载和执行分离；
- 不延迟网页的 load 事件（除非 Preload 资源刚好是阻塞 window  加载的资源）；
- 仅限于解析 HTML 的外链资源，程序中的 异步加载 无法提前收到；

## 提前加载资源

- as：告诉浏览器异步加载文件的类型

```js
<link rel="preload" href="./index.js" as="script" />
<link rel="preload" href="./index.png" as="image" />
<link rel="preload" href="./index.mp4" as="video" type="video/mp4" />

<link rel="preload" href="./index.css" as="style" onload="this.rel='stylesheet'" />
<link rel="stylesheet" href="./other.css" media="none" onload="this.media='all'" />
```

