# CSS

> CSS 全称： cascading style sheet [CSS 官网](https://www.w3.org/TR/CSS22/)

> [Chrome 默认样式表](https://github.com/chromium/chromium/blob/main/third_party/blink/renderer/core/html/resources/html.css)

## CSS 引入:

#### 1. 行间样式

```html
<div style="color: red"></div>
```

#### 2. 页面级 css

```html
<style type="text/css"></style>
```

#### 3. 外部 css 文件

```html
<link rel="stylesheet" type="text/css" href=""></link>
<!-- rel="stylesheet" 告诉浏览器文件类型是 css，href 是 css 文件的地址 -->
```

> 开发规范：结构html 样式css 行为js相分离

## 选择器:

- id 选择器: 特点 一个元素只能有一个 id 值，一个 id 只能对应一个元素，一一对应
- class 选择器: （最常用的选择器）特点 一个 class 可以对应多个元素
- 标签选择器: 特点 如果只写一个标签选择器，不管被嵌套多少层都会被选出来，而且是全部
- 通配符选择器: * 是任意的意思，此处表示 all，所有的标签（包括html>和body>）

## css 权重值: 

|  标签名 | 权重值 |
| --- | --- |
| !important | infinity正无穷 |
| 行间样式 | 1000 |
| id 选择器 | 100 |
| class 选择器 or 属性选择器 or 伪类选择器 | 10 |
| 标签选择器 or 伪元素选择器 | 1 |
| 通配符选择器 | 0 |

> !important > 行间样式 > id > class | 属性 > 标签选择器 > 通配符选择器
> (在计算机中，正无穷+1 > 正无穷)
> (如果权重值一样，则优先级一样，后面的会覆盖前面的)
> (css 权重中，为 256 进制)

```html
<div id="id" class="demo" type="div">demo</div>
```

```css
#id.demo { color: orange }  /* 100 + 10 = 110 */
div#id { color: yellow }  /* 1 + 100 = 101 */
div.demo:hover { color: red }  /* 1 + 10 + 10 = 21 */
div.demo[type='div'] { color: green }  /* 1 + 10 + 10 = 21 */
```

## 复杂选择器:

```html
<div><span><em></em></span></div><div class="name"></div>
```

#### 父子选择器(派生选择器)

```css
div span em{
    display: block;
    height: 100px;
    width: 100px;
    background-color: #f00;
}
```

#### 直接子元素选择器

```css
span > em{
    display: block;
    height: 100px;
    width: 100px;
    background-color: #f00;
}
```

#### 并列选择器

```css
div.name{
    height: 100px;
    width: 100px;
    background-color: #f00;
}
```

> 要么用 id 选择器，要么用并列选择器。在并列选择器中，标签选择器和 id 选择器和 class 选择器在一起，标签选择器必须放前面

#### 分组选择器（常用选择器）

```css
div, .name{
    height: 100px;
    width: 100px;
    background-color: #f00;
}
```

#### 伪类选择器

```css
em:hover{
    display: block;
    height: 16px;
    width: 30px;
    background-color: #f00;
}
```

> :link 未访问的链接  :visited 已访问的链接  :hover 鼠标移动到链接上  :active 选定的链接  :focus 聚焦状态

#### 伪元素选择器

```css
span::before{
    content: "波仔";  /* 插入内容 */
    padding: 5px;
}
span::after{
    margin: 0;
}
```

## 元素类型

1. 行级元素：
    - 内容决定元素所占位置
    - 不可通过css改变宽高
    - span strong em a del
2. 块级元素：
    - 独占一行
    - 可通过css改变宽高
    - div p ul li ol form address
3. 行级块元素：
    - 内容决定大小，块级元素的后代
    - 可通过css改变宽高
    - img
