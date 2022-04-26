# form 表单

```html
<form action="">
    <input type="email">  <!-- 判断是否是邮箱格式 -->
    <input type="range" max="100" min="0" step="10">  <!-- 与 number 功能相同，显示方式不同 -->
    <input type="search">  <!-- 与 text 格式相同，多一个删除按钮 -->
    <input type="tel">  <!-- 移动端电话格式 -->
    <input type="submit" value="提交">
    
    <input type="url" value="http:">  <!-- 判断是否是网址格式（只有chrome支持） -->
    <input type="range">  <!-- 进度条（火狐，IE不支持） -->
    <input type="color">  <!-- 选择颜色（safari，IE不支持） -->
    <input type="number" max="100" min="0" step="10">  <!-- 判断是否是数字格式 并提示数字间隔（safari,IE不支持） -->
    <input type="date">  <!-- 日期格式（只有chrome支持） -->
    <input type="month">  <!-- 日期月 -->
    <input type="week">  <!-- 日期周 -->
    <input type="time" value="12:00:00">  <!-- 时间 -->
    <input type="datetime">  <!-- 国际时间 -->
    <input type="datetime-local" value="12:00:00">  <!-- 本地时间 -->
</form>

<form action="http://www.baidu.com">
    <input type="text" autocomplete="on"> <!-- 保存提交内容 -->
    <input type="text" autofocus="on"> <!-- 获取焦点 -->
    <input type="text" form="form"> <!-- form 属性可设置到 input 里面 -->
    
    <input type="file" multiple>  <!-- 可选择多个文件 -->
    <input type="text" pattern="[\d]{4}" placeholder="请输入4位有效数字">  <!-- 正则表达式 -->
    <input type="image" src="">  <!-- 图片按钮 -->
    <input type="submit">
</form>
```
