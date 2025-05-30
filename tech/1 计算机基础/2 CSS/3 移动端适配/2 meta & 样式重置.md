## meta

### viewport 设置

```html
<meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=no" />
```

| 属性 | 作用 |
| --- | --- |
| `width=device-width` |  设备实际宽度（一般不设置数值，有些移动端无法识别宽度适配） |
| `user-scalable=no` |  是否允许缩放（iOS10 无效，通过 js 事件解决） |
| `initial-scale=1` | 初始缩放值 |
| `minimum-scale=.5` |  最小缩放值 |
| `maximum-scale=1` |  最大缩放值 |

## 其他设置

```html
<!-- 禁止识别手机号、邮箱 -->
<meta name="format-detection" content="telephone=no, email=no" />

<!-- 设置添加主屏后的标题 -->
<meta name="apple-mobile-web-app-title" content="标题" />

<!-- 设置 webAPP logo -->
<link rel="apple-touch-icon-precomposed" href="img/logo.png" />

<!-- 设置全屏显示（无用） -->
<meta name="apple-mobile-web-app-capable" content="yes" />

<!-- 设置启动画面（无用） -->
<link rel="apple-touch-startup-image" href="img/logo.png" />

<!-- X5 内核浏览器（QQ、微信）-->
<meta name="X5-orientation" content="portrait">  <!-- portrait 强制竖屏
                                                      landscape  强制横屏-->
<meta name="X5-fullscreen" content="true">  <!-- 全屏（F11）-->

<!-- UC 内核浏览器 -->
<meta name="screen-orientation" content="portrait">  <!-- 强制竖屏 -->
<meta name="full-screen" content="yes">  <!-- 全屏 -->

<meta http-equiv="X-UA-Compatible" content="ie=edge">
```

## 样式重置

```css
body {
    font-family: Helvetica;  /* 移动端通用字体 */
    -webkit-text-size-adjust: 100%;  /* 禁止文字缩放（安卓不识别，通过 js 解决） */
    -webkit-user-select: none;  /* 取消文字选中（安卓不识别，通过 js 解决） */
    -webkit-touch-callout: none;  /* 禁止弹出系统菜单（安卓无效） */
    /* 移动端字体会有大小不一的情况，需手动设置高度 */
}

/* 移动端 a 标签点击时有默认阴影 */
a, input, button {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}

/* 对有些移动端按钮默认为圆角做恢复 */
input, button {
    -webkit-appearance: none;
    border-radius: 0;
}

input::-webkit-input-placeholder {
    color: black;
}
input:focus::-webkit-input-placeholder {
    color: red;
}
```

### 设备默认字体

- ios 
    - 默认中文字体： Heiti SC
    - 默认英文字体： Helvetica
    - 默认数字字体： HelveticaNeue
- android
    - 默认中文字体： Droidsansfallback
    - 默认英文，数字字体： Droid Sans

