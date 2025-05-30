# canvas

```html
<canvas width='800px' height="600px" style="border:1px solid #000"></canvas>
<script>
    var canvas = document.getElementsByTagName('canvas')[0];
    var ctx = canvas.getContext('2d');

// 矩形
    ctx.fillStyle = '#f00';  // 填充绘画的颜色、渐变或模式
    ctx.rect(   20,     20,   100,  50);
            // 左边距、上边距、 宽、  高
    ctx.stroke();
    ctx.fill();

    ctx.strokeRect(130, 20, 50, 100);  /* 矩形 */
    ctx.fillRect(190, 20, 50, 100);  // 填充矩形

// 画线
    ctx.beginPath();  // 重置路径
    ctx.moveTo(250, 20); // 起点
    ctx.lineTo(300, 20);  // 添加一个新点
    ctx.lineTo(300, 100);
    ctx.closePath();  // 闭合
    ctx.lineWidth = 1;  // 线宽
    ctx.strokeStyle = '#0f0';  // 笔触的颜色、渐变或模式
    ctx.lineCap = 'round';  // 线条的结束端点样式
    ctx.stroke();  // 绘制已定义的路径
    ctx.fill();  // 填充

// 圆
    ctx.beginPath();
    ctx.arc(370, 70,  50,      0,    1.5 * Math.PI,  false );
            // 圆心、 半径、 起始位置，   结束位置、    逆时针
    ctx.stroke();

// 圆角
    ctx.beginPath();
    ctx.moveTo(440, 20);  // A
    ctx.arcTo(  520,  20,  520,  90,  50);  // 创建两切线之间的弧/曲线
            // B(x,   y)  C(x,   y)   半径
    ctx.stroke();

// 二次贝塞尔曲线
    ctx.beginPath();
    ctx.moveTo(20, 200);
    ctx.quadraticCurveTo(50, 120, 188, 200);  // 创建二次贝塞尔曲线
    ctx.strokeStyle = 'blue';
    ctx.stroke();

// 三次贝塞尔曲线
    ctx.beginPath();
    ctx.moveTo(250, 200);
    ctx.bezierCurveTo(300, 150, 350, 250, 400, 200);  // 创建三次贝塞尔曲线
    ctx.stroke();

// 变换        
    ctx.save();  // 保存 (坐标系的平移数据，缩放等)
    ctx.beginPath();
    ctx.translate(20, 250);  // 移动
    ctx.rotate(Math.PI * .25);  // 旋转
    ctx.scale(1.4, 1);  // 缩放 （改变的是坐标轴的比例，而不是尺寸）
    ctx.moveTo(0, 0);
    ctx.lineTo(100, 0);
    ctx.stroke();
    ctx.restore();  // 还原

// 背景
    let img = new Image();
    img.src = './img/img1.jpg';
    img.onload = () => {
        ctx.save();
        ctx.beginPath();
        ctx.translate(160, 250);
    //     let bg = ctx.createPattern(img, 'no-repeat');
    //     ctx.fillStyle = bg;
    //     ctx.fillRect(0, 0, 200, 100);

        ctx.drawImage(img, 0, 0, 200, 100);  // 设置图像大小
        // 背景图片         起点、 bg-size
        ctx.drawImage(img, 0, 0,     3840, 2160,   50, 50, 100, 50);
        // 图像裁剪        偏移像素、 图片大小(像素)、 起点、  宽、 高
        ctx.restore();
    }

// 属性
    ctx.save();
    ctx.beginPath();
    ctx.translate(400, 250);
    let clg = ctx.createLinearGradient(0, 0,  50, 50);  // 渐变
                                    //  起点、 宽、高
    clg.addColorStop(0, '#f00');
    clg.addColorStop(1, '#ff0');
    ctx.fillStyle = clg;
    ctx.globalAlpha = .5;  // 透明度
    ctx.shadowColor = 'rgba(0, 0, 0, .6)';  // 阴影
    ctx.shadowOffsetX = 10;
    ctx.shadowOffsetY = 10;
    ctx.shadowBlur = 10;  // 模糊度
    ctx.fillRect(0, 0, 50, 100);
    ctx.restore()

// 镜像渐变
    ctx.save();
    ctx.beginPath();
    ctx.translate(500, 250);
    let crg = ctx.createRadialGradient(50, 50,   0,   50, 50,   80);
                                    //  圆心1、 半径、  圆心2、  半径
    crg.addColorStop(0, 'red');
    crg.addColorStop(.5, 'orange');
    crg.addColorStop(1, 'yellow');
    ctx.fillStyle = crg;
    ctx.fillRect(0, 0, 100, 100);
    ctx.restore();

// 文字
    ctx.beginPath();
    ctx.font = '60px Georgia';
    ctx.strokeText('hello', 20, 440);
    ctx.fillText('bozai', 200, 440);

// 线
    ctx.beginPath();
    ctx.lineWidth = 10;
    ctx.moveTo(450, 440);
    ctx.lineTo(550, 440);
    ctx.lineTo(450, 400);
    ctx.lineCap = 'butt';  // butt square round  端点
    ctx.lineJoin = 'round'; // bevel miter round  拐角
    ctx.miterLimit = 5;  // 边角阶段处理
    ctx.stroke();

// 混合模式
    ctx.save();
    ctx.fillRect(20, 500, 100, 50);
    ctx.globalCompositeOperation = 'lighter';
    ctx.fillStyle = '#0f0';
    ctx.fillRect(60, 520, 100, 50);
    ctx.restore();

// 文字对齐方式
    ctx.lineWidth = 1;
    ctx.strokeRect(250, 500, 200, 50);
    ctx.textAlign='left';
    ctx.textBaseline='middle';
    ctx.fillText('hello', 250, 500);
</script>
```
