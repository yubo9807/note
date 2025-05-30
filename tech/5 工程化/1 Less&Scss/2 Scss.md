# Scss

[Scss中文文档](https://www.sass.hk/docs/)

### 变量定义

```scss
$gray: #999;  // 变量
$rice: #ffcf76;
$grass: #58fc73;
$side: top;
```

### 暴露到全局

```scss
.sty{
    $width: 200px !global;
}
```

### 父级引用

```scss
.box{
    color: $gray;
    &:hover{
        cursor: pointer;
    }
}
```

### 继承选择器

```scss
.content{
    @extend .box;
    width: $width;
    height: $width * .7;
    background: $rice;
}
```

### 类名嵌套

```scss
.item-border {
    border: {
        style: solid;
        left: {
            width: 1px;
            color: red;
        }
        right: {
            width: 2px;
            color: blue;
        }
    }
}
```

### 变量引用

```scss
.round-#{$side} {
    border-#{$side}: 10px;
}
```

### 定义模块

```scss
@mixin name($width, $height, $radius) {
    width: $width;
    height: $height;
    border-radius: $radius;
    background: $grass;
}
```

### 调用模块

```scss
.round{
    @include name(100px, 100px, 50%);
}
```

### if 条件

```scss
$navbar-width: 800px;
$item: 5;
p {
    @if $navbar-width/$item - 10px < 200 { border: 2px dotted; }
    @if $navbar-width/$item - 10px == 150 { border: 1px solid; }
}
```

### for 循环

```scss
@for $i from 1 to 5 {
    .border-#{$i} {
        border: #{$i}px solid blue;
    }
}
```

### while 循环

```scss
$i: 1;
@while $i < 5 {
    .border-#{$i} { border: #{$i}px solid blue; }
    $i: $i + 1;
}
```

### each 循环

```scss
$arr: top, right, bottom, left;
@each $item in $arr {
    .icon-#{$item} {
        background-image: url("/image/#{$item}.jpg");
    }
}
```

### 自定义函数

```scss
@function double($n) {
    @return $n * 2;
}
#navbar {
    width: double(5px);  // 函数调用
}
```
