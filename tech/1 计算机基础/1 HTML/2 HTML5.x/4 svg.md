# svg

```
                                    <!-- 比例尺 -->
<svg width="700px" height="400px" viewbox="0,0,700,400" style="border: 1px solid">
    <style>
        line{
            stroke: black;
            stroke-width: 1px;
            stroke-dasharray: 10px 2px 5px;
                    /* 虚线   线长、空隙、线长(挨个拿) */
            stroke-dashoffset: 5px;  /* 向前偏移 */
        }
        polyline, polygon{
            fill: none;
            stroke: red;
        }
        text{
            font-size: 40px;
            stroke: orange;
            fill: none;
        }
        .test{
            stroke: red;
            stroke-opacity: .5;
            stroke-width: 10px;
            fill: orange;
            stroke-linejoin: bevel;  /* square miter round bevel */
        }
        path{
            stroke: red;
            fill: none;
        }
        .demo{
            fill: url(#lg);
            filter: url(#gaussian);
        }
    </style>
    <!-- 线 -->
    <line x1="20" y1="20" x2="20" y2="100" />
    <!-- 矩形 -->
    <rect x="40" y="20" width="50" height="80" />
    <!-- 圆 -->
    <circle r="40" cx="150" cy="60" />
    <!-- 椭圆 -->
    <ellipse rx="20" ry="40" cx="230" cy="60" />
    <!-- 折线 -->
    <polyline points="270 20, 280, 100, 300, 60" />
    <!-- 多边形 -->
    <polygon points="320 20, 330, 100, 350, 60" />
    <!-- 文本 -->
    <text x="370" y="70">bozai</text>
    <rect class="test" x="500" y="40" width="80" height="50" />

    <!-- 大写：绝对位置，小写：相对位置 -->
    <!--     开始     到                  横向   纵向  闭合-->
    <path d="M 20 120 L 100 120 l -80 30  H 60  V 180  z"/>
    <!--         起点  圆弧 长短半径 旋转角度 长弧 顺时针   终点 -->
    <path d="M 120 150  A   70 20     0      1    1    180 170"></path>
    
    <!-- 定义 -->
    <defs>
        <!-- 渐变 -->
        <linearGradient id='lg' x1='0' y1='0' x2='0' y2='100%'>
            <stop offset="0%" style="stop-color: yellow"></stop>
            <stop offset="100%" style="stop-color: red"></stop>
        </linearGradient>
        <!-- 高斯模糊 -->
        <filter id="gaussian">
            <feGaussianBlur in="SourceGraphic" stdDeviation="10"></feGaussianBlur>
        </filter>
    </defs>

    <rect class="demo" x="20" y="200" width="50px" height="100px"></rect>

</svg>
```