# HTML

[W3C官方文档](https://www.w3school.com.cn/)  [HTML 官方文档](https://html.spec.whatwg.org/multipage/)

```html
<!DOCTYPE html>  <!-- 开启 html 标准模式，没有则为混杂模式 -->
<html lang="en">  <!-- 根标签 
                       lang="en" 告诉搜索引擎爬虫，网站是关于什么内容的
                       "en"(英文) "zh"(中文) "de"(德语) -->
<head>  <!-- 一些思想，给浏览器看的 -->
    <meta charset="UTF-8">  <!-- 等号前面是属性名，后面是属性值（属性值必须加引号）
                                 "UTF-8" (unicode)万国码，包括了所有国家的语言
                                 "gb2312" 国家编码字符集（简体，亚裔字符集）
                                 "gbk" gb2312+繁体 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>html笔记</title>  <!-- 标题栏 -->
</head>
<body>  <!-- 展示给用户看的 -->
    <p>段落标签</p>
    <h1>标题标签</h1>  <!-- <h1>-<h6> -->
    <strong>加粗</strong>
    <em>斜体</em>
    <del>中划线</del>
    <address>地址</address>  <!-- 可以成段倾斜展示 -->
    <div>容器</div>  <!-- 独占一行 -->
    <span>容器</span>  <!-- 不独占一行 -->
    <!-- <div>和<span>两个标签是为了成块展示，规格化
         分块明确，让整个页面更加结构化；捆绑操作的作用（搬书架） -->
         
    <!-- 空格的含义是英文单词分隔符，不代表文本中的空格，打多少空格都只显示一个空格；回车也是文字分隔符 -->
    &nbsp;  <!-- 空格 -->
    &lt;  <!-- 左尖角号 -->
    &gt;  <!-- 右尖角号 -->
    <br>  <!-- 回车换行 -->
    <hr>  <!-- 水平线 -->

    <ol type="a" start="6" reversed="reversed">  <!-- 有序列表
                                                      这里的排序值只有5个："a" / "A" / "i" / "I" / "1" 
                                                      reversed="reversed" 倒叙排列 -->
        <li>举个例子</li>
        <li>举个例子</li>
        <li>举个例子</li>
    </ol>

    <ul type="disc">  <!-- 无序列表（<ul>只有 type 一个属性可以改）
                            disc 实心圆
                            spuare 实心方块
                            circle 空心圆 -->
        <li>举个例子</li>
        <li>举个例子</li>
        <li>举个例子</li>
     </ul>  <!-- <ul>和<li>是一对很好的父子结构，可以做导航栏，可维护性好 -->

    <img src="" alt="" title="">  <!-- 图片标签  
                                        1.网上地址
                                        2.本地路径：绝对路径
                                                   相对路径
                                        src="" 占位符（当图片无法显示的情况下起到占位作用）
                                        alt="" 提示符（鼠标移向图片是起提示作用） -->

    1.  <a href=""></a>  <!-- 本页超链接 -->
        <a href="" target="blank"></a>  <!-- 新页超链接 -->
    2.  <div id="顶部">顶部</div>  <!-- 锚点 -->
        <a href="#顶部">回到顶部</a>   
    3.  <a href="tel:18235557369">电话号码</a>  <!-- 触发其他应用 -->
        <a href="mailto:1781926993@qq.com">邮箱号</a>
    4.  <a href="javascript: while(1){alert('让你手欠')}">死循环</a>  <!-- 协议签订符 -->

    <form method="get" action="">  <!-- 前端向后端发送数据的一个表单
                                        method="get" 数据发送方式
                                        action="" 数据接收地址 -->
        <p>
            账号：<input id="" class="" type="text" autocomplete="off" maxlength="100" name="账号" placeholder="请输入账号">
                    <!-- autocomplete 属性启用自动完成功能的表单
                         maxlength 属性规定输入字段的最大长度，以字符个数计。
                         placeholder 属性提供可描述输入字段预期值的提示信息（hint）该提示会在输入字段为空时显示，并会在字段获得焦点时消失。 -->
        </p>
        <p>
            密码：<input id="" class="" type="password" autocomplete="off" maxlength="100" name="密码" placeholder="请输入密码">
        </p>  <!-- 要注意语义化，所以<p>标签更好，<p>天生的功能就是换行 -->
        <input type="submit" value="注册">
        <input type="submit" value="登录">  <!-- text      输入框
                                                 sublime   按钮
                                                 password  密码框
                                                 radio     单选框
                                                 checkbox  复选框
                                                 checked="checked" 默认选框
                                                 email     邮箱 -->
    </form>  <!-- 发送数据要注重（数据名）和数据的内容（数据值），缺一不可，没有这个就发送不了数据 -->
    <form action="">
        <select name="地址" id="">  <!-- 下拉菜单 -->
            <option value="北京">北京</option>
            <option value="上海">上海</option>
            <option value="天津">天津</option>
        </select>
        <input type="submit">
    </form>

    <p>
        <label for="demo">username</label>  <!-- for 为了谁 -->
        <input type="text" id="demo">
    </p>

    <!-- 主流浏览器和内核，主流浏览器是有一定市场份额，并且有自己独立研发的内核
         浏览器分 shell+内核
         主流浏览器（必须有独立内核）市场份额大于3%        内核
                    IE                              trident
                    Friefox                         Gecko
                    Google chrome                   Webkit/blink
                    Safari                          Webkit
                    Opera                           presto -->

    <!-- 属性、特性
         特性：id / class / type  特性与DOM对象一一对应，映射关系
         属性：data cst -->

</body>
</html>
```