# 移动端 bug

## 固定定位问题

- 在页面有滚动条，flex 定位的情况下：会出现定位问题
    - 借助相对定位、绝对定位解决

## 1px 问题

```css
@media screen and (-webkit-min-device-pixel-ratio: 2) {
    #list h3::after {
        content: '';
        position: absolute;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 1px;
        background: #000;
        color: #c1c0c5;
        transform-origin: 0 0;
        transform: scaleY(.5);
    }
}
```

## 图片模糊问题

```html
<!-- 根据不同 DPR 设置不同路径 -->
<img src='1x.png' srcset='2x.png 2x, 3x.png 3x' />

<style>
    img{
        -webkit-img-set: 1.png 1x, 2x.png 2x, 3x.png 3x;
    }
</style>
```

