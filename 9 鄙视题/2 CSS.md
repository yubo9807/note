# CSS

## 浏览器中默认 margin 值是多少？

- 8px
- IE7：margin-top:15px; margin-left:10px;

## margin: auto 是如何解析的？

- 块级元素：
    1. 给auto后必定会有一个值，
    2. 自动分配剩余空间
    3. 文档规定 margin-top/bottom 设置为 auto 时值变为 0
- 行级元素：设置 auto 时没有一个特定的值，还是 auto
- 浮动元素：设置 auto 后会分配剩余可视空间

## 重绘与重排（回流）

- 重绘：不影响布局的属性
    - 元素背景色、文字颜色、边框颜色……
- 重排：影响布局的属性
    - 改变窗口大小、文字大小、内容改变、输入框文字、激活伪类 hover、类名操作、脚本操作 DOM、计算 offsetWidth、设置 style 属性
- CSS 开启 GPU 渲染加速：
    - opacity: 
    - will-change: 
    - transform: translateZ(0);  仅 z 轴有效

## CSS4 变量声明与使用

```css
:root {
    --Color: red;
}
.demo {
    color: var(--Color);
}
```

## em 和 px 的区别

- px：相对于分辨率长度的单位；
- em：相对于字体大小的长度单位；
- rem：相对于根节点 html 字体大小的长度单位。

## BFC 是什么，是怎样产生的，如何解决？

- BFC：全称为 块格式化上下文 (Block Formatting Context)
    - 使 BFC 内部浮动元素不会到处乱跑
    - 和浮动元素产生边界
- 如何创建 BFC：
    - 根元素或其它包含它的元素
    - 浮动元素 (元素的 float 不是 none)
    - 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
    - 内联块 (元素具有 display: inline-block)
    - 表格单元格 (元素具有 display: table-cell，HTML 表格单元格默认属性)
    - 表格标题 (元素具有 display: table-caption, HTML 表格标题默认属性)
    - 具有overflow 且值不是 visible 的块元素，
    - display: flow-root
    - column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被   - 包裹在一个多列容器中。
    - 一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。

## 如何理解 flex 的主轴与副轴，如何控制

## 使元素消失的几种方式

- 看不见，摸不着：
    - display: none;
- 看不见，摸得着（没有真正消失）：
    - overflow: hidden;
    - z-index: -1;
    - opacity: 0;
    - transform： translate(-100%);

## line-height: 2; 和 line-height: 200%; 的区别

- line-height: 2;  相对于自身的高度
- line-height: 200%;  相对于浏览器字体的 2 倍

## margin 塌陷问题

- 问题的产生：
    - 父元素与子元素同时具有 margin 属性都时，会发生 margin 值重复问题
- 解决方式：触发 BFC （margin 不会传递给父级）
    - 父元素设置 overflow: hidden;
    - 父元素改为 行级块元素 display: inline-block;
    - position，float

## 怎么解决两张图片中间的缝隙问题

1. 将 font-size 设置为 0

## link 标签与 @import 的区别

- link 支持并行下载，@import 过过嵌套会出现 FOUC（页面闪烁，花屏）；
- link 可指定候选样式；
- 可利用 @import 兼容性对老版浏览器样式进行隐藏。

## CSS 中有哪些继承属性

- 字体
    - font
    - word-break
    - word-spacing
    - letter-spacing
    - text-aline
    - text-indent
    - text-shadown
    - text-transform
    - text-rendering
    - white-space
- line-height
- color （a 标签除外）
- visibility
- cursor
