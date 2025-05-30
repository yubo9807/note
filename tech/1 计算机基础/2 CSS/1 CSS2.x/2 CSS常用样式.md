## css 常用样式

[CSS 参考手册](http://css.cuishifeng.cn)

```css
.text{
    text-align:left;  /* 左对齐 */
    text-align:center;  /* 居中 */
    text-align:right;  /* 右对齐 */
    text-indent:2em;  /* 首行缩进  1em = 1 * font-size; */
    text-decoration: line-through;  /* line-through中划线
                                       underline; 下划线
                                       overline; 上划线
                                       none; 消除属性 */
}
.font{
    font-family: arial;  /* 使用某个字体或字体序列
                            arial | georgia | verdana | helvetica | simsun and etc. */
    font-size: 16;  /* 字体大小 */
    color: #f00;  /* 字体颜色 */
    font-weight: bold;  /* 字体粗细
                           normal 正常的字体相当于数字值400
                           bold 粗体相当于数字值700
                           bolder 定义比继承值更重的值
                           lighter 定义比继承值更轻的值
                           [integer] 用数字表示文本字体粗细取值范围 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 */
    font-style: italic;  /* 字体样式
                            normal 字体样式为正常的字体
                            italic 字体样式为斜体对于没有设计斜体的特殊字体，如果要使用斜体外观将应用oblique
                            oblique 字体样式为倾斜的字体人为的使文字倾斜，而不是去选取字体中的斜体字 */
    font-variant: small-caps;  /* 是否为小型的大写字母
                                  normal 正常的字体
                                  small-caps 小型的大写字母字体 */
    line-height: normal;  /* 文本字体行高
                             normal 允许内容顶开或溢出指定的容器边界
                             [length] 用长度值指定行高不允许负值
                             [percentage] 用百分比指定行高，其百分比取值是基于字体的高度尺寸不允许负值
                             [number] 用乘积因子指定行高不允许负值 */
}
.border{
    width: 300px;
    height: 100px;
    background-color: #f00;
    border: 5px solid #000;
    border-top-width: 10px;
    border-bottom-color: #ff0;
    border-top-style: dashed;  /* dashed 条虚线
                                  dotted 点虚线 
                                  solid 实线  */
}
.display{
    display: inline;  /* inline 行级元素
                         block 块级元素
                         inline-block 行级块元素（凡是带有inline属性都有文字特性） */
}
.cursor{
    cursor: pointer;  /* pointer    小手
                         help       问号 
                         auto       默认光标
                         crosshair  十字线
                         move       对象可被移动
                         text       文本
                         wait       程序正忙
                         e-resize	向右移动
                         n-resize	向上移动
                         s-resize	向下移动
                         w-resize	向左移动
                         ne-resize	向上及向右移动
                         nw-resize	向上及向左移动
                         se-resize	向下及向右移动）
                         sw-resize	向下及向左移动 */
}
.position{
    position: absolute;  /* absolute 绝对定位（脱离原来位置进行定位） 
	                          relative 相对原来位置定位（保留原来位置进行定位）
		                        fixed 固定定位 */
    left:200px;  /* 左边距 */
    top:100px;  /* 上边距 */
    opacity:0.5;  /* 透明度 */
    clear:both;  /* 清除浮动流，只对块级元素有作用 */
}
/* position: absolute;float: left;打内部把元素转换为 inline-bloak */
.bfc{
    position: absolute;
    display: inline-block;
    /* float: left; */
    overflow: hidden;  /* 溢出部分隐藏 */
}  /* 解决 margin 塌陷 */
.float{
    float: left;
}
/* 浮动元素会产生浮动流
   所有产生了浮动流的元素，块级元素看不到他们；
   产生bfc的元素和文本类属性（inline）元素及文本都能看到浮动流 */
ul::after{
    content: "";
    display: block;
    clear: both;
}  /* 清除浮动流三件套 */
div{
    white-space: nowrap;  /* 失去换行功能 */
    overflow: hidden;
    text-overflow: ellipsis;  /* 溢出部分打点展示 */
}
/* 行级元素只能嵌套行级元素 a 嵌套 a 除外
   块级元素能嵌套任何元素 p 嵌套 div 除外 */
.background{
    background: url("") no-repeat 50% 50% / 100% 100%; 
    background-image: url("");  /* 背景图片 */
    background-size: 100% 100%;  /* cover 按短边扩展剪切
                                    contain 按长边扩展 */
    background-repeat: no-repeat;
    background-position: center center;
    backface-visibility: hidden;  /* 设置元素背面不可见 */

}
.transfrom{  /* 转换 */
    transform: translate(50px,50px);  /* 元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标） 位置参数 */
    transform: rotate(45deg);  /* 元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转 */
    transform: scale(1.5, 0.8);  /* 元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数 */
    transform: skew(25deg, 25deg);  /* 元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）参数 */
}
.transition{  /* 过渡 */
    transition: all 2s;
    transition-property: all;	 /* 规定设置过渡效果的 CSS 属性的名称。*/
    transition-duration: 2s;  /* 规定完成过渡效果需要多少秒或毫秒。 */
    transition-timing-function: linear;	 /* 速度曲线。 */
    transition-delay: 1s;  /* 动画延迟 */
}
.filter{
    filter: blur(10px);  /* blur(10px) 模糊度 */
                         /* brightness(200%) 明暗 */
                         /* contrast(200%) 对比度 */
                         /* drop-shadow(10px 10px 5px #000) 阴影 */
                         /* hue-rotate(90deg) 色相 */
                         /* invert(100%) 反向 */
                         /* saturate(10%) 饱和度 */
                         /* sepia(100%) 复古 */
                         /* opacity(30%) 透明度 */
}
```
